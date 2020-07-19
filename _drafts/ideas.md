---
layout: default
#title: Ideas for Posts
---

# Ideas for posts

## Everyday statistics

### Instrumental variables and BMI (paper summary)

### Importance of understanding how data is generated

## Ethics, fairness and statistics

### Causality and fairness

### Model confidence

## Machine learning
### Machine learning vs statistical inference
- Introduce the two paradigms. Include distinctions:
  - Learning without noise / with noise
  - Inference where explanatory variables are control variables vs random
- Compare and contrast approaches
- How are they ultimately similar?

### Learning Uncertainty
- Standard ML, and how it doesn't directly deal with three sorts of uncertainty:
  1. Uncertainty in predictions given a fixed model
  1. Uncertainty in model parameters
  1. Uncertainty in the choice of model
- How the last two are really the same problem (e.g. compare with parameters vs hyper parameters)
- Illustrate with simple example (e.g. 1D model and linear regression / constant prediction)
- First a problem for regression but not classification
- Idea for dealing with problem 1 for regression -- non-parametric learning of all distribution parameters (e.g. mean and variance). Experiment to illustrate this. How well does it work?
- Bayesian methods for dealing with problem 2 (and 3?)
- Alternative approaches for dealing with problem 2 and 3 -- give the fitting algorithm flexibility to estimate confidence (and downweight the loss contribution where confidence is low). Flesh out details. Can this be recast as a "non-parametric" Bayesian approach?

## Deep learning theory

### Training neural networks through stochastic optimisation

### Approximate training through sparse feed-forward and back propagation

### Sparse neural networks (without weights) (find paper and review)

### Fast training on CPUs (intel paper review)

### CNNs -- ideas for extension
- random features (link to [this paper](https://www.inference.vc/dilated-convolutions-and-kronecker-factorisation/))
- tile coding and coarse coding -- link with convolutions
- thinking outside the grid -- random local linear maps instead of rigidly patterned convolutions. Can this make CNNs more robust to digitisation artefacts? Taking it further, should we first encode pictures using a random (rather than regular) pixel-map?

## Reinforcement learning

### A unified approach to RL
- All approaches involve learning a policy and / or value function.
- General framework for estimating both, and using a combination of Monte Carlo and iteration.
- How table updates can also be viewed as stochastic gradient descent
- How discrete actions and continuous actions can be combined by outputting probability distributions as actions.
- How deterministic policies + exploration noise are really stochastic policies.
- Can every gradient based RL algorithm be recast as some combination of generalised policy gradients (with an optional value estimate) plus Q-learning (possibly n-step)?

### RL and American option pricing
- Both ultimately solving the same problem, but in RL the strategy is primary whereas in option pricing the value function is primary.
- Is this just an interesting comparison or useful?

### RL and classical dynamics?
- RL used to approximately solve problems in variational calculus
- Can this be used, for example in semi-classical problems?

### RL and the brain
- What other signals do we receive that help us learn (anticipation, fear, frustration, curiosity, haste), etc and how could we create such signals for machines?

### RL and evolved priors
- We seem to learn quicker because of a preference for various types of actions (energy-conserving, not uncomfortable, etc). Can we provide similar motives to machines?

### Continuous actions spaces -- are they ever really necessary?
- Can we look at all actions as discrete (possibly integrating) processes? Perhaps with an urgency signal?

### Undirected RL
- How can we encourage machines to explore and understand their environment without a goal in mind?

### RL and human learning
- Comparison of how we learn new skills vs modern RL

## Paedagogy
### Review of gradient boosting
- How it works
- Viewing as gradient descent
- Optimising arbitrary cost functions

### Stochastic optimisation
- Review of methods (incl. cross-entropy method and evolutionary strategies)
- Comparison to gradient descent
- Pros and cons

### Deep generative models
- Review of GANs and Autoencoders

### Sequence models
- Review of different models
- Attention
- Transformers

### NLP
- Review of basic concepts
- Taxonomy NLP problems and techniques for solving them

### Going deep
- Review of strategies for effectively training very deep networks (e.g. successful CNNs)

### Implementing CNNs from scratch in Torch

### Implementing RNNs from scratch in Torch

