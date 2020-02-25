Input Options
=====
The simplest input.::

    $nofinp

The &INPRUN namelist specifies the run type, use of core potentials,
the atomic basis, and similar fundamental job options. These options
are controlled by the following keywords:

RUNTYP:  specifies the run calculation

    = ENERGY  1) single-point energy calculation (Default)

    = GRAD   2) energy + gradients with respect to nuclear coord.

    = OPTGEO 3) optimize the molecular geometry
    
MULT:    Multiplicity of the electronic state

    = 1      singlet (Default)

    = 2,3,...doublet, triplet, and so on

ICHARG:  Molecular charge

    = 0  Neutral Molecule (Default)

IEMOM:   Electrostatic moments calculation

    = 0      skip calculation

    = 1      calculate monopole and dipole (Default)

    = 2      also calculate quadrupole moments

    = 3      also calculate octopole moments

UNITS:   Distance units (Any angles must be in degrees)

    = ANGS   Angstroms (Default)

    = BOHR   Bohr atomic units

EVEC:    An array of the three x,y,z components of the applied electric field, in a.u. (1 a.u. = 1 Hartree/e*bohr = 5.1422082(15)d+11 V/m)

    = ZERO   (Default)

DONTW:   Do not write 2e- integrals on the disk (Unit=1)

    = F      (Default)
    
    = T
    
    
The &NOFINP namelist specifies the type of PNOF calculation, options
for the iterative diagonalization method, perturbative corrections,
input and output, and similar fundamental job options. These options
are controlled by the following keywords:
    
-----------------------------------------------------------------------
                     --- NAMELIST VARIABLES ---
-----------------------------------------------------------------------

.......... MAXIT               Maximum number of OCC-SCF iterations 
                      = 1000   (DEFAULT)

- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
 Type of Calculation
- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -

.......... ICOEF               Coefficient Optimization 
                      = 0      Optimize Energy only by the occupations
                      = 1      use the ID (SCF) method (DEFAULT)
                      = 2      Optimize Energy only by the orbitals
                      = 3      Optimize Energy by all occupations and
                               only core-fragment orbitals, the rest
                               of fragment orbitals remain frozen
                      = 4      use a HF-like Fockian

.......... IEINI               Calculate only the initial energy
                      = 0      (DEFAULT)

.......... NO1                 MAX. index of NOs with Occupation = 1
                      = -1     Consider Core NOs (DEFAULT)
                      = 0      All NOs are considered
                      = Value  User specifies how many NOs have OCC.=1

- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
 Hartree-Fock
- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -

..........  HFID               Use the Iterative Diagonalization Method 
                               to generate the HF Orbitals
                      = F      HF MO (DEFAULT)
                      = T      HF MO are obtained using the ID (HFIDr)

- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
 PNOF Selection
- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -

.......... IPNOF               Type of Natural Orbital Functional (NOF)
                      = 5      PNOF5
                      = 6      PNOF6
                      = 7      PNOF5 + Inter-pair (DEFAULT)

.......... NCWO                Number of coupled weakly occupied MOs 
                               per strongly occupied = Nc -> PNOFi(Nc)
                      = 1      NCWO = 1 (DEFAULT)
                      = 2,3,...
                      =-1      NCWO = NVIR/NDOC
                               NVIR: Number of HF virtual  MOs (OCC=0)
                               NDOC: Number of strongly occupied MOs

