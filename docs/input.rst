#############
Input Options
#############

Use only capital letters in the input file, except for specific cases (see below). For instance, "RUNTYP=energy" will not work, but "RUNTYP=ENERGY" yes.

*********
Basis Set
*********

For the moment DoNOF requires to read the basis set for any calculation from the input file. Regarding the format, for historical reasons we employ the format used in GAMESS US. You will find corresponding basis for any atomic element in https://www.basissetexchange.org/. Note that you must use the "Advanced" option from the "Download basis set" box, and there choose the "GAMESS US" format, Version 1, and click the button to activate the "Optimize General Contractions". This will automatically give you the information to put in the input file.

Many examples are shown in the section "Examples".

*******
&INPRUN
*******

The &INPRUN namelist specifies the run type, the atomic basis, and similar fundamental job options. These options are controlled by the following keywords:

RUNTYP:    Specifies the run calculation

    = ENERGY   single-point energy calculation (Default)

    = GRAD   energy + gradients with respect to nuclear coord.

    = OPTGEO  optimize the molecular geometry
    
MULT:      Multiplicity of the electronic state

    = 1      singlet (Default)

    = 2,3,... doublet, triplet, and so on

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

Number of total iterations
^^^^^^^^^^^^^^^^^^^^^^^^^^

MAXIT:               Maximum number of OCC-SCF iterations 

    = 1000   (DEFAULT)


Type of calculation
^^^^^^^^^^^^^^^^^^^

ICOEF:               Coefficient Optimization

                      = 0      Optimize Energy only by the occupations
                      
                      = 1      use the ID (SCF) method (DEFAULT)
                      
                      = 2      Optimize Energy only by the orbitals
                      
                      = 3      Optimize Energy by all occupations and only core-fragment orbitals, the rest of fragment orbitals remain frozen

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

NTHRESHEID          Convergence of the total energy
                    THRESHEID=10.0**(-NTHRESHEID)
                     
                      = 8      (DEFAULT)

MAXITID             Maximum number of external iterations
                     
                      = 30     (DEFAULT)

PNOF Selection
^^^^^^^^^^^^^^

IPNOF:               Type of Natural Orbital Functional (see section "NOF approximations")

                      = 3      PNOF3

                      = 4      PNOF4

                      = 5      PNOF5
                      
                      = 6      PNOF6
                      
                      = 7      PNOF5 + Inter-pair (DEFAULT)

NCWO:                Number of coupled weakly occupied MOs per strongly occupied = Nc -> PNOFi(Nc)

                      = 1      NCWO = 1 (DEFAULT)
                      
                      = 2,3,etc.
                      
                      =-1      NCWO = NVIR/NDOC where NVIR: Number of HF virtual MOs (OCC=0) and NDOC: Number of strongly occupied MOs

Ista:                Use Static version of PNOF7

                      = 0      PNOF7 (DEFAULT)
                      
                      = 1      PNOF7s
                      
HighSpin             Spin-uncompensated calculation type

                      = F      (DEFAULT) Multiple state (Ms=0)

                      = T      High-spin uncompensated state (Ms=S)


Convergence criteria in NOF calculation
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Fore more info see section 3 in [CPC (2020) by Piris and Mitxelena]

NTHRESHL:            Convergence of the lagrange multipliers THRESHL=10.0**(-NTHRESHL)

                      = 4      (DEFAULT)

NTHRESHE:            Convergence of the total energy THRESHE=10.0**(-NTHRESHE)

                      = 6      (DEFAULT)

NTHRESHEC:           Convergence of the total energy (ORBOPT) THRESHEC=10.0**(-NTHRESHEC)

                      = 12     (DEFAULT)

NTHRESHEN:           Convergence of the total energy (OCCOPT) THRESHEN=10.0**(-NTHRESHEN)

                      = 16     (DEFAULT)


Options for the occupation (GAMMA) and nuclear geometry optimization program
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

ICGMETHOD:           Define the congate gradient method in routines OCCOPTr, CALTijabIsym and OPTIMIZE

                      = 1      (DEFAULT)
                               SUMSL: CGOCUPSUMSLr,OPTSUMSL
                               SparseSymLinearSystem_CG

                      = 2      Use NAG routines:
                               E04DGF: OPTCGNAG,CGOCUPNAGr
                               F11JEF: SparseSymLinearSystem_NAG         

                      = 3      LBFGS: OPTLBFGS,LBFGSOCUPr

