# nk.py
Refractive indices/dispersion models of many common optical films from the U.C. Santa Barbara Nanofabrication Facility & common alloys, for use in python scripts.
All wavelengths are in MICRONS (µm).

Materials may be called from another script like so:

    import nk
    # Return the refractive index of SiO2 at the given wavelength(s) in Micrometers:
    >>> nk.SiO(1.550)       
    : 1.448333
    
You can pass/return multiple wavelengths/indices. They must in a numpy.array (not [list]), as so:

    >>> nk.SiO(  numpy.array([1.550, 1.551, 1.552])  )       
    : array([ 1.4483336 ,  1.44832036,  1.44830712])

## More examples:
    
    core_material = nk.SiN   # Despite appearances, these are functions, not variables!
    core_material( 1.550 )   # will give index at that wavelength
    
    # Return the refractive index for the Alloy Al(0.92)Ga(0.08)As @ 1.550 micron wavelength:
    >>> nk.AlGaAs(0.92, 1.550)   
    : 2.93059
    
    
Complex Refractive indices, in the form (n + i*k), can be requested from certain materials via the `k=True` argument, as so:

    >>> nk.GaSb( 0.632 , k=True)
    : (4.9285209602676332-0.69616573380335467j)

## Define your own materials:

Materials may be defined in this file like so:

    >>> cauchy = lambda p ,x: p[0] + p[1]/x**2 + p[2]/x**4      
where cauchy is a defined lambda (in-line) fitting function, and p can be passed as a list/tuple of 3 values to set the constants in the equations.
For SiO2 with the Cauchy fitting params of A=1.4764, B=0.0229, C=-0.012346 (for wavelength in microns):

    >>> SiO2 = lambda x: cauchy([ 1.4764 , 0.02299 , -0.012346 ], x)     # note x is still a passed variable.
    >>> SiO2( 1.550 )    # in microns! (as defined by fitting params, above)
    : 1.4764000095691965
    
See the GaAs_interp & GaSb_interp functions for examples of how to interpolate directly from raw tabulated data, which can be found online for various materials at websites like:
- http://www.filmetrics.com/refractive-index-database
- https://refractiveindex.info


# Help
After importing use the following for additional help:
- `help( nk )` to see usage info.
- `dir( nk )` to list defined materials
- `help( nk.Si )` to see info on specific material model


# Authors
Originally written by Dustin Kleckner, U.C. Santa Barbara, 2008
Updated and maintained by Demis D. John.
