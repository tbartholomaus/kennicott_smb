# Kennicott Glacier: mass-balance profiles for zero net balance

`kennicott_mass_balance.ipynb` asks a simple question with a real-world
answer: given the actual shape of Kennicott and Root Glaciers (Wrangell-St.
Elias, Alaska), what surface mass-balance-vs-elevation profile would leave
the glacier system with zero net (glacier-wide) mass balance? The notebook
is fully self-contained -- it downloads the RGI outlines for Kennicott
(RGI60-01.15645) and its tributary Root Glacier (RGI60-01.26722), merges
them, auto-downloads and mosaics the Copernicus GLO-30 DEM tiles covering
the combined ice extent, and builds the resulting hypsometry (area per
elevation band) entirely from public, no-authentication data sources.

That hypsometry is combined with a piecewise-linear surface mass balance
parameterization in the same form as PISM's `elevation_dependent` surface
mass balance
model. The ablation-zone shape and the equilibrium-line altitude are
anchored to field observations from Petersen et al. (2025); the potential for a
high-elevation accumulation plateau is not locally constrained, so the
notebook also reviews the peer-reviewed literature (chiefly Mt. Logan) on
where such plateaus tend to occur elsewhere in the region. Starting from
the reference profile interpretted from Petersen et al., 2025 -- which 
does *not* zero out the glacier-wide net balance as
specified -- the notebook solves for two independent ways to modify the 
surface mass balance parameters and arrive at zero mass balance. These are
sliding the accumulation cap up or down along its existing gradient, or
shifting the entire balance profile by a constant offset. 
The code then maps out the full
continuum of combinations of those two adjustments that produce a 
Kennicott-Root Glacier system in balance.

The end product is a pair of ready-to-use PISM `elevation_dependent` config
blocks -- one for each method -- that can be copied directly into a PISM run
to simulate this glacier system at steady state. All intermediate outputs
(DEM tiles, RGI shapefiles, clipped rasters) are cached locally and are
reproducible by simply re-running the notebook.
