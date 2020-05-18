---
layout: post
title:  "The Differentiable Bread Toaster: A Discontinuity in Modern Software Systems"
date:   2020-05-06 18:00:00
categories: differentiable-programming software future
---

In the last couple of years, I've had the opportunity to focus full-time on keeping up with the latest developments in machine learning (ML). Fortunately, I've been able to improve some highly-used software systems using that knowledge. When building intelligent systems today, there is a discontinuity in thought and software development process which feels unnatural to me. The discontinuity is between the standard Java/C++/Python/Go programs we write in classical notion of software engineering and the artifacts of ML (i.e. learned models). This article is a collection of ideas related to differentiable programming and how it can address that gap.

[6 minute read]

{:toc}

# What is Differentiable Programming

Differentiable programming allows you to write computer programs that could be differentiated with respect to their inputs. This has been possible for decades now -- we can use numerical approximations to differentiation which suffers from inaccuracies or using symbolic differentiation techniques like what is done in Python's SymPy package and in Wolfram which suffer from lack of speed and flexibility required for more practical applications. Recent improvements in Automatic Differentiation has allowed libraries like AutoDiff, AutoGrad, and JAX (which is used in this post) to address this concern enabling differentiation in mainstream software development. Following is a very simple example of a differentiable program. By the end of this blog post, I will give an idea of how composing such programs can enable us to build systems which were hitherto unachievable.

```python
def squared(x):
  return x**2

print(squared(4)) #  x^2 = 16
print(grad(squared)(4)) #  First order derivative = 2*x = 8
print(grad(grad(squared))(4)) #  Second order derivative = 2 for all values of x.
```

# Current Applications of derivatives: Natural Sciences, Finance

Differentiation has been widely applied in scientific computing for decades now. Following are some examples, but you can find more in [1]:
1. [Finance] Black Scholes equation for pricing options.
2. [Physics] Equation of motion, Heat dissipation, Brownian motion.
3. [Biology] Population growth models, neuron action potentials.
4. [Chemistry] Rate equation - rate of change of concentration of reactants and products.
5. [Archaeology] Carbon dating.

We have had programming languages for this atleast since the mid-1950s with the introduction of Fortran. But the landscape has evolved a lot since then. Today, there are Domain Specific Languages like MatLab, R, Julia and Wolfram. Fortran itself would fall in this class. There are also General Purpose Programming languages like C++ and Python which have extensions to perform efficient scientific computing. E.g. Python has specialized libraries like Numpy, Scipy, Sympy, Sklearn, Pandas, great plotting libraries like matplotlib and to help scientists communicate better, we have literate programming tools like iPython and Jupyter Notebooks.

To make the conversation easier, let's pick a specific area and programming language. Let's talk about the plethora of work being done on Machine Learning (ML) using Python. Firstly, I still see a dochotomy in thought and in code from where science ends and software begins today. For instance, where do a TF SavedModel or pickled PyTorch models fit today? At best, you can think of the model as a learned function with clean API's, but still these extensions and DSLs are currently being viewed and used as blackbox function approximators. We still need to worry about reshaping tensors, writing SWIG wrappers to move between languages etc.