See more details in "Additional notes" section


Options for the orbital optimization program (ID method)
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

For more info see [JCC 30, 2078 (2009)]

For computational details see section 3 in [CPC (2020) by Piris and Mitxelena]

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


Options for perturbative calculations
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

For more info see [PRA 98, 022504 (2018)]

OIMP2:               NOF - Orbital Invariant MP2

                     = F       (DEFAULT)

SC2MCPT:             SC2-MCPT perturbation theory is used to correct the PNOF5 Energy. 2 outputs: PNOF5-SC2-MCPT and PNOF5-PT2

                     = F       (DEFAULT)

NO1PT2:              Frozen MOs in perturbative calculations. Maximum index of NOs with Occupation = 1

                      = -1     = NO1 (DEFAULT)
                      
                      = 0      All NOs are considered
                      
                      = Value  User specifies how many NOs are frozen

NEX:                 Number of excluded coupled orbitals in the PNOF5-PT2 calculation

                      = 0      All NOs are included (DEFAULT)


Restart options for GAMMA, C, diagonal F, and nuclear coordinates
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

RESTART:             Restart from GCF file (DEFAULT=F)

                      = F      ; corresponds to INPUTGAMMA=0,INPUTC=0,INPUTFMIUG=0
                      
                      = T      ; corresponds to INPUTGAMMA=1,INPUTC=1,INPUTFMIUG=1

INPUTGAMMA:          Guess for gamma matrix in NOF

                      = 0      No input (DEFAULT)
                      
                      = 1      Input from GCF file

INPUTC:              Guess for coefficient matrix in NOF

                      = 0      No input, use HF (DEFAULT)
                      
                      = 1      Input from GCF file

INPUTFMIUG:          Guess for diagonal elements (FMIUG0)

                      = 0      No input (DEFAULT)
                      
                      = 1      Input from GCF file

INPUTCXYZ:           Read nuclear coordinates (Cxyz)

                      = 0      From file INP
                      
                      = 1      From file GCF


Output options
^^^^^^^^^^^^^^

NPRINT:              Output option (DEFAULT VALUE: 0)

                      = 0      Short Printing
                      
                      = 1      Output at initial and final iterations including MOs,Pop,APSG,Lag,IPs,DMs,CJK
                      
                      = 2      Output everything at each iteration

IWRITEC:             Output option for the coefficient matrix

                      = 0      No output (DEFAULT)
                      
                      = 1      Output the coefficient matrix

IMULPOP:             Mulliken population analysis

                      = 0      Do not do (DEFAULT)
                      
                      = 1      Do a Mulliken pop. analysis

PRINTLAG:            Output option for the lagrange multipliers

                      = F      No output (DEFAULT)

DIAGLAG:             Diagonalize lagrange multipliers print canonical vectors and print new diagonal elements of 1RDM

                      = F      (DEFAULT)

IEKT:                Use the EKT (DEFAULT VALUE = 0)

                      = 1      Calculate ionization potentials

IAIMPAC:             Write information into a WFN file  (UNIT 7) for the AIMPAC program

                      = 0      Do not do

                      = 1      Write into a WFN file (DEFAULT)

NOUTRDM:             Print option for atomic RDMs

                      = 0      No output (DEFAULT)

                      = 1      Print atomic RDMs in 1RDM and 2RDM files

NTHRESHDM:           THRESHDM=10.0**(-NTHRESHDM)

                      = 6      (DEFAULT)

NSQT:                Use an unformatted 2RDM file

                      = 1      (DEFAULT)

NOUTCJK:             Print option for CJ12 and CK12

                      = 0      No output (DEFAULT)

                      = 1      Print CJ12 and CK12 in file 'CJK'

NTHRESHCJK:          THRESHCJK=10.0**(-NTHRESHCJK)

                      = 6      (DEFAULT)

NOUTTijab:           Print option for Tijab

                      = 0      No output (DEFAULT)

                      = 1      Print Tijab in file 'Tijab'

NTHRESHTijab:        THRESHTijab=10.0**(-NTHRESHTijab)

                      = 6      (DEFAULT)

