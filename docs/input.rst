#############
Input Options
#############

This page summarizes current DoNOF input namelists. For full local reference, see:

- ``doc/namelist.md`` in https://github.com/DoNOF/DoNOFsw

Overview
********

DoNOF inputs are centered on:

- ``&INPRUN``: run type, integral options, electric field, and global controls
- ``&NOFINP``: NOF/optimization settings and post-NOF options
- ``&INPDYN``: molecular dynamics parameters (required when ``RUNTYP='DYN'``)

Typical jobs use ``&INPRUN``, ``$DATA``, and ``&NOFINP``.

********
&INPRUN
********

Main options
^^^^^^^^^^^^

- ``RUNTYP``

  - ``'ENERGY'``: single-point energy
  - ``'GRAD'``: analytic gradient
  - ``'OPTGEO'``: geometry optimization
  - ``'HESS'``: numerical Hessian from analytic gradients
  - ``'TSOPT'``: transition-state optimization
  - ``'DYN'``: Born-Oppenheimer molecular dynamics

- ``MULT``: spin multiplicity
- ``ICHARG``: molecular charge
- ``IECP``: ECP control
- ``IEMOM``: electrostatic moments (dipole/quadrupole/octopole)

Integral and basis controls
^^^^^^^^^^^^^^^^^^^^^^^^^^^

- ``USELIB``

  - ``.TRUE.``: LIBCINT
  - ``.FALSE.``: HONDO

- ``GTYP``: ``SPH`` or ``CART``
- ``ERITYP``: ``FULL``, ``RI``, or ``MIX``
- ``RITYP``: ``JKFIT``, ``GEN``, or ``RIFIT``
- ``GEN``: generative auxiliary basis (e.g. ``A2*``)
- ``CUTOFF``: Schwarz screening threshold
- ``SMCD``: symmetric modified Cholesky decomposition

Electric field and NLOP
^^^^^^^^^^^^^^^^^^^^^^^

- ``EVEC``: external electric-field vector (a.u.)
- ``NLOP``

  - ``-1``: alpha, beta, gamma
  - ``0``: disabled
  - ``1``: alpha
  - ``2``: beta
  - ``3``: gamma

- ``NPOINT``: field points for dyadic Romberg-Richardson procedure
- ``STEP``: base field step
- ``ISOALPHA``: isotropic/anisotropic polarizability analysis

********
&NOFINP
********

Core controls
^^^^^^^^^^^^^

- ``IPNOF``

  - ``5``: PNOF5
  - ``6``: PNOF6
  - ``7``: PNOF7
  - ``8``: GNOF

- ``Ista``: PNOF7 variant selector
- ``Imod`` (for ``IPNOF=8``)

  - ``0``: GNOF
  - ``1``: GNOFm

- ``ICOEF``: occupation/orbital optimization mode
- ``ISOFTMAX``: occupation parametrization
- ``IORBOPT``: orbital optimizer (ID/ADAM/AdaBelief/YOGI/DEMON/SQP)
- ``MAXIT``: max OCC-SCF iterations
- ``NO1``: fully occupied orbital policy

Hartree-Fock and convergence
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

- ``IRHF``: RHF pre-optimization mode
- ``NCONVRHF`` / ``MAXITRHF``: RHF convergence controls
- ``NTHRESHL``, ``NTHRESHE``, ``NTHRESHEC``, ``NTHRESHEN``: convergence thresholds

Post-NOF and extra features
^^^^^^^^^^^^^^^^^^^^^^^^^^^

- ``ERPA``: excited-state ERPA analysis
- ``MBPT`` / ``MBPT2`` / ``MBPT3``: NOF-based perturbative corrections
- ``MOLDEN`` / ``MOLDENGEO`` / ``MOLPRO`` / ``FCHK``: output controls

********
&INPDYN
********

Used only for ``RUNTYP='DYN'``.

Typical fields:

- ``dt``: time step
- ``tmax``: total simulation time
- ``Vxyz``: initial velocity components
- ``IRESTART``: restart control

Dynamics jobs require a valid ``GCF`` file to initialize occupations and orbitals.

************
Basic example
************

::

    &INPRUN RUNTYP='ENERGY' MULT=1 ICHARG=0 /
    $DATA
    Water
    aug-cc-pVDZ
    O 8.0  0.000000  0.000000  0.000000
    H 1.0  0.000000  0.757000  0.587000
    H 1.0  0.000000 -0.757000  0.587000
    $END
    &NOFINP IPNOF=8 /