Secondly, these frameworks are too complex and have too many assumptions. At least the latter can be worked around by using more primitive components of the framework like TF. But still, I would argue the complexity remains: When I started working on ML (~2 years back) I was astounded at the level of complexity TF incorporated. Is it a library? Is it a runtime? Is it a programming language? Is it even Python? Why is such complexity required. It is to provide speed and flexibility. Numerics, derivatives and parallelism (https://julialang.org/blog/2017/12/ml-pl/#fnref:tf). We got Numpy to take care of the Numerics. *Automatic Differentiation* to the rescue for derivatives and parallelism! Dynamic graph computation started using AD in 2017 [paper].

<JIT graph>

# Using Differentiation as a first-class programming primitive

A computer program has historically meant to be a set of human defined rules which take an input X and outputs Y. On a higher level, humans observe actual physical processes, model them into computer programs and automate those processes. f(x,y) = x + y will always return x + y irrespective of the actual function it approximates in reality. When the actual physical processes change, we have channels like product forums, monitoring etc. to detect a shift, re-design, re-implement, rinse and repeat.

But.. what if software can rewrite themselves over time? What if we are continually feeding soft rules into the software and software keeps improving over time. Thanks to representation learning techniques in ML, we can no write software for things which were previously impossible to think about or have been ludicrously hard. To test out this thought, I implemented an individual artificial neuron in JAX ([code](https://github.com/narendran/differentiable-programming/tree/master/jaxnn)) and trained it towards a simple objective -- i.e. given three numbers output the second number. It learns it with a few dozen examples. Composing this upward we get differentiable data structures and programming constructs like Attention, CNNs, and RNNs which could be considered differentiable equivalents of hash maps, image filters and loops. Now would we use a hashmap to process a text document? That is a question for a different blog, but you get the idea.

Let's think of this from the other direction. I have a physical process, and I have very little understanding on how it works but I can observe how it operates under different inputs. To make things concrete, let's consider a bread toaster which can take different number of bread slices. I have been manually stopping my toaster all these days by constantly peeping into my toaster to see how much toasting is done. I decide to write some code.

V1 - Fixed Linear Toasting time

V2 - Linear Toasting Time, but I don't know the exact relationship.

V3 - Polynomial Toasting Time, and I know it sort of fluctuates.

I've uploaded my differentiable bread toaster as well ([code](https://github.com/narendran/differentiable-programming/blob/master/bread_toaster/bread_toaster.py)). We can do much more by adding further known phenomena like the equation for heat dissipation, structure of the grill inside the toaster etc. Also I am referring to this idea on re-writeable software when I am talking about differentiable programs because the idea of learning via back-propagation has been widely proven and recognized at this point.

To expand from the example where we bias a learning program using a sine curve, imagine what other biases in applications like the following:

1. Differentiable [Ray Tracers](https://people.csail.mit.edu/tzumao/diffrt/) - Give the best ray trace given inputs like camera parameters, lighting etc.
2. Differentiable [Physics Engine](https://arxiv.org/pdf/1611.01652.pdf) for robotics
2. [Differentiable Sorting](https://arxiv.org/abs/2002.08871)
3.  Put a differentiable [camera calibration system](http://openaccess.thecvf.com/content_WACV_2020/html/Riba_Kornia_an_Open_Source_Differentiable_Computer_Vision_Library_for_PyTorch_WACV_2020_paper.html) into a gaze prediction model
4. Even learn metrics like used in [audio processing](https://arxiv.org/abs/2001.04460), evaluative metrics for [natural language tasks](https://arxiv.org/abs/2004.04696).

To get more grand, AutoPilot - Plug in high-precision rules or even better, models for individual aspects of driving into a differentiable program. The components could be how a stop sign or traffic lights look like.

# Building intelligent software systems

Differentiable programming completely blurs the lines between engineering and intelligence and allows us to model seemingly all possible physical processes more efficiently with known biases. Imagine what all we could build now! A learning program does not have to be grand -- there are also more day-to-day engineering problems like optimizing the size of the thread pool and determining time to outage as seen from Sumit Nigam's book. These are very useful problems that can be solved more efficiently with derivatives. This paradigm of programming lets us leverage all the amazing things we have done with converting physical processes into programs so far, and quickly build more complex and hitherto hard-to-implement systems on top of it. This is a direction I am super-excited about since it radically opens up the domain of things we can make automate and make more efficient as engineers.

*If our small minds, for some convenience, divide this glass of wine, this universe, into parts -- physics, biology, geology, astronomy, psychology, and so on -- remember that nature does not know it! - Richard P. Feynman*

(This is a living blog, and I will keep updating this blog post as I come to know any developments in this direction. Stay tuned.)

# References

1. JAX on Github: https://github.com/google/jax
1. Engineering Applications of Differential
equations, B. Sumithra [link](https://www.ijaiem.org/Volume6Issue7/IJAIEM-2017-07-13-30.pdf)
2. Gordon Plotkin 2019 slides - One and a half simple differential programming languages
3. Implications from Andrej Karpathy - Software 2.0
4. 2017 - https://julialang.org/blog/2017/12/ml-pl/#what_might_a_tailor-made_ml_language_look_like
5. 2019 - https://fluxml.ai/2019/02/07/what-is-differentiable-programming.html
6. What every programmer should know about Mathematics [https://www.amazon.com/every-programmer-should-about-Mathematics-ebook/dp/B01FNVAYW4]