APSG                 Open an APSG file for printing the coefficient matrix ($VEC-$END) and the expansion coefficients of the APSG generating wavefunction.

                      = F      Output (DEFAULT)

NTHAPSG:             Threshold for APSG expansion coefficients THAPSG = 10.0**(-NTHAPSG)

                      = 10     (DEFAULT)


Options related to orthonormality of Natural Orbitals
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

ORTHO:               Orthogonalize the initial orbitals

                      = F      No 
                      
                      = T      Yes (DEFAULT)

CHKORTHO:            Check the orthonormality of the MOs

                      = F      No (DEFAULT)
                      
                      = T      Yes


Options related to frozen coordinates in geometry optimization
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

See also "Additional notes" section

FROZEN:              Is there any fixed coordinate

                      = F      (DEFAULT)

IFROZEN:             By pairs, what coordinate of which atom, e.g. 2,5,1,1 means "y" coordinate of atom 5 and "x" coor of atom 1 to freeze. MAXIMUM of frozen coordinates = 10

                      = 0      (DEFAULT)


****************
Additional Notes
****************


Dependencies
^^^^^^^^^^^^

You may notice above that setting ICGMETHOD=2 in the input file DoNOF will use the conjugate gradient algorithm coded in NAG for the optimization of natural occupancies, as well as nuclear coordinates (if RUNTYP=OPTGEO). However, since the license of NAG is restricted (see https://www.nag.co.uk/content/nag-library), these routines are not provided by DoNOF and the user must include them to the code. Namely, the following routines are called by DoNOF if ICGMETHOD=2: E04DGF, E04UEF, E04UCF, and F11JEF. The latter is required for perturbative calculations, while the other routines are required for optimization processes.

That is why by default DoNOF employs the "SUMSL" routine to minimize a general unconstrained objective function.For more details see the next references:

J E Dennis, David Gay, and R E Welsch,
An Adaptive Nonlinear Least-squares Algorithm,
ACM Transactions on Mathematical Software,
Volume 7, Number 3, 1981.

J E Dennis, H H W Mei,                                            
Two New Unconstrained Optimization Algorithms Which Use           
Function and Gradient Values,                                     
Journal of Optimization Theory and Applications,                  
Volume 28, pages 453-482, 1979.

J E Dennis, Jorge More,                                           
Quasi-Newton Methods, Motivation and Theory,                      
SIAM Review,                                                      
Volume 19, pages 46-89, 1977.

D Goldfarb,                                                       
Factorized Variable Metric Methods for Unconstrained Optimization,
Mathematics of Computation,                                       
Volume 30, pages 796-811, 1976.

Alternatively, we have also implemented the LBFGS algorithm written by J. Nocedal (see http://users.iems.northwestern.edu/~nocedal/lbfgs.html, and cite references therein if ICGMETHOD=3) for the occupation and geometry optimizations. This method is activated by setting ICGMETHOD=3). In our experience, LBFGS works fine for occupation optimization, whereas it must be employed carefully for geometry optimization as detailed below.

New algorithms and numerical methods for carrying out these optimizations are welcome, so we encourage new collaborations to work on this task.


Geometry Optimization
^^^^^^^^^^^^^^^^^^^^^

If RUNTYP=OPTGEO is set, DoNOF automatically will set HFID=F and OIMP2=F at the beginning of the calculation.

Related with the previous section, for geometry optimization (RUNTYP=OPTGEO) it is strongly recommended to set ICGMETHOD=1 (DEFAULT) or ICGMETHOD=2. In fact, the latter has proven to be much more accurate than LBFGS for this task. The LBFGS algorithm has been employed before in quantum chemistry programs to optimize the geometry (see http://openmopac.net/Manual/lbfgs.html). Since LBFGS employs very low memory it is recommended only if a large number of variables is to be optimized. Nevertheless, LBFGS may not work accurately if low-energy interactions are significant in our system.

RUNTYP=OPTGEO may be a computationally demanding task for any ICGMETHOD option. Nevertheless, we have demonstrated (JCP 146, 014102 (2017)) that PNOF approximations produce similar equilibrium geometries for perfect pairing or larger coupling options (i.e. NCWO>1). Therefore, for RUNTYP=OPTGEO is recommended to employ the minimum value of NCWO, that is, run a single-point calculation and check in the output how many weakly-occupied-orbitals have significant occupancies in each subspace. For example, if there are two weakly-occupied-orbitals with non-negligible occupations in each subspace, it will be enough to set NCWO=2 in the RUNTYP=OPTGEO calculation. This can save a large amount of computational time and produce similar equilibrium geometries to those that would be obtained by considering all orbitals correlated with a large basis set.

GCF: All information required to restart any calculation is printed in a file called GCF during the iterative procedure. At the end of the calculation this file is renamed to "name-of-the-molecule.gcf". It is worth noting that at the end of the GCF the nuclear coordinates are printed. The latter are read at the beginning of the calculation (so the ones from the .inp file are ignored) only if explicitly required by the user, by setting INPUTCXYZ=1 or if RESTART=T in $NOFINP. This option is particularly useful if the calculation stops unexpectedly during the geometry optimization procedure (RUNTYP=OPTGEO). If that is the case, run a new calculation setting RUNTYP=ENERGY, RESTART=F, and INPUTCXYZ=1 to converge the energy at the last geometry obtained during the geometry optimization. Then you can just set regular geometry optimization calculation, i.e. RUNTYP=OPTGEO, RESTART=T, and INPUTCXYZ=0. In this vein, the GCFe file (that contains the minimal energy obtained during each single-point calculation) can be ignored for RUNTYP=OPTGEO.

Regarding number of initial zeroes at Fij matrix, NZEROSr, it is convenient to set NZEROSr=0 if RUNTYP=OPTGEO. In fact, the solution can change significantly after a displacement of nuclei, then we must let free the SCF procedure. On the contrary, if we restart a calculation that is almost converged, we can save some extra iterations by setting some initial value for NZEROSr, e.g. NZEROSr=2 or NZEROSr=3 depending on the system and how close from the solution is out starting point (in the GCF file).

In geometry optimization calculations (RUNTYP=OPTGEO), you will note that a file named CGGRAD is created during the calculation. Once the calculation ends it is renamed to "name-of-the-molecule.cgo". This file contains information about the geometry optimization procedure carried out by using the conjugate gradient method (set in the input file by ICGMETHOD), as well as the Hessian and harmonic vibrational frequencies at the solution point. Recall that the Hessian is computed by numerical differentiation of the analytic energy gradients (see details at I. Mitxelena et al. Adv Quant. Chem. ISSN 0065-3276 (2019)), so numerical precision of reported harmonic vibrational frequencies is limited and, apriori, they should be taken only qualitatively.

You may notice in the $NOFINP section that a keyword FROZEN is used to fix nuclear coordinates during geometry optimization. This is done in cartesians, though it is recommended, for obvious reasons, doing it by using internal coordinates. For the moment this has not been implemented in DoNOF yet. Therefore, we recommend the user to employ FROZEN carefully.


Dissociation
^^^^^^^^^^^^

Molecular dissociation is considered the main still unresolved problem of DFT, but of fundamental interest for quantum chemistry. PNOF methods are able to reproduce benchmark potential energy curves of molecular bond dissociation. Nevertheless, this calculation is tricky and must be carried out carefully. In fact, different solutions may arise during the dissociation process depending on the electron correlation present in our system. Computationally it is convenient to converge a single-point calculation to NTHRESHL=5, and then start the dissociation process manually by setting: RESTART=F, ORTHO=T, and INPUTFMIUG=T. The latter allows to use the natural occupancies from the previous point but not the natural orbitals, since the latter may change significantly after the displacement of nuclear coordinates. ORTHO=T ensures the orthonormality of the orbitals along the dissociation procedure.

Symmetry
^^^^^^^^

In DoNOF point-group symmetry is not employed, so C1 symmetry is assumed for any molecular system.

WFN file
^^^^^^^^

The WFN file contains the necessary info to study the output data by using external programs, such as AIMPAC. Note that in this WFN file the energy is referred to as "HF energy", but it really corresponds to the PNOF energy.


Numerical Precision
^^^^^^^^^^^^^^^^^^^

You may notice that different numerical precision is shown for each quantity (orbitals, energy, occupancies, etc) in the output file. The latter is done according to the trustworthy precision inherent to NOF methods. On the contrary, for other purposes such as restarting a calculation is more convenient to employ as much digits as possible. Accordingly, you should use data from the GCF file.


