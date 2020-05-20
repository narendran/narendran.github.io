---
layout: post
title:  "The Differentiable Bread Toaster: A Discontinuity in Modern Software Systems"
date:   2020-05-20 10:00:00
categories: differentiable-programming software future
---

In the last couple of years, I've had the opportunity to improve some highly-used software systems applying recent developments in machine learning (ML). Amid all the joys and the noise in developing and deploying ML models in production, there is a nagging discontinuity in both the thought-process and actual software development which has felt unnatural to me. The discontinuity is between the Java/C++/Python/Go programs we write as part of standard software development and the artifacts of ML i.e. learned models. In this post, I will quickly describe the problem and a potential opportunity to address it using differentiable programming.

[8 minute read]

# What is Differentiable Programming

Differentiable programming allows you to write computer programs that could be differentiated with respect to their inputs. This has been possible for decades now either via numerical approximations to differentiation (which suffers from inaccuracies) or using symbolic differentiation techniques like what is done in Python's SymPy package and in Wolfram (which suffers from lack of speed and flexibility required in practice). Recent improvements in Automatic Differentiation has allowed libraries like AutoDiff, AutoGrad, and JAX (which is used in this post) to address these concerns enabling differentiation as a first-class tool in mainstream software development.

Following is a very simple example of a differentiable program. By the end of this post, I will give an idea of how composing such simple programs enables us to build software systems which were hitherto hard to build or even inconceivable.

```python
def squared(x):
  return x**2

print(squared(4)) #  x^2 = 16
print(grad(squared)(4)) #  First order derivative = 2*x = 8
print(grad(grad(squared))(4)) #  Second order derivative = 2 for all values of x.
```

# Current Applications and State of Differentiable Programs

Differentiation has been largely applied in scientific computing for decades now and following is a small sample from the application domains.
1. Finance: Black Scholes equation for pricing options.
2. Physics: Equation of motion, Heat dissipation, Brownian motion.
3. Biology: Population growth models, Neuron action potentials.
4. Chemistry: Rate equation to predict rate of change of concentration of reactants and products.
5. Archaeology: Carbon dating.
6. Web: Content ranking, Click prediction.

And we have lots of tools to perform differentiation using computers. Today, there are Domain Specific Languages like MatLab, R, Julia & Wolfram, and General-purpose Programming Languages like C++ and Python which have extensions to do differentiation. However, when thought about in the context of mainstream software development, they suffer two problems.

