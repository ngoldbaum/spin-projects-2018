# SPH Volume Rendering

Make it possible to volume render SPH data in yt.

Background on SPH formalism and visualization:

* The paper describing the SPLASH visualization software (http://users.monash.edu.au/~dprice/splash/): https://doi.org/10.1071/AS07022
* "Smoothed Particle Hydrodynamics and Magnetohydroynamics" by Dan Price: https://arxiv.org/abs/1012.1885 (in particular Sections 1, 2, and 4)
* Review: Kd-tree Traversal Algorithms for Ray Tracing. See http://onlinelibrary.wiley.com/doi/10.1111/j.1467-8659.2010.01844.x/pdf
* cykdtree, the cython KDTree library by Meagan Lang we've been using for this project: https://github.com/cykdtree/cykdtree
* Splotch: visualizing cosmological simulations. See http://iopscience.iop.org/article/10.1088/1367-2630/10/12/125006/meta

This work will be happening in a yt branch we call "the demeshening". You can learn more about that here:

* YTEP-0032: http://ytep.readthedocs.io/en/latest/YTEPs/YTEP-0032.html
* The talk Meagan Lang and I gave at SciPy 2017: https://www.youtube.com/watch?v=pkZgQIGac6I

The code lives in the "sph-viz" branch on my fork of yt: https://github.com/ngoldbaum/yt/tree/sph-viz

I'm going to try to get that branch moved into the main yt repo to make code review easier.

Project deliverables:

Toy python volume renderer. Not expected to be fast but will allow easy prototyping and exploring different algorithms.

Serial CPU ray-tracing volume renderer for SPH datasets written in cython and integrated with yt. Ideally will work well with datasets with millions of particles.

MPI and OpenMP-parallel version able to scale to large particle datasets.

Realtime rendering using OpenGL (e.g. GLFW) or WebGL.

