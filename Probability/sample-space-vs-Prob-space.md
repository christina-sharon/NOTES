This is one of the most fundamental distinctions in probability theory. Nearly every modern probability text (including those used in ML and RL) starts from it.

The short answer is:

* **Sample space** = *What can happen?*
* **Probability space** = *What can happen, which events are allowed, and how likely are they?*

Let's build this carefully.

---

# Motivation

Suppose we toss a fair coin.

What are the possible outcomes?

[
\Omega={H,T}
]

This tells us **what outcomes exist**, but it tells us nothing about:

* probabilities,
* which collections of outcomes are measurable,
* random variables,
* expectations.

To do probability rigorously, we need more than just the outcomes.

This leads to the concept of a **probability space**.

---

# 1. Sample Space

## Definition

The **sample space** is the set of all possible elementary outcomes of an experiment.

It is denoted by

[
\boxed{\Omega}
]

Examples:

### Coin

[
\Omega={H,T}
]

---

### Die

[
\Omega={1,2,3,4,5,6}
]

---

### Two Coins

[
\Omega=
{
HH,HT,TH,TT
}
]

---

### Lifetime of a Machine

Possible outcomes are every positive real number.

[
\Omega=[0,\infty)
]

Notice this is infinite.

---

The sample space answers only one question:

> **What outcomes are possible?**

Nothing more.

---

# 2. Probability Space

A probability space contains **three objects**.

[
\boxed{(\Omega,\mathcal F,P)}
]

where

* (\Omega) = sample space
* (\mathcal F) = sigma-algebra (allowed events)
* (P) = probability measure

The sample space is only the **first component**.

---

# Think of it like a game

Imagine a game board.

The board itself is

[
\Omega.
]

The legal moves are

[
\mathcal F.
]

The scoring rules are

[
P.
]

Together they define the entire game.

---

# Component 1

## Sample Space

[
\Omega
]

Possible outcomes.

Example:

[
\Omega={1,2,3,4,5,6}
]

---

# Component 2

## Sigma-algebra

This is usually the mysterious part.

It is written

[
\mathcal F.
]

It is simply

> the collection of events to which we are allowed to assign probabilities.

An event is just a subset of the sample space.

Example

Rolling a die

[
\Omega={1,2,3,4,5,6}
]

Events:

"Even"

[
{2,4,6}
]

"Odd"

[
{1,3,5}
]

"Greater than 4"

[
{5,6}
]

Each of these belongs to

[
\mathcal F.
]

---

For finite sample spaces,

usually

[
\mathcal F=2^\Omega
]

(the power set),

meaning

**every subset is measurable**.

---

For continuous spaces this is **not true**, which is why measure theory introduces sigma-algebras.

---

# Component 3

## Probability Measure

The probability function

[
P
]

assigns probabilities.

For a fair die,

[
P({1})=\frac16
]

[
P({2})=\frac16
]

etc.

For an event

Even

[
P({2,4,6})
==========

# \frac36

\frac12.
]

---

So

[
P
:
\mathcal F
\rightarrow
[0,1].
]

It takes an event and returns a probability.

---

# Visual Picture

```
Probability Space

(Ω, F, P)

│
├── Ω
│     possible outcomes
│
├── F
│     measurable events
│
└── P
      assigns probabilities
```

---

# Example

Rolling a die.

### Sample space

[
\Omega
======

{
1,2,3,4,5,6
}
]

---

### Sigma-algebra

For finite spaces,

[
\mathcal F
==========

2^\Omega
]

meaning every subset.

Examples

[
{1}
]

[
{2,4,6}
]

[
{5,6}
]

etc.

---

### Probability Measure

[
P({i})
======

\frac16
]

Then

Even numbers

[
P({2,4,6})
==========

\frac12.
]

---

Hence

[
(\Omega,\mathcal F,P)
]

is a probability space.

---

# Why isn't the sample space enough?

Suppose

[
\Omega=[0,1].
]

There are infinitely many subsets.

Some are so pathological that mathematicians proved **you cannot consistently assign probabilities to all of them**.

So we only assign probabilities to "nice" subsets.

Those subsets form

[
\mathcal F.
]

This is one of the main reasons measure theory exists.

---

# Relation to Random Variables

A random variable

[
X
]

is **not defined on the sample space alone**.

It is defined on the **probability space**:

[
X:\Omega\rightarrow\mathbb R.
]

The probabilities that (X) induces come from the probability measure (P).

Without (P), you can compute values of (X), but not probabilities, expectations, or variances.

---

# Connection to Machine Learning

In ML we often write

[
x\sim P(X).
]

Behind this simple notation is a complete probability space.

For example:

* Sample space: all possible images.
* Events: sets of images (e.g., "contains a cat").
* Probability measure: how likely each image is under the data-generating process.

Most ML texts hide the measure-theoretic details, but they are always present in the background.

---

# Connection to Reinforcement Learning

In an MDP:

* **Sample space**: all possible trajectories
  [
  \omega=(s_0,a_0,r_1,s_1,\ldots)
  ]
* **Probability measure**: induced by the transition probabilities and the policy.
* **Probability space**:
  [
  (\Omega,\mathcal F,P_\pi)
  ]

where (P_\pi) depends on the policy (\pi).

Expected returns such as

[
\mathbb E_\pi[G]
]

are expectations with respect to this probability space.

---

## Summary Table

| Concept                          | Sample Space (\Omega)           | Probability Space ((\Omega,\mathcal F,P)) |
| -------------------------------- | ------------------------------- | ----------------------------------------- |
| Meaning                          | All possible outcomes           | Complete mathematical model of randomness |
| Contains outcomes?               | Yes                             | Yes                                       |
| Contains events?                 | No (only implicitly as subsets) | Yes, via (\mathcal F)                     |
| Contains probabilities?          | No                              | Yes, via (P)                              |
| Enough to compute probabilities? | No                              | Yes                                       |
| Used in rigorous probability?    | As one component                | Always                                    |

A good mental model is:

* **Sample space** = the universe of possible outcomes.
* **Probability space** = the universe **plus** the rules for which events are measurable and how probability is assigned to them. This distinction becomes essential once you move from finite examples to continuous probability, stochastic processes, and reinforcement learning.