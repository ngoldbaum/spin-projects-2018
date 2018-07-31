My code for the KDRayTracer can be found in this repository:
https://github.com/bqia0/KDRayTracer

The current code can be tested with:

```
def test():
    resolution = np.array([256, 256], dtype='uint64')
    ones = np.ones(int(1e6))
    positions = np.random.random((int(1e6), 3))
    bounds = [0, 1, 0, 1, 0, 1]
    px = positions[:, 0]
    py = positions[:, 1]
    pz = positions[:, 2]
    buf = KDRayTrace.kdtreeRayTrace(positions,
                                    ones,
                                    ones,
                                    ones,
                                    ones,
                                    left_edge,
                                    right_edge,
                                    bounds,
                                    resolution)
    plt.imsave('KDRayTrace.png', np.log10(buf))
```

The ones passed to the function are purely for testing purposes. These quantities are smoothing length, density, mass,
and smoothing quantity in that order.

The function works by iterating over every pixel. The number of pixels is given by `resolution`. For every pixel, the code 
parametrically defines a line that runs through the center of the pixel, andstarts some small distance away from the simulation domain.
The point of intersection between the line and simulation domain is found, and the leaf node for this point is then found. Then, the 
exit point of the line in the current leaf node is found, and the next leaf node the line enters is found. This is repeated until the
line leaves the simulation domain. For each leaf node, intersection checks between particles and the line are performed. If the line
intersects with a particle, SPH interpolation is performed on that particle for that pixel only. Since yt does not have an SPH
interpolation function that works on one particle and one pixel, I wrote one in my fork of yt:
https://github.com/bqia0/yt/blob/3f7f33c433c929b65b7f074c9201531b8b883481/yt/utilities/lib/pixelization_routines.pyx#L1057

Since the current version only accounts for particles who are centered in the current leaf node, particles centered 
elsewhere but whose smoothing regions overlap with the current leaf node are not accounted for. I believe this is 
what contributes to the blocky nature of the projections created by my code. I had the program check the immediate 
neighbors of the current leaf node as well, and the problem became a bit less apparent. However, I have not definitively 
proved this is the problem, so tests will have to be written to determine this. If this is in fact the problem, a more advanced
KD-Tree traversal will have to be written.

As part of testing, one could compare projections created by this code to projections created by the yt SPH pixelization routines. 
They should both produce the same result.
