Input Options
=============

*******
&INPRUN
*******

The &INPRUN namelist specifies the run type, the atomic basis, and similar fundamental job options. These options are controlled by the following keywords:

RUNTYP:    specifies the run calculation

    = ENERGY  1) single-point energy calculation (Default)

    = GRAD   2) energy + gradients with respect to nuclear coord.

    = OPTGEO 3) optimize the molecular geometry
    
MULT:      Multiplicity of the electronic state

    = 1      singlet (Default)

    = 2,3,...doublet, triplet, and so on

ICHARG:    Molecular charge

    = 0  Neutral Molecule (Default)

IEMOM:     Electrostatic moments calculation

    = 0      skip calculation

    = 1      calculate monopole and dipole (Default)

    = 2      also calculate quadrupole moments

    = 3      also calculate octopole moments

UNITS:     Distance units (Any angles must be in degrees)

    = ANGS   Angstroms (Default)

    = BOHR   Bohr atomic units

EVEC:      An array of the three x,y,z components of the applied electric field, in a.u. (1 a.u. = 1 Hartree/e*bohr = 5.1422082(15)d+11 V/m)

    = ZERO   (Default)

DONTW:     Do not write 2e- integrals on the disk (Unit=1)

    = F      (Default)
    
    = T

*******
&NOFINP
*******

The &NOFINP namelist specifies the type of PNOF calculation, options
for the iterative diagonalization method, perturbative corrections,
input and output, and similar fundamental job options. These options
are controlled by the following keywords:

NUMBER OF TOTAL ITERATIONS
^^^^^^^^^^^^^^^^^^^^^^^^^^

MAXIT:               Maximum number of OCC-SCF iterations 

    = 1000   (DEFAULT)


TYPE OF CALCULATION
^^^^^^^^^^^^^^^^^^^

ICOEF:               Coefficient Optimization

                      = 0      Optimize Energy only by the occupations
                      
                      = 1      use the ID (SCF) method (DEFAULT)
                      
                      = 2      Optimize Energy only by the orbitals
                      
                      = 3      Optimize Energy by all occupations and only core-fragment orbitals, the rest of fragment orbitals remain frozen
                      
                      = 4      use a HF-like Fockian

IEINI:               Calculate only the initial energy

                      = 0      (DEFAULT)

NO1:                 MAX. index of NOs with Occupation equal to 1.0

                      = -1     Consider Core NOs (DEFAULT)
                      
                      = 0      All NOs are considered
                      
                      = Value  User specifies how many NOs have OCC equal to 1.0


HARTREE-FOCK
^^^^^^^^^^^^

HFID:               Use the Iterative Diagonalization Method to generate the HF Orbitals

                      = F      HF MO (DEFAULT)
                      
                      = T      HF MO are obtained using the ID (HFIDr)


PNOF SELECTION
^^^^^^^^^^^^^^

IPNOF:               Type of Natural Orbital Functional (see section "NOF approximations")

                      = 5      PNOF5
                      
                      = 6      PNOF6
                      
                      = 7      PNOF5 + Inter-pair (DEFAULT)

NCWO:                Number of coupled weakly occupied MOs per strongly occupied = Nc -> PNOFi(Nc)

                      = 1      NCWO = 1 (DEFAULT)
                      
                      = 2,3,...
                      
                      =-1      NCWO = NVIR/NDOC
                               NVIR: Number of HF virtual  MOs (OCC=0)
                               NDOC: Number of strongly occupied MOs

