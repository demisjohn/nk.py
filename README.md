# nk.py
File containing refractive indices of many common optical films from the U.C. Santa Barbara Nanofabrication Facility, for use in python scripts.

Materials may be called from another script like so:

    import nk
    # Return the refractive index of SiO2 at the given wavelength(s) in Micrometers:
    >>> nk.SiO(1.550)       
    : 1.448333
    
You can pass/return multiple wavelengths/indices. They must in a numpy.array (not [list]), as so:

    >>> nk.SiO(  numpy.array([1.550, 1.551, 1.552])  )       
    : array([ 1.4483336 ,  1.44832036,  1.44830712])
