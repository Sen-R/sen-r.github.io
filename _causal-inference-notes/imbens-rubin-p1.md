---
layout: post
title: Causal Inference Book Notes — Part 1
mathjax: true
tikzjax: true
---

*These are my personal notes on Part 1 of the book "Causal Inference for Statistics, Social, and Biomedical Sciences" by Imbens and Rubin.*

# Chapter 1

## Introduction

### What's a causal effect?

Causal statements (often of the form "$Y$ because of $X$") are commonly used in everyday life. Underlying such statements is the idea that things could have been otherwise: i.e. if $X$ had instead been $\tilde{X}$, would $Y$ still be true? However, statistics texts tend to shy away from discussing causality (or even actively discourage its discussion).

Examples from the book:
* "My headache went away because I took an aspirin." What would have happened to my headache if I hadn't taken an aspirin?
* "She got a good job last year because she went to college." What sort of job would she have got if she hadn't gone to college?
* "She has long hair because she is a girl." What if she weren't a girl?

> "The fundamental notion underlying our approach is that causality is tied to an **action**... applied to a **unit**. ... For our purposes, the same physical object or person at a different time is a different unit. From this perspective, a causal statement presumes that, although a unit was (at a particular point in time) subject to, or exposed to, a particular action... the same unit could have been exposed to an alternative action."

