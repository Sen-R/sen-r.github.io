---
layout: post
mathjax: true
author: SR
title: Hill climbing
---

# Introduction

Hill climbing is a group of algorithms that perform [local search](post-todo). The basic idea is to iteratively move to higher and higher points until you reach a local optimum.

Suppose we are interested in finding a maximiser

$$ x^{*} \triangleq
   \underset{x \in \mathcal{X}}{\operatorname{arg\,max}} f(x) $$

where $\mathcal{X}$ is the *search space*. As with all local search algorithms, we must also suppose that there exists the concept of a neighbourhood $N(x) \subseteq \mathcal{X}$ of all points $x \in \mathcal{X}$.

For many problems there is no unique concept of a neighbourhood -- this is really an opportunity to insert some domain knowledge. The neighbourhood function could itself be parametrized, $N_\theta(x)$, e.g. to allow the algorithm to widen the search when far from an optimum and to narrow the search close to an uptimum.

# The algorithm

The basic hill climbing algorithm starts at an initial point $x_0$ (say, randomly chosen) and repeatedly applies the following iteration:

$$ x_{i+1} \leftarrow \underset{x \in n(x_i) \cup \{x_i\}}{\operatorname{arg\,max}} f(x).$$

The function $n(x)$ selects out a manageable subset of $N(x)$. It is the choice of $n(x)$ that distinguishes the various flavours of hill climbing:
* **Simple hill climbing**. 