Firstly, to make the discussion easier, let's pick a specific area and programming language, say Supervised ML and Python. There is a dichotomy in thought and code when we think about where our classical programs end and supervised "intelligence" begins today. For instance, where do TensorFlow SavedModels and pickled PyTorch models fit in our software? At best, we can think of them as opaque learned functions with rigid expectations on inputs and outputs. As a software developer if I have to modify their functionality a little bit, there is a completely different set of tools and terminology I have to work with -- let's call it the [Software 2.0](https://medium.com/@karpathy/software-2-0-a64152b37c35) workflow. This dichotomy shows through right from the code, to the developers' perception, the surrounding workflow, inter-team coordination and bubbles up all the way to the job listings from companies (like SWE, SWE-ML, ML-SWE, Research Engineer, Applied Scientist in ML etc.) and university courses/programs.

Secondly, today's Supervised ML frameworks are too complex and have too many assumptions built in. The latter can be worked around by using more granular components of the framework like TensorFlow. The argument on complexity still remains. When I got introduced to ML, I was astounded at the level of complexity in systems like Tensorflow and PyTorch. What are they? Libraries/runtimes/programming languages? Even before I answered those questions, I had gotten used to the workflow and deferred thinking about it. Over time I realized that bringing together the core pieces required for mainstream machine learning is very, very hard. As this [blog from Julia team](https://julialang.org/blog/2017/12/ml-pl/#fnref:tf) puts it, machine learning is heavy on numerics, derivatives and parallelism which explains the complexity in developing ML systems of today.

In that backdrop, it is exciting to see a coherent suite for ML coming together in Python. There is always numpy to take care of the numerics. Recent developments in well-thought Automatic Differentiation libraries can take care of the derivatives and parallelism aspects while also allowing programming flexibility by differentiating through constructs like variables, loops and conditionals. Woohoo! Ok, what can we do with this capability?

# Using Differentiation as a first-class programming primitive

To some approximation, software developers observe how humans communicate and exchange in real world and model those behaviors in computer programs. In this paradigm, `f(x,y) = x + y` will always return `x + y` irrespective of the actual real-world function `f` has to approximate. And when the underlying assumptions on real-world behaviors do change, we have channels like monitoring, product forums, brand analysis etc. to detect a shift in expectations, re-design, re-implement, rinse and repeat.

But.. what if programs can automatically adapt and rewrite themselves over time? Like the way humans grow intelligent by composing knowledge extracted from daily observations on top of existing knowledge, can we continually feed soft rules into the program and make it increasingly aware of its purpose in life? Yes, we can. A ~20 line artificial neuron (**[code](https://github.com/narendran/differentiable-programming/tree/master/jaxnn)**) could arguably be the smallest unit of such a composable, learning program. And here is a **[tiny demo](https://github.com/narendran/differentiable-programming/blob/master/jaxnn/jaxnn_test.py#L57)** where we learn the rule "given three numbers, always return the second number". The differentiable program learns it with just 20 examples! Composing this idea of an artificial neuron with some structural assumptions, we get differentiable data structures and programming constructs like Attention, RNNs, Pooling techniques and even CNNs. These could be considered differentiable equivalents of hashmaps, loops, conditionals and image filters. So from latest trends in ML, we have been exploiting differentiable image filters to make sense of images and differentiable hashmaps to keep track of the words in a document.

We don't need to stop with the differentiable versions of data structures and programming constructs.

Let's look at programming from the other direction i.e. from top to bottom. I have a physical process I want to emulate, and I have very little understanding of how it works. However, I can observe how it operates under different inputs. To help our imagination, let's consider a simple bread toaster (because... why not?) which can take in different number of bread slices, say `N`, and toasts them in an unknown `f(N)` seconds. I have been manually powering down this toaster all these days and I really want to automate it. Let's consider three hypotheses about `f(N)`.
1. `f(N) = 30 * N` // It says 30 seconds on the toaster's manual, no learning needed.
2. `f(N) = 30 * N` // Its not on the manual, needs a learning program.
3. `f(N) = 7th order Taylor approximation of sin(N)` // Its not on the manual, needs some biased learning program.

Our differentiable bread toaster (**[code](https://github.com/narendran/differentiable-programming/blob/master/bread_toaster)**) can handle all these cases now. And we can improve its accuracy further by adding well-known physical phenomena like the equation for heat dissipation + structure of the grill inside the toaster and Automatic Differentiation would effortlessly differentiate it for you. Similar ideas have been seen in robotics with differentiable physics engines, improving computer vision with differentiable modules for image transformation + camera calibration and dramatically improving computer graphics rendering using differentiable ray tracers. Tesla's AutoPilot can be framed as a gigantic differentiable program where we plug in high-precision algorithms or learned models for different aspects of driving and compose them in a principled manner with appropriate differentiable data structures and algorithms to output steering, braking and acceleration. As we can see, the possibilities are endless.

# Let's build!

I strongly believe differentiable programming can address the aforementioned discontinuity in modern software systems by seamlessly blending hand-coded and learned rules. Plus, we can leverage all the existing hard-earned, well-tested knowledge on algorithms and data structures to tackle grander challenges in software engineering. It's time to differentiate our bread toasters and build the next "AutoPilot".

<div style="background-color:rgba(0, 0, 200, 0.1); vertical-align: middle; padding:20px; margin: 10px; border-radius: 15px;">
  If our small minds, for some convenience, divide this glass of wine, this universe, into parts -- physics, biology, geology, astronomy, psychology, and so on -- remember that nature does not know it!
  - Richard P. Feynman
</div>

# References

[JAX](https://github.com/google/jax), [Engineering Applications of Differential equation](https://www.ijaiem.org/Volume6Issue7/IJAIEM-2017-07-13-30.pdf), [Differential programming languages](https://pages.cpsc.ucalgary.ca/~robin/FMCS/FMCS2019/slides/GordonPlotkin-FMCS2019.pdf), [Software 2.0](https://medium.com/@karpathy/software-2-0-a64152b37c35), [Tailor-made ML language](https://julialang.org/blog/2017/12/ml-pl/#what_might_a_tailor-made_ml_language_look_like), [Differentiable Programming](https://fluxml.ai/2019/02/07/what-is-differentiable-programming.html)