Ista:                Use Static version of PNOF7

                      = 0      PNOF7 ((DEFAULT)
                      
                      = 1      PNOF7s
                      

CONVERGENCE CRITERIA IN NOF CALCULATION
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Fore more info see section X in [CPC ...]

NTHRESHL:            CONVERGENCE OF THE LAGRANGE MULTIPLIERS THRESHL=10.0**(-NTHRESHL)

                      = 4      (DEFAULT)

NTHRESHE:            CONVERGENCE OF THE TOTAL ENERGY THRESHE=10.0**(-NTHRESHE)

                      = 6      (DEFAULT)

NTHRESHEC:           CONVERGENCE OF THE TOTAL ENERGY (ORBOPT) THRESHEC=10.0**(-NTHRESHEC)

                      = 12     (DEFAULT)

NTHRESHEN:           CONVERGENCE OF THE TOTAL ENERGY (OCCOPT) THRESHEN=10.0**(-NTHRESHEN)

                      = 16     (DEFAULT)


OPTIONS FOR THE OCCUPATION (GAMMA) OPTIMIZATION PROGRAM
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

USENAG:              Use NAG Library Routine: DUMCGG

                      = T      (DEFAULT)
                      
                      = F      use instead a LBFGS method (see note in "Additional notes" section)


OPTIONS FOR THE ORBITAL OPTIMIZATION PROGRAM (ID METHOD)
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

For more info see [JCC 30, 2078 (2009)]
For computational details see section X in [1]

NOPTORB:             Number of the optimized orbitals

                      = NBF    (DEFAULT)

MAXLOOP:             Maximum Iteration Number for the SCF ITERATION cycle in each ITCALLs

                      = 30     (DEFAULT)

    The straightforward iterative scheme fails to converge very often due to the values of some off-diagonal elements Fki. The latters must be suffciently small and of the same order of magnitude. A variable factor scales Fki. We establish an upper bound B, in such a way that when the absolute value of the matrix element Fki is greater than B, it is scaled by a factor Cki (F'ki = Cki*Fki ), as to satisfy ABS(Fki) <= B.

SCALING:             A variable factor scales Fki

                      = T      (DEFAULT)

NZEROS:              B = 10.0**(1-NZEROS). Initial number of ZEROS in Fij. The scaling factor varies until the number of ZEROS (.000##) is equal for all elements Fij

                      = 0      B = 10.0 (DEFAULT)

NZEROSm:             B = 10.0**(1-NZEROSm) Maximum number of zeros in Fij

                      = 4      B = 10.0 (DEFAULT)

NZEROSr:             B = 10.0**(1-NZEROSr) Number of zeros in Fij to restart automatically the calculation

                      = 0      B = 10.0 (DEFAULT)

ITZITER:             Number of Iterations for constant scaling

                      = 10     (DEFAULT)

DIIS:                Direct Inversion in the Iterative Subspace in the orbital optimization if DUMEL < THDIIS every NDIIS loops

                      = T      (DEFAULT)

NTHDIIS:             Energy threshold to begin DIIS

                      = 3      THDIIS = 10.0**(-NTHDIIS) (DEFAULT)

NDIIS:               Number of considered loops to interpolate the generalized Fock matrix in the DIIS

                      = 5      (DEFAULT)

PERDIIS:             Periodic DIIS

                      = T      Apply DIIS every NDIIS (DEFAULT)
                      
                      = F      DIIS is always applied after NDIIS


OPTIONS FOR PERTURBATIVE CALCULATIONS
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

For more info see [PRA 98, 022504 (2018)]

CLMP2:               Correlated local MP2 = NOF - oiMP2

                     = F       (DEFAULT)

SC2MCPT:             SC2-MCPT perturbation theory is used to correct the PNOF5 Energy. 2 outputs: PNOF5-SC2-MCPT and PNOF5-PT2

                     = F       (DEFAULT)

NO1PT2:              Frozen MOs in perturbative calculations. Maximum index of NOs with Occupation = 1

                      = -1     = NO1 (DEFAULT)
                      
                      = 0      All NOs are considered
                      
                      = Value  User specifies how many NOs are frozen

NEX:                 Number of excluded coupled orbitals in the PNOF5-PT2 calculation

                      = 0      All NOs are included (DEFAULT)


RESTART OPTIONS FOR GAMMA, C, Diagonal F, and NUCLEAR COORDINATES
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

RESTART:             RESTART FROM GCF FILE (DEFAULT=F)

                      = F      INPUTGAMMA=0,INPUTC=0,INPUTFMIUG=0
                      
                      = T      INPUTGAMMA=1,INPUTC=1,INPUTFMIUG=1

INPUTGAMMA:          GUESS FOR GAMMA MATRIX IN NOF

                      = 0      NO INPUT (DEFAULT)
                      
                      = 1      INPUT FROM FILE GCF

INPUTC:              GUESS FOR COEFFICIENT MATRIX IN NOF

                      = 0      NO INPUT, USE HF (DEFAULT)
                      
                      = 1      INPUT FROM FILE GCF

INPUTFMIUG:          GUESS FOR DIAGONAL ELEMENTS (FMIUG0)

                      = 0      NO INPUT (DEFAULT)
                      
                      = 1      INPUT FROM FILE GCF

INPUTCXYZ:           READ NUCLEAR COORDINATES (Cxyz)

                      = 0      INPUT FROM FILE INP
                      
                      = 1      INPUT FROM FILE GCF


OUTPUT OPTIONS
^^^^^^^^^^^^^^

NPRINT:              OUTPUT OPTION (DEFAULT VALUE: 0)

                      = 0      Short Printing
                      
                      = 1      Output at initial and final iterations including Ei,Coef,Pop,Occ,Emom
                      
                      = 2      Output at each iteration

IWRITEC:             OUTPUT OPTION FOR THE COEFFICIENT MATRIX

                      = 0      NO OUTPUT (DEFAULT)
                      
                      = 1      OUTPUT THE COEFFICIENT MATRIX 

IWRITEE:             Output option for one-particle energies

                      = 0      No Output (Default)
                      
                      = 1      Output EiHF, Elag

IMULPOP:             MULLIKEN POPULATION ANALYSIS

                      = 0      DO NOT DO (DEFAULT)
                      
                      = 1      DO A MULLIKEN POP. ANALYSIS 

APSG:                OPEN AN APSG FILE FOR OUTPUT THE COEFFICIENT MATRIX ($VEC-$END) AND THE EXPANSION COEFFICIENTS OF THE APSG GENERATING WAVEFUNCTION.


                      = F      OUTPUT (DEFAULT)

NTHAPSG:             THRESHOLD FOR APSG EXPANSION COEFFICIENTS THAPSG = 10.0**(-NTHAPSG)

                      = 10     (DEFAULT)

PRINTLAG:            OUTPUT OPTION FOR THE LAGRANGE MULTIPLIERS

                      = F      NO OUTPUT (DEFAULT)

DIAGLAG:             DIAGONALIZE LAGRANGE MULTIPLIERS PRINT CANONICAL VECTORS and PRINT NEW DIAGONAL ELEMENTS OF 1-RDM

                      = F      (DEFAULT)

IAIMPAC:             WRITE INFORMATION INTO A WFN FILE (UNIT 7) FOR THE AIMPAC PROGRAM

                      = 0      DO NOT DO
                      
                      = 1      WRITE INTO WFN FILE (DEFAULT)

IEKT:                Use the EKT (DEFAULT VALUE = 0)

                      = 1      Calculate ionization potentials 

ICATION:             (DEFAULT VALUE = 0)

                      = 1      Calculate the Cation Energy (Eelec+EN+IonPotential)

ICHEMPOT:            (DEFAULT VALUE = 0)

                      = 1      Calculate the Chemical Potential

NOUTRDM:             PRINT OPTION FOR ATOMIC RDMs

                      = 0      NO OUTPUT (DEFAULT)
                      
                      = 1      PRINT ATOMIC RDMs IN 1RDM and 2RDM FILES

NTHRESHDM:           THRESHDM=10.0**(-NTHRESHDM)

                      = 6      (DEFAULT)

NSQT:                Use an unformatted 2RDM file.

                      = 1      (DEFAULT)

NOUTCJK:             PRINT OPTION FOR CJ12 and CK12

                      = 0      NO OUTPUT (DEFAULT)
                      
                      = 1      PRINT CJ12 and CK12 in FILE 'CJK'

NTHRESHCJK:          THRESHCJK=10.0**(-NTHRESHCJK)

                      = 6      (DEFAULT)

NOUTTijab:           PRINT OPTION FOR Tijab

                      = 0      NO OUTPUT (DEFAULT)
                      
                      = 1      PRINT Tijab in FILE 'Tijab'

NTHRESHTijab:        THRESHTijab=10.0**(-NTHRESHTijab)

                      = 6      (DEFAULT)

IGVB:                GVB orbitals connection to PNOFi(1) NOS

                      = 0      (DEFAULT)
       

OPTIONS RELATED TO ORTHONORMALITY OF NATURAL ORBITALS
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

ORTHO:               Orthogonalize the initial orbitals

                      = F      No 
                      
                      = T      Yes (DEFAULT)

CHKORTHO:            CHECK THE ORTHONORMALITY OF THE MOs

                      = F      No (DEFAULT)
                      
                      = T      Yes


OPTIONS RELATED TO FROZEN COORDINATES IN GRADIENT COMPUTATION
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

FROZEN:              Is there any fixed coordinate

                      = F      (DEFAULT)

IFROZEN:             By pairs, what coordinate of which atom, e.g. 2,5,1,1 means "y" coordinate of atom 5 and "x" coor of atom 1 to freeze. MAXIMUM of frozen coordinates = 10

                      = 0      (DEFAULT)


****************
Additional Notes
****************


Dependencies
^^^^^^^^^^^^

You may notice above that setting USENAG=T in the input file DoNOF will use the conjugate gradient algorithm for the optimization of natural occupancies, as well as nuclear coordinates (if RUNTYP=OPTGEO). However, since the license of NAG is restricted (see https://www.nag.co.uk/content/nag-library), these routines are not provided by DoNOF and the user must include them to the code.

Alternatively, we have implemented the LBFGS algorithm written by J. Nocedal (see http://users.iems.northwestern.edu/~nocedal/lbfgs.html, and cite references therein if USENAG=F) for the occupation and geometry optimizations. This method is activated by setting USENAG=F). In our experience, LBFGS works fine for occupation optimization, whereas it must be employed carefully for geometry optimization as detailed below.

New algorithms and numerical methods for carrying out these optimizations are welcome, so we encourage new collaborations to work on this task.


Geometry Optimization
^^^^^^^^^^^^^^^^^^^^^

Related with the previous section, for geometry optimization (RUNTYP=OPTGEO) it is strongly recommended to set USENAG=T and thereby use the conjugate gradient algorithm to find the equilibrium geometry. In fact, the latter has proven to be much more accurate than LBFGS for this task. The LBFGS algorithm has been employed before in quantum chemistry programs to optimize the geometry (see http://openmopac.net/Manual/lbfgs.html). Since LBFGS employs very low memory it is recommended if a large number of variables is to be optimized. Nevertheless, LBFGS may not work accurately if low-energy interactions are significant in our system.

Only information about the initial and final points is printed in the output file ("name-of-the-molecule.out") in geometry optimization calculations (RUNTYP=OPTGEO). For more printing in this file ($NOFINP namelist section) set NPRINT=2 in the input file before runing DoNOF.

GCF: All information required to restart any calculation is printed in a file called GCF during the iterative procedure. At the end of the calculation this file is renamed to "name-of-the-molecule.gcf". It is worth noting that at the end of the GCF the nuclear coordinates are printed. The latter are read at the beginning of the calculation (so the ones from the .inp file are ignored) only if explicitly required by the user, by setting INPUTCXYZ=1 in $NOFINP. This option is particularly useful if the calculation stops unexpectedly during the geometry optimization procedure (RUNTYP=OPTGEO). If that is the case, run a new calculation setting RUNTYP=ENERGY, RESTART=F, and INPUTCXYZ=1 to converge the energy at the last geometry obtained during the geometry optimization. Then you can just set regular geometry optimization calculation, i.e. RUNTYP=OPTGEO, RESTART=T, and INPUTCXYZ=0. In this vein, the GCFe file (that contains the minimal energy obtained during each single-point calculation) can be ignored for RUNTYP=OPTGEO.

Regarding number of initial zeroes at Fij matrix, NZEROSr, it is convenient to set NZEROSr=0 if RUNTYP=OPTGEO. In fact, the solution can change significantly after a displacement of nuclei, then we must let free the ID procedure. On the contrary, whenever we restart a calculation that is almost converged, we can save some extra iterations by setting some initial value for NZEROSr, e.g. NZEROSr=2 or NZEROSr=3 depending on the system and how close from the solution is out starting point (in the GCF file).

In geometry optimization calculations (RUNTYP=OPTGEO), you will note that a file named CGGRAD is created during the calculation. Once the calculation ends it is renamed to "name-of-the-molecule.cgo". This file contains information about the geometry optimization procedure carried out by using the conjugate gradient or LBFGS method (set in the input file by USENAG=T or USENAG=F, respectively), as well as the Hessian and harmonic vibrational frequencies at the solution point. Recall that the Hessian is computed by numerical differentiation of the analytic energy gradients (see details at I. Mitxelena et al. Adv Quant. Chem. ISSN 0065-3276 (2019)), so numerical precision of reported harmonic vibrational frequencies is limited and, apriori, they should be taken only qualitatively.


Dissociation
^^^^^^^^^^^^

Molecular dissociation is considered the main still unresolved problem of DFT, but of fundamental interest for quantum chemistry. PNOF methods are able to reproduce benchmark potential energy curves of molecular bond dissociation. Nevertheless, this calculation is tricky and must be carried out carefully. In fact, different solutions may arise during the dissociation process depending on the electron correlation present in our system. Computationaly it is convenient to converge a single-point calculation to NTHRESHL=5, and then start the dissociation process manually by setting: RESTART=F, ORTHO=T, and INPUTFMIUG=T. The latter allows to use the natural occupancies from the previous point but not the natural orbitals, since the latter may change significantly after the displacement of nuclear coordinates. ORTHO=T ensures the orthonormality of the orbitals along the dissociation procedure.


