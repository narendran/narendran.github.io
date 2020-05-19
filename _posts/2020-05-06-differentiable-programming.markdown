---
layout: post
title:  "The Differentiable Bread Toaster: A Discontinuity in Modern Software Systems"
date:   2020-05-06 18:00:00
categories: differentiable-programming software future
---

In the last couple of years, I've had the opportunity to improve some highly-used software systems using recent developments in machine learning (ML). Amidst all the noise in developing and deploying ML models, there is an obvious discontinuity in thought-process and actual software development which has felt unnatural to me. The discontinuity is between the Java/C++/Python/Go programs we write as part of standard software development and the artifacts of ML (i.e. learned models). In this post, I will explain this discontinuity and a potential opportunity to address it using differentiable programming.

[6 minute read]

{:toc}

# What is Differentiable Programming

Differentiable programming allows you to write computer programs that could be differentiated with respect to their inputs. This has been possible for decades now either via numerical approximations to differentiation (which suffers from inaccuracies) or using symbolic differentiation techniques like what is done in Python's SymPy package and in Wolfram (which suffer from lack of speed and flexibility required in practice). Recent improvements in Automatic Differentiation has allowed libraries like AutoDiff, AutoGrad, and JAX (which is used in this post) to address these concerns enabling differentiation as a first-class tool in mainstream software development.

Following is a very simple example of a differentiable program. By the end of this post, I will give an idea of how composing such simple programs enables us to build software systems which were hitherto inconceivable.

```python
def squared(x):
  return x**2

print(squared(4)) #  x^2 = 16
print(grad(squared)(4)) #  First order derivative = 2*x = 8
print(grad(grad(squared))(4)) #  Second order derivative = 2 for all values of x.
```

# Current Applications and State of Differentiable Programs

Differentiation has been largely applied in scientific computing for decades now. Following are some domains where it is used today, and you can find more in [1]:
1. [Finance] Black Scholes equation for pricing options.
2. [Physics] Equation of motion, Heat dissipation, Brownian motion.
3. [Biology] Population growth models, Neuron action potentials.
4. [Chemistry] Rate equation to predict rate of change of concentration of reactants and products.
5. [Archaeology] Carbon dating.

Today, there are Domain Specific Languages like MatLab, R, Julia and Wolfram, and General-purpose Programming Languages like C++ and Python which have extensions to perform differentiation and other techniques required for scientific computing. E.g. Python has specialized libraries like Numpy, Scipy, Sympy, Sklearn, Pandas, great plotting libraries like matplotlib and to help scientists communicate better, there are literate programming tools like iPython and Jupyter Notebooks. However, when thought about in context of mainstream software development, they suffer from the following two problems.

Firstly, to make the discussion easier, let's pick a specific area and programming language say Supervised ML and Python. There is a dichotomy in thought and code when we think about where our classical programs end and supervised intelligence begins today. For instance, where do TensorFlow SavedModels and pickled PyTorch models fit in our software today? At best, we can think of them as opaque learned functions with rigid expectations of input and output. If I have to modify their functionality a little bit, there is a completely different set of tools and terminology we have to work with. This dichotomy shows through right from the code, to the developers' perception all the way to job listings from companies (like SWE, SWE-ML, ML-SWE, Research Engineer, Applied Scientist in ML etc.) and university courses/programs.

Secondly, today's Supervised ML frameworks are too complex and have too many assumptions (contributing to the dichotomy mentioned above). The latter can be worked around by using more granular components of the framework like TensorFlow when available. The argument on complexity still remains: When I got introduced to ML, I was astounded at the level of complexity libraries like Tensorflow and PyTorch had. What would I call them - library/runtime/programming language? Is it even Python? Even before I answered those questions, I had gotten used to the flow and deferred that inkling. Over time, I realized that bringing together the core pieces required for mainstream differentiable programming is non-trivial. As this [blog from Julia team](https://julialang.org/blog/2017/12/ml-pl/#fnref:tf) puts it, the core pieces are numerics, derivatives and parallelism.

I am excited to see the full, coherent suite coming together in Python. There is Numpy to take care of the numerics and excellent Automatic Differentiation libraries to take care of the derivatives and parallelism aspects while also allowing flexibility by differentiating through programming constructs like variables, loops and conditionals. Yay!

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

# Closing Thoughts

I believe the paradigm of differentiable programming can address the aforementioned discontinuity in modern software systems. To begin with, a differentiable program does not have to be as grand as the Tesla AutoPilot -- there are day-to-day heuristics-based engineering solutions like thread pool size optimization and service outage prediction [Sumit Nigam] which can solved more correctly and elegantly with differentiable programs. What is more beautiful is that besides democratizing the idea of continuously evolving programs, differentiable programming lets us leverage all the amazing things we have built already instead of learning from scratch all the time. Now, let's differentiate some bread toasters and throw in the heat equation!

*If our small minds, for some convenience, divide this glass of wine, this universe, into parts -- physics, biology, geology, astronomy, psychology, and so on -- remember that nature does not know it! - Richard P. Feynman*

# References

1. JAX on Github: https://github.com/google/jax
1. Engineering Applications of Differential
equations, B. Sumithra [link](https://www.ijaiem.org/Volume6Issue7/IJAIEM-2017-07-13-30.pdf)
2. Gordon Plotkin 2019 slides - One and a half simple differential programming languages
3. Implications from Andrej Karpathy - Software 2.0
4. 2017 - https://julialang.org/blog/2017/12/ml-pl/#what_might_a_tailor-made_ml_language_look_like
5. 2019 - https://fluxml.ai/2019/02/07/what-is-differentiable-programming.html
6. What every programmer should know about Mathematics [https://www.amazon.com/every-programmer-should-about-Mathematics-ebook/dp/B01FNVAYW4]
