# SPH Volume Rendering

Make it possible to volume render SPH data in yt.

Background on SPH formalism and visualization:

* The paper describing the SPLASH visualization software (http://users.monash.edu.au/~dprice/splash/): https://doi.org/10.1071/AS07022
* A more pedagogical review article: https://www.annualreviews.org/doi/abs/10.1146/annurev-astro-081309-130914
* "Smoothed Particle Hydrodynamics and Magnetohydroynamics" by Dan Price: https://arxiv.org/abs/1012.1885 (in particular Sections 1, 2, and 4)
* Review: Kd-tree Traversal Algorithms for Ray Tracing. See http://onlinelibrary.wiley.com/doi/10.1111/j.1467-8659.2010.01844.x/pdf
* cykdtree, the cython KDTree library by Meagan Lang we've been using for this project: https://github.com/cykdtree/cykdtree
* Splotch: visualizing cosmological simulations. See http://iopscience.iop.org/article/10.1088/1367-2630/10/12/125006/meta

This work will be happening in a yt branch we call "the demeshening". You can learn more about that here:

* YTEP-0032: http://ytep.readthedocs.io/en/latest/YTEPs/YTEP-0032.html
* The talk Meagan Lang and I gave at SciPy 2017: https://www.youtube.com/watch?v=pkZgQIGac6I

The code lives in the "sph-viz" branch on my fork of yt: https://github.com/ngoldbaum/yt/tree/sph-viz

I'm going to try to get that branch moved into the main yt repo to make code review easier.

You might also try running the gizmo SPH code (http://www.tapir.caltech.edu/~phopkins/Site/GIZMO.html) just a test problem or two, and then visualize the results using yt (yt-project.org).

# Cython tutorial:

https://github.com/kwmsmith/scipy-2017-cython-tutorial

# Intermediate Python Tutorials:

Building python APIs using the Python data model:

https://www.youtube.com/watch?v=k55d3ZUF3ZQ&t

Building a full-fledged application:

https://www.youtube.com/watch?v=SUt3wT43AeM&t

NumPy, SciPy, matplotlib tutorials:

http://www.scipy-lectures.org/

# Prep problem:

I'd like you write a function `splat` that produces splatted visualization of a particle distribution. This is the simplest way to visualize a particle distribution. The resulting image should be filled with values that are either zero or one: zero if the pixel does not contain any particles and one if the pixel does contain a particle.

The function should take a numpy array of particle positions, the coordinates of the bottom left and top right corner of the image, and the resolution of the image. Here's one way to set things up:

```python
import numpy as np

num_particles = 1000

# px and py contains randomly generated values between 0 and 1
px = np.random.random(num_particles)
py = np.random.random(num_particles)

bottom_left = [0, 0]
top_right = [1, 1]

resolution = (1024, 1024)

image = splat(px, py, left_corner, right_corner, resolution)

# basic tests
assert image.shape == resolution
assert image.sum() <= num_particles

```

Your job is to write the `splat` function. First I'd suggest writing it in pure python. Once you feel like you have a good solution you should try speeding it up using cython. It will be easiest to initially write the `splat` function in a Jupyter notebook. Once you have that working I can help you convert the notebook into a proper python package and handle compiling using a `setup.py` file. Don't worry if you don't know what that means, I will teach you :)

I'd also like you to think about how you might test the `splat` function. Testing is very important for ensuring that code is correct and stays correct even while it gets modified.

# Project deliverables:

Toy python volume renderer. Not expected to be fast but will allow easy prototyping and exploring different algorithms.

Serial CPU ray-tracing volume renderer for SPH datasets written in cython and integrated with yt. Ideally will work well with datasets with millions of particles.

MPI and OpenMP-parallel version able to scale to large particle datasets.

Realtime rendering using OpenGL (e.g. GLFW) or WebGL.

