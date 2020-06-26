# ExoLens
Compositional calculator for rocky planets based on ExoPlex (Unterborn et al. 2018).

ExoLens is based off of the open mass-radius software ExoPlex (See Unterborn et al. 2016, 2018). We fit an analytical expression for core mass fraction (CMF) to CMF vs R curves generated with ExoPlex from 0.01 to 11.0 Earth masses. For these curves, we assume a pure Fe core and Fe-free MgSiO3 mantle.

This function reproduces CMF values calculated by ExoPlex with an RMS of 1.5%, 
significantly smaller than the CMF resolution that is obtainable with the current
planetary mass and radius precisions in this mass range. 
See Schulze et al. 2020 for more details

The main goal of this calculator is to provide the user with a quick way to 
accurately infer interior compositions for a large sample of likely rocky 
planets quickly. An additional goal is to determine how consistent the composition
of a given planet is with what is expected from its host star's [Fe/H], [Si/H],
and [Mg/H] abundances. However, this determination is optional, and the
user is able to determine the parameter space of just the planet.

We have include additional functionality in functions_misc.py.


Required inputs:
(1)	mass: a tuple of measured planetary mass and it's uncertainty -- [M, sigM]
(2)	radius: a tuple of measured planetary radius and it's uncertainty -- [R, sigR]
   
    
Optional inputs:
(1) planet_fname: file name for plot output
(2) sratios: the host star's Fe/Mg and Si/Mg ratios -- [FeMg, sigFeMg,SiMg,sigSiMg]
      If the user only has stellar [Fe/H] there is a function called approx_SiH_MgH in functions_misc.py that will approximate values for [Si/H] and [Mg/H] from the Hypatia Catalogue (Hinkel et al. 2014).
•	There is also a function called calc_FeMg_SiMg in functions_misc.py that takes in [Fe/H], [Si/H], and [Mg/H] which will calculate the Fe/Mg and Si/Mg ratios and their uncertainties.
             
Outputs:
    cmfrho: planetary core mass fraction and uncertainties
•	[CMF, sigCMF upper, sigCMF lower]
    cmfstar: expected core mass fraction from host's Fe/Mg and Si/Mg ratios
•	[CMFstar, sigCMFstar]
•	If no abundances are given to ExoLens this tuple will be filled with NaN.    integral: computes the likelihood that the CMF inferred from mass and radius 
             is consistent with what is expected from the host star.
                  -- if no CMF star is provided, 'NaN' is returned for the integral.
    
    Plots: ExoLens returns the following four plots
                (1) Planetary radius vs CMF
                (2) Planetary mass vs CMF
                (3) Mass vs Radius with a contour of CMF
                (4) PDF's for planetary CMF and CMF star (if CMF star is
                    provided).



***If you only wish to compute the CMF inferred from planetary mass and radius, use the calc_cmfrho function in functions_main. This function only requires the mass and radius of a planet and their uncertainties in the form: Mass = [mass, sigM] and Radius = [radius, sigR]. This function is at the heart of ExoLens.
