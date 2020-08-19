---
layout: post
mathjax: true
author: SR
title: Local search
---

# Introduction

Several mathematical problems boil down to minimising -- or more often finding the minimiser of -- a function:

$$ x^* \triangleq \underset{x \in \mathcal{X}}{\operatorname{arg\,max}} f(x) $$

where $\mathcal{X}$ is the *search space* (or feasible set), made up of all allowed values of $x$.

**Local search** is a class of algorithms that look for an optimum by sequentially searching through the search space, repeatedly moving from one point to another "nearby" point in the hope of finding progressively better solutions.

Local search algorithms share the following properties:
1. They find local, not global, optima.
2. They are *anytime* algorithms: if stopped early, they can provide the best solution they have found so far.
3. They require a well defined concept of a "neighbourhood": i.e. for any point $x \in \mathcal{X}$ that there exists a set $N(x) \subseteq \mathcal{X}$ of all points that are "near" $x$.

## Examples of local search

Examples of local search include:
* Hill climbing
* Random search
* Simulated annealing
* Tabu search

## Related search topics

Local search can be combined with other searching concepts:
* **Local beam search**. Beam search keeps a shortlist of $\beta$ candidate solutions at every step (instead of one). Local beam search involves searching through the neighbourhoods of these $\beta$ points to come up with a revised shortlist.
* **Gradient descent**. Where $\mathcal{X}$ is a manifold, $f$ is differentiable, and the gradient of $f$ can be practically calculated, this information can be used to inform local search.
* **Line-search / trust region**. These are used for search spaces that have notions of *direction* and *distance*. Line search involves first picking a direction and then solving a subproblem to determine how far to move in that direction; trust region involves picking a region that is well-approximated, analytically picking what looks like the best point in that region, and then updating the approximation.
* **Genetic algorithms**. In local search, each point gives rise to a child point by itself. In a genetic algorithm, there is a heuristic for combining two points to give rise to (generally two) child points.
* **Evolutionary strategies**. 