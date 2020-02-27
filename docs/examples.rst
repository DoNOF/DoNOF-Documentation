########
Examples
########

Single-point calculation
------------------------

PNOF5 single-point energy calculation of HF molecule with cc-pVDZ basis set starting from HCORE calculation.::

    &INPRUN RUNTYP=ENERGY MULT=1 ICHARG=0 /
    $DATA
    HF-Singlet: CCD, Exp. Geom. ( 0.90148 at HF/CCD level )
    H 1.0 0.00 0.00 0.0000
    S 3
     1 13.0100000 0.0196850
     2 1.9620000 0.1379770
     3 0.4446000 0.4781480
    S 1
     1 0.1220000 1.0000000
    P 1
     1 0.7270000 1.0000000

    F 9.0 0.00 0.00 0.9168
    S 8
     1 14710.0000000 0.0007210
     2 2207.0000000 0.0055530
     3 502.8000000 0.0282670
     4 142.6000000 0.1064440
     5 46.4700000 0.2868140
     6 16.7000000 0.4486410
     7 6.3560000 0.2647610
     8 1.3160000 0.0153330
    S 8
     1 14710.0000000 -0.0001650
     2 2207.0000000 -0.0013080
     3 502.8000000 -0.0064950
     4 142.6000000 -0.0266910
     5 46.4700000 -0.0736900
     6 16.7000000 -0.1707760
     7 6.3560000 -0.1123270
     8 1.3160000 0.5628140
    S 1
     1 0.3897000 1.0000000
    P 3
     1 22.6700000 0.0448780
     2 4.9770000 0.2357180
     3 1.3470000 0.5085210
    P 1
     1 0.3471000 1.0000000
    D 1
     1 1.6400000 1.0000000

    $END
    &NOFINP /


PNOF7 single-point energy calculation optimizing only with respect to natural occupation numbers of HF molecule with cc-pVDZ basis set starting from Hartree-Fock calculation, without writting integrals at disk.::

    &INPRUN RUNTYP=ENERGY MULT=1 ICHARG=0 DONTW=T /
    $DATA
    HF-Singlet: CCD, Exp. Geom. ( 0.90148 at HF/CCD level )
    H 1.0 0.00 0.00 0.0000
    S 3
     1 13.0100000 0.0196850
     2 1.9620000 0.1379770
     3 0.4446000 0.4781480
    S 1
     1 0.1220000 1.0000000
    P 1
     1 0.7270000 1.0000000

    F 9.0 0.00 0.00 0.9168
    S 8
     1 14710.0000000 0.0007210
     2 2207.0000000 0.0055530
     3 502.8000000 0.0282670
     4 142.6000000 0.1064440
     5 46.4700000 0.2868140
     6 16.7000000 0.4486410
     7 6.3560000 0.2647610
     8 1.3160000 0.0153330
    S 8
     1 14710.0000000 -0.0001650
     2 2207.0000000 -0.0013080
     3 502.8000000 -0.0064950
     4 142.6000000 -0.0266910
     5 46.4700000 -0.0736900
     6 16.7000000 -0.1707760
     7 6.3560000 -0.1123270
     8 1.3160000 0.5628140
    S 1
     1 0.3897000 1.0000000
    P 3
     1 22.6700000 0.0448780
     2 4.9770000 0.2357180
     3 1.3470000 0.5085210
    P 1
     1 0.3471000 1.0000000
    D 1
     1 1.6400000 1.0000000

    $END
    &NOFINP IPNOF=7 ICOEF=0 HFID=T /

    
PNOF7 for multiplets single-point energy calculation optimizing only with respect to natural orbitals of Oxygen atom at its spin state S=1 with STO-3G basis set.::


    &INPRUN RUNTYP=ENERGY MULT=3 ICHARG=0 /
    $DATA
    O-Triplet: STO-3G
    O 8.0 0.00 0.00 0.0000
    S   3
      1         0.1307093214E+03       0.1543289673E+00
      2         0.2380886605E+02       0.5353281423E+00
      3         0.6443608313E+01       0.4446345422E+00
    L   3
      1         0.5033151319E+01      -0.9996722919E-01       0.1559162750E+00
      2         0.1169596125E+01       0.3995128261E+00       0.6076837186E+00
      3         0.3803889600E+00       0.7001154689E+00       0.3919573931E+00
    
    $END
    &NOFINP IPNOF=7 ICOEF=2 /
    
    
