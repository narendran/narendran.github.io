---
layout: post
title:  "Differentiable Programming: Current and Future Implications on Software Development"
date:   2020-05-06 18:00:00
categories: differentiable-programming software future
---

My last technical blog was on [MongoDB vs. RethinkDB](https://ntvita.com/2015/06/04/mongo-vs-rethink.html) and it has been ~5 years since then!

Why the gap?

This article is about how a collection of ideas are converging towards an exciting future for software development. I will give links to individual topics wherever possible though.

{:toc}

# Differentiable Programming

Differentiable programming allows you to write functions that could be differentiated with respect to their inputs. Here is a simple example.

```python
def squared(x): return x**2
print(squared(4)) #  x^2 = 16
print(grad(squared)(4)) #  2*x = 8
print(grad(grad(squared))(4)) #  2 for all values of x.
```

# Current Applications: Natural Sciences, Finance, Software 2.0

Differentiation has been widely applied in scientific computing for decades now. Following are some examples, but you can find more in [1]:
1. [Finance] Black Scholes equation for pricing options.
2. [Physics] Equation of motion, Heat dissipation, Brownian motion.
3. [Biology] Population growth models, neuron action potentials.
4. [Chemistry] Rate equation - rate of change of concentration of reactants and products.
5. [Archaeology] Carbon dating.
6. [Software Development] Software 2.0 via machine learning with backpropagation.

We have had programming languages for this atleast since the mid-1950s with the introduction of Fortran. But the landscape has evolved a lot since then. Today, there are Domain Specific Languages like MatLab, R, Julia and Wolfram. Fortran itself would fall in this class. There are also General Purpose Programming languages like C++ and Python which have extensions to perform efficient scientific computing. E.g. Python has specialized libraries like Numpy, Scipy, Sympy, Sklearn, Pandas, great plotting libraries like matplotlib and to help scientists communicate better, we have literate programming tools like iPython and Jupyter Notebooks.

To make the conversation easier, let's pick a specific area and programming language. Let's talk about the plethora of work being done on Machine Learning (ML) using Python. I still see a dochotomy in thought and in code from where science ends and software begins today. For instance, where do a TF SavedModel or pickled PyTorch models fit today? At best, you can think of the model as a learned function with clean API's, but still these extensions and DSLs are currently being viewed and used as blackbox function approximators.

Secondly, these frameworks are too complex and have too many assumptions. At least the latter can be worked around by using more primitive components of the framework like TF. But still, I would argue the complexity remains: When I started working on ML (~2 years back) I was astounded at the level of complexity TF incorporated. Is it a library? Is it a runtime? Is it a programming language? Is it even Python? Why is such complexity required. It is to provide speed and flexibility. Numerics, derivatives and parallelism (https://julialang.org/blog/2017/12/ml-pl/#fnref:tf). We got Numpy to take care of the Numerics. Automatic Differentiation to the rescue for derivatives and parallelism! Dynamic graph computation started using AD in 2017 [paper].


<JIT graph>

# In Software 2.0

**What if software can rewrite themselves over time?**

Meta-learning and other approaches to learning which can change this assumption that backpropagation is the only way we can learn.

<code snippet>

# Future Applications: Using Differentiation as a first-class programming primitive

Now, we have been able to differentiate inside programs for years now. There are languages and frameworks which are optimized for this. Why do these first-class differentiable programs matter?

<plot of thread vs request per second>

<Differentiate my bread toaster>
<More advanced examples using physics engine>

# How to get started?

<conclusion>

# References

1. Engineering Applications of Differential
equations, B. Sumithra [link](https://www.ijaiem.org/Volume6Issue7/IJAIEM-2017-07-13-30.pdf)