.......... Ista                Use Static version of PNOF7 
                      = 0      PNOF7 ((DEFAULT)
                      = 1      PNOF7s

- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
 Convergence Criteria in NOF calculation
 Fore more info see section X in [1]
- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -

.......... NTHRESHL            CONVERGENCE OF THE LAGRANGE MULTIPLIERS
                               THRESHL=10.0**(-NTHRESHL)
                      = 4      (DEFAULT)

.......... NTHRESHE            CONVERGENCE OF THE TOTAL ENERGY
                               THRESHE=10.0**(-NTHRESHE)
                      = 6      (DEFAULT)

.......... NTHRESHEC           CONVERGENCE OF THE TOTAL ENERGY (ORBOPT)
                               THRESHEC=10.0**(-NTHRESHEC)
                      = 12     (DEFAULT)

.......... NTHRESHEN           CONVERGENCE OF THE TOTAL ENERGY (OCCOPT)
                               THRESHEN=10.0**(-NTHRESHEN)
                      = 16     (DEFAULT)

- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
 Options for the Occupation (GAMMA) Optimization Program
- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -

.......... USENAG              Use NAG Library Routine: DUMCGG
                      = T      (DEFAULT)
                      = F      use instead a LBFGS method (see note
                               in "Additional notes" section)

- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
 Options for the Orbital Optimization Program (ID Method)
 For more info see [2, i.e. JCC 2009]
 For computational details see section X in [1]
- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -

.......... NOPTORB             Number of the optimized orbitals
                      = NBF    (DEFAULT)

.......... MAXLOOP             Maximum Iteration Number for the SCF-
                               ITERATION cycle in each ITCALLs 
                      = 30     (DEFAULT)

     The straightforward iterative scheme fails to converge very 
     often due to the values of some off-diagonal elements Fki. The 
     latters must be suffciently small and of the same order of 
     magnitude. A variable factor scales Fki. We establish an upper
     bound B, in such a way that when the absolute value of the 
     matrix element Fki is greater than B, it is scaled by a factor 
     Cki (F'ki = Cki*Fki ), as to satisfy ABS(Fki) <= B.

.......... SCALING             A variable factor scales Fki
                      = T      (DEFAULT)

.......... NZEROS              B = 10.0**(1-NZEROS). 
                               Initial number of ZEROS in Fij. The 
                               scaling factor varies until the number 
                               of ZEROS (.000##) is equal for all 
                               elements Fij.
                      = 0      B = 10.0 (DEFAULT)

.......... NZEROSm             B = 10.0**(1-NZEROSm)
                               Maximum number of zeros in Fij.
                      = 4      B = 10.0 (DEFAULT)

.......... NZEROSr             B = 10.0**(1-NZEROSr)
                               Number of zeros in Fij to restart 
                               automatically the calculation.
                      = 0      B = 10.0 (DEFAULT)

.......... ITZITER             Number of Iterations for constant scaling
                      = 10     (DEFAULT)

.......... DIIS                Direct Inversion in the Iterative 
                               Subspace in the orbital optimization if 
                               DUMEL < THDIIS every NDIIS loops
                      = T      (DEFAULT)

.......... NTHDIIS             Energy threshold to begin DIIS
                      = 3      THDIIS = 10.0**(-NTHDIIS) (DEFAULT)

.......... NDIIS               Number of considered loops to interpolate
                               the generalized Fock matrix in the DIIS
                      = 5      (DEFAULT)

.......... PERDIIS             Periodic DIIS
                      = T      Apply DIIS every NDIIS (DEFAULT)
                      = F      DIIS is always applied after NDIIS

- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
 Options for pertubative calculations
 For more info see [3, i.e. PRA 2019]
- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -

.......... CLMP2               Correlated local MP2 = NOF - oiMP2
                     = F       (DEFAULT)

.......... SC2MCPT             SC2-MCPT perturbation theory is used to
                               correct the PNOF5 Energy. 
                               2 outputs: PNOF5-SC2-MCPT and PNOF5-PT2
                     = F       (DEFAULT)

.......... NO1PT2              Frozen MOs in perturbative calculations
                               Maximum index of NOs with Occupation = 1
                      = -1     = NO1 (DEFAULT)
                      = 0      All NOs are considered
                      = Value  User specifies how many NOs are frozen

.......... NEX                 Number of excluded coupled orbitals 
                               in the PNOF5-PT2 calculation
                      = 0      All NOs are included (DEFAULT)

- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
 Restart Options for Gamma (Occ), C, Diagonal F, and nuclei
- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -

.......... RESTART             RESTART FROM GCF FILE (DEFAULT=F)
                      = F      INPUTGAMMA=0,INPUTC=0,INPUTFMIUG=0
                      = T      INPUTGAMMA=1,INPUTC=1,INPUTFMIUG=1

.......... INPUTGAMMA          GUESS FOR GAMMA MATRIX IN NOF
                      = 0      NO INPUT (DEFAULT)
                      = 1      INPUT FROM FILE GCF

.......... INPUTC              GUESS FOR COEFFICIENT MATRIX IN NOF
                      = 0      NO INPUT, USE HF (DEFAULT)
                      = 1      INPUT FROM FILE GCF

.......... INPUTFMIUG          GUESS FOR DIAGONAL ELEMENTS (FMIUG0)
                      = 0      NO INPUT (DEFAULT)
                      = 1      INPUT FROM FILE GCF

.......... INPUTCXYZ           READ NUCLEAR COORDINATES (Cxyz)
                      = 0      INPUT FROM FILE INP
                      = 1      INPUT FROM FILE GCF

- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
 Output Options
- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -

.......... NPRINT              OUTPUT OPTION (DEFAULT VALUE: 0)
                      = 0      Short Printing
                      = 1      Output at initial and final iterations
                               including Ei,Coef,Pop,Occ,Emom
                      = 2      Output at each iteration

.......... IWRITEC             OUTPUT OPTION FOR THE COEFFICIENT MATRIX
                      = 0      NO OUTPUT (DEFAULT)
                      = 1      OUTPUT THE COEFFICIENT MATRIX 

.......... IWRITEE             Output option for one-particle energies
                      = 0      No Output (Default)
                      = 1      Output EiHF, Elag

.......... IMULPOP             MULLIKEN POPULATION ANALYSIS
                      = 0      DO NOT DO (DEFAULT)
                      = 1      DO A MULLIKEN POP. ANALYSIS 

.......... APSG                OPEN AN APSG FILE FOR OUTPUT THE 
                               COEFFICIENT MATRIX ($VEC-$END) AND THE
                               EXPANSION COEFFICIENTS OF THE APSG
                               GENERATING WAVEFUNCTION.
                      = F      OUTPUT (DEFAULT)

.......... NTHAPSG             THRESHOLD FOR APSG EXPANSION COEFFICIENTS
                               THAPSG = 10.0**(-NTHAPSG)
                      = 10     (DEFAULT)

.......... PRINTLAG            OUTPUT OPTION FOR THE LAGRANGE MULTIPLIERS
                      = F      NO OUTPUT (DEFAULT)

.......... DIAGLAG             DIAGONALIZE LAGRANGE MULTIPLIERS
                               PRINT CANONICAL VECTORS and 
                               PRINT NEW DIAGONAL ELEMENTS OF 1-RDM
                      = F      (DEFAULT)

.......... IAIMPAC             WRITE INFORMATION INTO A WFN FILE (UNIT 7)
                               FOR THE AIMPAC PROGRAM
                      = 0      DO NOT DO 
                      = 1      WRITE INTO WFN FILE (DEFAULT)

.......... IEKT                Use the EKT (DEFAULT VALUE = 0)
                      = 1      Calculate ionization potentials 

.......... ICATION             (DEFAULT VALUE = 0)
                      = 1      Calculate the Cation Energy 
                               (Eelec+EN+IonPotential)

.......... ICHEMPOT            (DEFAULT VALUE = 0)
                      = 1      Calculate the Chemical Potential

.......... NOUTRDM             PRINT OPTION FOR ATOMIC RDMs 
                      = 0      NO OUTPUT (DEFAULT)
                      = 1      PRINT ATOMIC RDMs IN 1DM and 2DM FILES

.......... NTHRESHDM           THRESHDM=10.0**(-NTHRESHDM)
                      = 6      (DEFAULT)

.......... NSQT                Use an unformatted 2DM file.
                      = 1      (DEFAULT)

.......... NOUTCJK             PRINT OPTION FOR CJ12 and CK12
                      = 0      NO OUTPUT (DEFAULT)
                      = 1      PRINT CJ12 and CK12 in FILE 'CJK'

.......... NTHRESHCJK          THRESHCJK=10.0**(-NTHRESHCJK)
                      = 6      (DEFAULT)

.......... NOUTTijab           PRINT OPTION FOR Tijab
                      = 0      NO OUTPUT (DEFAULT)
                      = 1      PRINT Tijab in FILE 'Tijab'

.......... NTHRESHTijab        THRESHTijab=10.0**(-NTHRESHTijab)
                      = 6      (DEFAULT)

.......... IGVB                GVB orbitals connection to PNOFi(1) NOS
                      = 0      (DEFAULT)
       
- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
 Optional Options
- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -

.......... ORTHO               Orthogonalize the initial orbitals
                      = F      No 
                      = T      Yes (DEFAULT)

.......... CHKORTHO            CHECK THE ORTHONORMALITY OF THE MOs
                      = F      No (DEFAULT)
                      = T      Yes

- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
 Options related to Frozen coordinates in gradient computation
- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -

.......... FROZEN              Is there any fixed coordinate
                      = F      (DEFAULT)

.......... IFROZEN             By pairs, what coordinate of which atom,
                               e.g. 2,5,1,1 means "y" coordinate of
                               atom 5 and "x" coor of atom 1 to freeze.
                               MAXIMUM of frozen coordinates = 10
                      = 0      (DEFAULT)


Additional Notes
^^^
LBFGS: good for large, but lacks precision

GCF: contains geometry just if optgeo stops

NZEROSr should be zero if IRUNTYP==3

HESSIAN and FREQS: only qualitative meaning

For optgeo only print intermediate info if NPRINT=2,
and forget GCFe if it ends badly


Examples
^^^^

Single-point

Hartree-Fock

Geometry Optimization

Convergence