Some key points to draw out:
* Causal effects are individual and time-specific. I.e. the effect of aspirin on my headache today is not *necessarily* the same as the effect of aspirin on my headache last week, nor is it the same as the effect of aspirin on my wife's headache today.
* Although interventions or actions seem either active (take an aspirin) or passive (don't take an aspirin), they are actually formally symmetric for the purpose of this approach -- e.g. not taking a medication is an action in itself. This means that some of the casual language examples above do not fit into this framework well, i.e. where the alternative treatment is ill-defined. For example, what exactly is the alternative to the person being a girl in the final example? The authors claim that an:
> "explicit description of the intervention makes the question a plausible one in our framework."
* This requirement seems to me related to the SUTVA assumption discussed later in the text -- in particular the equal treatment part of the assumption. If the counterfactual is not precisely defined, then there are range of alternative interventions, violating the equal treatment assumption. I wonder though whether this assumption could be relaxed as part of putting potential outcomes framework on a more probabilistic footing?

### Learning causal effects

As discussed above, causal effects involve the quantifying the effects of actions happening to units. Effects are quantified in terms of the difference in outcome versus a (counterfactual) alternative action having been applied.

It is important to stress that the counterfactual action should be considered to be applied *to the same unit*, e.g. to the same individual at the same time as the original action. This means the outcome under the alternative action is genuinely counterfactual: i.e. impossible to observe directly. [Puzzle: what is the ontology of such a fundamentally hypothetical outcome? It seems that the usefulness of the potential outcomes framework is to reason about potential future outcomes, is there really need to postulate "real" but fundamentally unobservable aternatives to past events?]

In turn, this implies that it is impossible to *learn* about a causal effect from observing a single unit. (The book makes a distinction between causal effects being "well-defined" for a single unit, but unlearnable for a single unit.) The only way to learn about causal effects is to observe outcomes for multiple units. Note that this could be the same individual at many times, many individuals at the same time, or a mix of the two.

**However**, even to learn a causal effect from multiple units, one must make further assumptions. For example, imagine there are two units, two treatment levels and two potential outcomes. Taking the units together, this means there are four treatment levels for the system, four potential outcomes, and six (i.e. $\binom{4}{2}$) comparisons between pairs of potential outcomes that could define a causal effect.

So, to learn anything, we must make further assumptions about the relationships between units and treatments to collapse these spaces. These assumptions are called **exclusion restrictions**: they are assumptions that *exclude* certain possibilities in order to make learning feasible.

**Stable unit treatement value assumption (SUTVA):** This is the first exclusion assumption introduced in the book. In fact, it comprises two assumptions:
1. We exclude the possibility of a treatment applied to one unit having an effect on another unit. For example, if I take an aspirin, we *assume* it can have no effect on your headache.
1. We exclude the possibility of treatments having intrinsic variation. For example, suppose you and I are both contemplating taking aspirin: we have two tablets in front of us. In reality, these are different tablets and there are now *three* treatment levels: $$ \left\{ \textrm{no aspirin}, \textrm{aspirin}_1, \textrm{aspirin}_2 \right\} $$. The SUTVA assumption *excludes* the possibility of the two aspirin tablets having different effects (e.g. because they are from different manufacturers, or from different batches) and *assumes* the two tablets are effectively equivalent for the purpose of causal inference. Note that another way treatments can differ is in how they are administered (e.g. whether the individual chose to take a treatment as opposed to being assigned to receive it).

The SUTVA assumption can be challenging for some problems.

For example, in economics and social sciences, there are often impacts on others from one person receiving a treatment. For example, providing one person training might impact employment outcomes for their peers. Similarly, the impact of immunisation depends on how many others have been immunised. Two strategies for dealing with such issues are:
1. To redefine units at a more coarse-grained level, e.g. define a school to be a unit.
2. To limit the number of units assigned to a particular treatment to minimise interaction effects (i.e. measure *partial equilibrium* effects).

Where there is genuine variability in treatments, one could randomise allocation (so that the randomly allocated tablet is the "one" treatment), or coarsen the outcome definition to reduce the impact of variation (e.g. dead versus alive instead of graded health status). [Puzzle: again, I wonder though whether this is really an artifact of the non-probabilistic manner in which the framework is set up. I.e. could we not naturally incorporate variation in a probabilistic setting?]

### Formalism

Let us assume SUTVA with $N$ units. Denote by $\mathbb{Y}$ the set of possible outcomes and by $\mathbb{T}$ the set of possible treatments.

* We can define a treatment indicators $W_i \in \mathbb{T}$, indexed by $i \in \{1, \ldots, N\}$, such that $W_i$ indicates the treatment assigned to unit $i$.
* We also define potential outcomes functions $Y_i : \mathbb{T} \to \mathbb{Y}$, again indexed by $i$, such that $Y_i(T)$ is the potential outcome for unit $i$ were treatment $T \in \mathbb{T}$ to be applied.
* Finally, we define $Y^\mathrm{obs}_i$ to denote realised (and possibly observed) outcomes for the units, i.e. $Y^\mathrm{obs}_i \triangleq Y_i(W_i)$.

Notice that the formalism is not probabilistic so far. [Although it should be feasible to turn $Y_i$ into random variables?]

The above information is still insufficient to infer causal effects of treatments. This is because we still do not know *how* treatments were allocated to units: i.e. the **assignment mechanism**. The book gives a medical example for why this is important: the observed outcomes where patients are randomly allocated to surgery or drug treatment may be quite different to observed outcomes where a doctor prescribes surgery or drugs based on their assessment of which is likely to work best for each patient. If we then average over the patients to estimate average causal effect of drugs versus surgery, we could draw quite different conclusions. [This is related to the concept of *confounding*: i.e. where treatment assignment is determined by a property that also affects treatment outcomes.] This is the subject of much of the rest of the book.

If the treatment assignment isn't completely random, it must depend on certain properties of the units. In turn, these properties must be known prior to treatment. These properties are called *pre-treatment variables* or *covariates*, and are denoted by a $K$-component row vector $X_i$ for unit $i$, where $K$ is the number of covariates. The book describes three uses for covariates:
1. To provide a more precise description of population-level effects, i.e. by explaining some of the variation in outcomes in terms of differences in covariates.
1. To provide sub-population level estimates of causal effects because of interest in understanding these.
1. Most importantly in this context, where the value of the covariate affects the assignment mechanism and potential outcomes. The basic idea here is that by restricting analyses to subpopulations that are homogeneous with respect to covariates, we can remove confounding and thus estimate causal effects.

Finally we turn to measures of causal effects, called **causal estimands**. For simplicity, consider a binary treatment: $$\mathbb{T} = \{0, 1\}$$. Two obvious measures of *unit-level causal effects* are simple differences and ratios,
$$Y_i(1) - Y_i(0)$$ and $$Y_i(1)/Y_i(0)$$. Generally, we would want to summarise causal effects over a population (called a *finite sample* in the book) or a sub-population; this leads to average differences:

$$\tau_\mathrm{fs} = \frac{1}{N}\sum_{i=1}^{N}(Y_i(1) - Y_i(0))$$.

We may further generalise by averaging where certain conditions are satisfied. These include:
1. Average effects for sub-populations defined by certain covariate values, e.g. over all females.
2. Average effects for sub-populations who received (or didn't receive) the treatment.
3. Average effects for sub-populations defined in terms of their potential outcomes.

Other generalisations include taking medians or other functions of potential outcomes. In general however (for the binary treatment case), causal estimands can be expressed as row-exchangeable functions of the form

$$\tau = \tau(\mathbf{Y}(0), \mathbf{Y}(1), \mathbf{X}, \mathbf{W})$$

where $\mathbf{Y}$, $\mathbf{X}$ and $\mathbf{W}$ are the column vectors formed from the components $Y_i$, $X_i$ and $W_i$ respectively.

### Pitfalls of looking solely at observed outcomes

The book gives an example of Lord's paradox to illustrate the importance of considering potential outcomes versus just observed outcomes. When observed outcomes are solely used, there is a temptation to draw causal inferences by making comparison across units (e.g. the same person across time, in the case of the impact of a diet change). The trouble is that (without carefully making further assumptions), such comparisons do not automatically generate causal conclusions.

### Causal inference and missing data

The book treats causal inference as a missing data problem. If $Y_i(T_i)$ were observable for all $T_i \in \mathbb{T}$, causal estimation would be straightforward.

In missing data problems, the challenge is to infer the missing data from the data available. To do so, one needs to model both the relationship between the observed and missing data, but also the mechanism by which data went missing. The latter is, in causal inference, the problem of modelling the treatment assignment mechanism.
