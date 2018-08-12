# [PyMC3: Alternative Computational Engines](https://summerofcode.withgoogle.com/projects/#5512517883789312)
### My Google Summer of Code 2018 project
## Org: [NumFOCUS](https://github.com/numfocus)
## Sub-org: [PyMC](https://github.com/pymc-devs)
## Repository : https://github.com/pymc-devs/pymc4/
## Mentor: [Colin Carroll](https://github.com/ColCarroll), [Chris Fonnesbeck](https://github.com/fonnesbeck)


## Introduction
PyMC4 is a high-level probabilistic programming interface for TensorFlow. We use the capabilities of Edward2 and tensorflow_probability to make user-friendly, functional API. 

Edward2 provides us with distributions and some sampling techniques. We combine these to build a user focused API.



## Functional Design
Tensorflow and Edward 2 use a functional approach, where each Tensorflow program is defined as a function that takes a tensor as input and outputs a tensor. We extend this design to the PyMC4 API.


## Interceptors
Edward2 wraps a tensorflow distribution as a function and makes it interceptable.

We make use of these interceptions for sampling, keeping track of variables, etc.



## Collaboration with the Google tf.probability Team
The PyMC team  has been coordinating with the Google tensorflow/probability team to  fix existing and potential implementation problems of PyMC4 or Tensorflow Probability.  



## Work Done
### Tested context manager based API [Link](https://github.com/pymc-devs/pymc4/tree/pymc3_based_api)
 I started the project by trying to replicate the existing API of PyMC3. This design relied on context manager which kept track of random variables. I got this design to sampling stage. However we (PyMC team and I) soon realized that we are not making use of TensorFlow's functional design properly. 

### Functional API
The functional API of PyMC4 is an effort to extend the functional design of Tensorflow probability and Edward2 to PyMC4 and fully make use of all their capabilities.
 - Took the prototype designed by Josh Safyan and adopted it to our functional design.
 - Got the models to sample using HMC.
 - Reproduced the famous Eight Schools Model using PyMC4 comparing it with the PyMC3 implementation. [Link](https://gist.github.com/sharanry/193f06f139ccf1b90e176139238a4468)

### Solving the Graph growth Problem
 - There is problem of tensorflow graph growth while sampling or specifically while evaluating log probability. This problem has been demonstrated in [this](https://gist.github.com/sharanry/8564931ecab9054ad21e062cde077d46) notebook and [this](https://sharanry.github.io/post/the-tensorflow-graph-problem/) blog post. The tensorflow team is actively helping in solving this problem.
 
 ### Half Cauchy Distribution
 Tensorflow Probability lacks Half Cauchy distribution which is often used in many probabilistic models. The PR for adding this to PyMC4 is in the process of being merged.



## My Blog Posts 
- [Google Summer of Code 2018 with PyMC](https://sharanry.github.io/post/google-summer-of-code-2018-with-pymc/)

- [It's been a Month](https://sharanry.github.io/post/its-been-a-month/)

- [
Non-Centered Eight Schools Model with PyMC4](https://sharanry.github.io/post/eight-schools-model/)

- [The Tensorflow Graph Problem](https://sharanry.github.io/post/the-tensorflow-graph-problem/)

## My PRs
 - [MERGED] [Model context manager, primitive default sampling, random variable class](https://github.com/pymc-devs/pymc4/pull/1)
 - [MERGED] [Get mcmc sampling to work](https://github.com/pymc-devs/pymc4/pull/9)
 - [MERGED] [Add credits](
https://github.com/pymc-devs/pymc4/pull/16)
 - [MERGED] [Update Readme](https://github.com/pymc-devs/pymc4/pull/19)
 - [MERGED] [Merge functional](https://github.com/pymc-devs/pymc4/pull/20)
 - [OPEN] [A simple solution to work on the copy of the graph](https://github.com/pymc-devs/pymc4/pull/15)
 - [OPEN] [Add HalfCauchy distribution](https://github.com/pymc-devs/pymc4/pull/17)


## Credits
As PyMC4 builds upon TensorFlow, particularly the TensorFlow Probability and Edward2 modules, its design is heavily influenced by innovations introduced in these packages. In particular, early development was partially derived from a [prototype](https://github.com/tensorflow/probability/blob/9c2a4c8bbeddebded2b998027ec7111dcdfd9070/discussion/higher_level_modeling_api_demo.ipynb) written by [Josh Safyan](https://github.com/jsafyan/).