Perturbative correction
-----------------------

NOF-MP2 single-point energy calculation of Oxygen atom at its spin state S=0 with STO-3G basis set.::

    &INPRUN RUNTYP=ENERGY MULT=1 ICHARG=0 /
    $DATA
    O-Singlet: STO-3G
    O 8.0 0.00 0.00 0.0000
    S   3
      1         0.1307093214E+03       0.1543289673E+00
      2         0.2380886605E+02       0.5353281423E+00
      3         0.6443608313E+01       0.4446345422E+00
    L   3
      1         0.5033151319E+01      -0.9996722919E-01       0.1559162750E+00
      2         0.1169596125E+01       0.3995128261E+00       0.6076837186E+00
      3         0.3803889600E+00       0.7001154689E+00       0.3919573931E+00
    
    $END
    &NOFINP IPNOF=7 Ista=1 CLMP2=T /


Geometry Optimization
---------------------
    
Geometry Optimization of HF molecule by using cc-pVDZ basis set and conjugate gradient algorithm.::

    &INPRUN RUNTYP=OPTGEO MULT=1 ICHARG=0 DONTW=T /
    $DATA
    HF-Singlet: CCD, starting from Exp. Geom. ( 0.90148 at HF/CCD level )
    H 1.0 0.00 0.00 0.0000
    S 3
     1 13.0100000 0.0196850
     2 1.9620000 0.1379770
     3 0.4446000 0.4781480
    S 1
     1 0.1220000 1.0000000
    P 1
     1 0.7270000 1.0000000

    F 9.0 0.00 0.00 0.9168
    S 8
     1 14710.0000000 0.0007210
     2 2207.0000000 0.0055530
     3 502.8000000 0.0282670
     4 142.6000000 0.1064440
     5 46.4700000 0.2868140
     6 16.7000000 0.4486410
     7 6.3560000 0.2647610
     8 1.3160000 0.0153330
    S 8
     1 14710.0000000 -0.0001650
     2 2207.0000000 -0.0013080
     3 502.8000000 -0.0064950
     4 142.6000000 -0.0266910
     5 46.4700000 -0.0736900
     6 16.7000000 -0.1707760
     7 6.3560000 -0.1123270
     8 1.3160000 0.5628140
    S 1
     1 0.3897000 1.0000000
    P 3
     1 22.6700000 0.0448780
     2 4.9770000 0.2357180
     3 1.3470000 0.5085210
    P 1
     1 0.3471000 1.0000000
    D 1
     1 1.6400000 1.0000000

    $END
    &NOFINP USENAG=T RESTART=T /


Convergence
-----------
    
PNOF5 single-point energy + Gradient calculation of Oxygen atom by using STO-3G basis set and convergence criteria of NTHRESHE=10**(-5) for total energy after both occupation and orbital optimization, NTHRESHEC=10**(-12) for energy after occupation optimization, and NTHRESHEN=10**(-16) for energy after orbital optimization. More importantly, set overall convergence of symmetry of matrix Fij as NTHRESHL=4 (usually that is enough, but NTHRESHL=5 is recommended for more accuracy).::

    &INPRUN RUNTYP=GRAD MULT=1 ICHARG=0 /
    $DATA
    O-Singlet: STO-3G
    O 8.0 0.00 0.00 0.0000
    S   3
      1         0.1307093214E+03       0.1543289673E+00
      2         0.2380886605E+02       0.5353281423E+00
      3         0.6443608313E+01       0.4446345422E+00
    L   3
      1         0.5033151319E+01      -0.9996722919E-01       0.1559162750E+00
      2         0.1169596125E+01       0.3995128261E+00       0.6076837186E+00
      3         0.3803889600E+00       0.7001154689E+00       0.3919573931E+00
    
    $END
    &NOFINP NTHRESHE=5 NTHRESHEC=12 NTHRESHEN=16 NTHRESHL=4 /


