# Tracking Molecular Clouds

## Background Information

Giant molecular clouds (GMCs) are the primary sites of star formation in star-forming disk galaxies like the present-day milky way. A typical GMC has a mass anywhere from 10^4 to a few times 10^6 solar masses, and consists primarily of molecular hydrogen. On the scale of a whole cloud, the gas is roughly in equilibrium with "pressure" provided by the supersonic turbulent motion of the gas in the cloud. In overdense regions of the cloud, the cloud is self-gravitating and star formation can proceed.

Sometimes massive stars form. These stars will produce both ionizing radiation, which can evaporate the cloud, producing structures like the Orion nebula or the Eagle nebula, and supernova explosions within a few million years, which can disrupt and unbind the cloud.

There is a wide breadth of literature on giant molecular clouds. I'd suggest the following review articles to start with:

* "Molecular Clouds in Nearby Galaxies" https://doi.org/10.1146/annurev-astro-081309-130854

   A review of observations of GMCs in nearby galaxies

* "Molecular Clouds in the Milky Way https://doi.org/10.1146/annurev-astro-082214-122324

   A review of observations of GMCs in our Galaxy.

* https://doi.org/10.2458/azu_uapress_9780816531240-ch001

   Theoretical background on the formation of GMCs and a galaxy-scale view of the star formation process.

## Project Details

The basis for this project is a set of three galaxy evolution simulations I ran for my thesis project. The data are archived at the yt hub:

https://girder.hub.yt/#collection/573647d3dd9119000164acf0

See the description for the archived dataset for more information about downloading and working with the data.

There are two papers describing these simulations:

https://doi.org/10.1088/0004-637X/814/2/131
https://doi.org/10.3847/0004-637X/827/1/28

The first describes the basic setup for the simulation as well as an earlier set of simulations that did not include the effect of supernova blastwaves on the gas in the galaxy simulation. The second describes the data we will be working with for this project. These simulations included a prescription for supernova blastwave feedback which produces galaxies that more closely resemble observed nearby disk galaxies.

You will be using the yt clump finder (see http://yt-project.org/doc/analyzing/analysis_modules/clump_finding.html) to create catalogues of gravitationally bound clumps in these galaxy simulations. Once we figure out how to identify the clumps in a single snapshot, we will parallelize the work and being to build catalogues of clumps as a function of time.

This will allow us to track clumps through the simulation and calculate interesting quantities like the merger and collision rate, merger trees, orbits and mass accretion rates.

You can track the molecular clouds in this simulation yourself. Just watch these movies of the simulation in a frame-by-frame fashion:

https://www.youtube.com/watch?v=t5RpOu1SEyA

http://www.watchframebyframe.com/watch/yt/t5RpOu1SEyA

## Project Deliverables

* A molecular cloud catalog for a single snapshot. This will be produced by a python-based analysis script that can be turned into a piece of a parallel analysis pipeline. The catalog should include entries for cloud properties like:

    * Mass
    * Velocity Vector
    * Position
    * A 3D model for the cloud boundary?

* Molecular cloud catalogues for the full simulation dataset.

* Identify algorithms to track clouds through time.

* Derive cloud histories from catalog.

* Draft and submit publication describing the results.
