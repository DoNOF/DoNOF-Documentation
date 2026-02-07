#############
Input Options
############# 

Use only capital letters in the input file, except for specific cases (see below). For instance, RUNTYP='energy' will not work, but RUNTYP='ENERGY' will.

*********
Basis Set
*********

The basis set for any calculation can be read from 'basis-name.bas' (see examples in folder https://github.com/DoNOF/DoNOFsw/tree/master/basis) or introduced in the input file (see examples in https://github.com/DoNOF/DoNOFsw/tree/master/examples). 

The basis set is specified on line 4 of the input file after the title. In case the basis set is provided in the input file, line 4 should be left blank. For historical reasons, we employ the format used in GAMESS US software package.

The file containing the basis sets (basis-name.bas) can be located in the directory where the calculation is performed ($PWD), in $HOME/DoNOFsw/basis/, $HOME/DoNOF/basis/ directories, or you can specify the full path where it is located, that is, PATH/basis-name.bas.

You can find corresponding basis sets for any atomic element in https://www.basissetexchange.org/. You must choose the "GAMESS US" format in the "Download basis set" box. In addition, you can use "Advanced" options from the "Download basis set" box to activate different options and versions of the basis set in the "GAMESS US" format, for instance, the "Optimize General Contractions" option.

*******
&INPRUN
*******

The &INPRUN namelist specifies the run type and other fundamental job options. These options are controlled by the following keywords:

RUNTYP:    Specifies the run calculation

    = 'ENERGY' single-point energy calculation (Default)

    = 'GRAD' energy + gradients with respect to nuclear coordinates

    = 'OPTGEO' optimize the molecular geometry
    
    = 'HESS' compute numerical hessian from analytic gradients

    = DYN run Born-Oppenheimer on-the-fly molecular dynamics
    
MULT:      Multiplicity of the electronic state

    = 1       singlet (Default)

    = 2,3,... doublet, triplet, and so on

ICHARG:    Molecular charge

    = 0    Neutral Molecule (Default)
    
IECP:      Effective Core Potentials 

    = 0    All electron calculation (Default) 
    
    = 1    Read ECP potentials in the $ECP group

IEMOM:     Calculation of electrostatic moments

    = 1    calculate dipole moments (Default)

    = 2    also calculate quadrupole moments

    = 3    also calculate octopole moments

NLOP:      Non-Linear Optical Properties

    = -1   calculate Alpha, Beta & Gamma

    =  0   No calculation of NLOPs (Default)

    =  1   calculate polarizability Alpha

    =  2   calculate 1st-order hyperpolarizability Beta

    =  3   calculate 2nd-order hyperpolarizability Gamma

NPOINT:    Number of steps used in the dyadic scaling of the electric field. It represents the total number of fields that will be considered in the calculations

    = 9   (Default)

STEP:      Initial step size for the electric field. It defines the base value of the field for the first step, with subsequent values being scaled by powers of 2.

    = 1.0d-04 (Default)

ISOALPHA:   Computes the diagonal components of the static polarizability tensor (αxx, αyy, αzz) using the dyadic Romberg–Richardson scheme looping the field direction over x, y, z. Then reports the isotropic average and the anisotropy (Raman convention)

     = 0    (Default)

UNITS:       Distance units (Any angles must be in degrees)

    = ANGS   Angstroms (Default)

    = BOHR   Bohr atomic units

EVEC:        An array of the three x,y,z components of the applied electric field, in a.u. (1 a.u. = 1 Hartree/e*Bohr = 5.1422082(15)d+11 V/m)

    = 0.0D0  (Default)

GTYP:        Type of Gaussian functions

      = CART Cartesian 

      = SPH  Spherical (Default)
    
DONTW:       Do not write 2e- integrals on the disk (Unit=1)

    = T      (Default)
    
ERITYP:      Typ of ERIs used in calculations

    = FULL   4c ERIs (Default)
    
    = RI     3c/2c ERIs for Resolution of the Identity (RI) App.
    
    = MIX    3c/2c ERIs for Resolution of the Identity (RI) App. once converged change to 4c ERIs (FULL)

CUTOFF       The Schwarz screening cut off for NAT>5

    = 1.0D-9 (Default)

RITYP        Typ of Auxiliary Basis

    = JKFIT  Read from jkfit files (Default)

    = GEN    Use Generative Auxiliary Basis

GEN:         Generative Auxiliary Basis to use in RI Approx. if ERITYP = RI. Values: A2,A2*,A3,A3*,A4,A4* 
             
    = A2*    (Default)

SMCD:        Symmetric Modified Cholesky Decomposition for the G matrix in the RI Approximation

   = F       (Default)
    
HSSCAL:      Compute Hessian from analytic gradients and carry out normal mode vibrational analysis at st. point if RUNTYP = OPTGEO (IRUNTYP=3)

   = T       (Default)

PROJECT:     Project Hessian to eliminate rot/vib contaminants

    = T      (Default)

ISIGMA:      Rotational symmetric number for thermochemistry

    = 1      There is not a center of symmetry (Default)
    
    = 2      There is a center of symmetry
    
             For more info see https://cccbdb.nist.gov/thermo.asp

NATmax:      Maximum Number of Atoms

   = 100     (Default)

NSHELLmax:  Maximum Number of Shells

   = 500    (Default)

NPRIMImax:  Maximum Number of Gaussian Functions

    = 2000  (Default)

USEHUB:     Use Hubbard Model Hamiltonian (1D,2D) (See Options in &INPHUB namelist)

    = F     (Default)
    
&INPHUB
^^^^^^^
The &INPHUB namelist specifies the type of Hubbard calculation

NSITE:      Number of sites in one dimension

    = 1     (Default)

NELEC:      Number of electrons

    = 1     (Default)

NDIMH:      Dimension considered in the Hubbard model

    = 1     (Default)

THOP:       Near-neighbors hopping (t>0)

   = 1.0d0  (Default)

UONS:       On-site energy = The site interaction parameter (U)

   = 1.0d0  (Default)
   

*******
&NOFINP
*******

The &NOFINP namelist specifies the type of PNOF calculation, options
for the iterative diagonalization method, perturbative corrections,
input and output, and similar fundamental job options. These options
are controlled by the following keywords:

Number of total iterations
^^^^^^^^^^^^^^^^^^^^^^^^^^

MAXIT:       Maximum number of OCC-SCF iterations 

    = 1000   (Default)


Type of calculation
^^^^^^^^^^^^^^^^^^^

ICOEF:       Energy Optimization with respect to Coefficient Matrix (Natural Orbitals)

    = 0      Optimize only with respect to Gamma variables that determine the occupation numbers
                      
    = 1      Optimize with respect to Gammas and Coefficient matrix (Default)
                      
    = 2      Optimize only by the orbitals keeping fixed the occupation numbers
                      
    = 3      Optimize by all occupations and core-fragment orbitals. The rest of fragment orbitals remain frozen

ISOFTMAX:    Parameterization type for the occupation numbers

    = 0      Trigonometric

    = 1      Softmax function (Default)

IORBOPT:     Select method for natural orbital optimization

    = 1      Iterative diagonalization

    = 2      Adaptative Momentum (ADAM) (Default)

IEINI:       Calculate only the initial energy

    = 0      (Default)

NO1:         Maximum index of natural orbitals with occupation numbers equal to 1.0

    = -1     Consider core natural orbitals 
                      
    = 0      All natural orbitals are considered (Default)
                      
    = Value  The user specifies how many natural orbitals have occupations equal to 1.0

Note: Use this option with caution, as orbitals may rearrange during optimization.

HARTREE-FOCK
^^^^^^^^^^^^

IRHF:        Restricted Hartree-Fock Calculation

    = 0      Not obtaining HF orbitals

    = 1      Self Consistent Field (SCF) (Default)

    = 2      Orbital rotations through ADAM

    = 3      Iterative Diagonalization (ID) Method

NCONVRHF:    RHF-SCF Density Convergence Criteria CONVRHFDM=10.0**(-NCONVRHF)

    = 5      (Default)
    
MAXITRHF:    Maximum number of RHF-SCF iterations

    = 100    (Default)
    
HFDAMP:      Damping of the Fock matrix

    = T      (Default)
    
HFEXTRAP:    Extrapolation of the Fock matrix

    = T      (Default)
                      
KOOPMANS:    Calculate ionization potentials using Koopmans' Theorem

    = 0      (Default)

PNOF Selection
^^^^^^^^^^^^^^

IPNOF:       Type of Natural Orbital Functional (see section "NOF approximations")

    = 3      PNOF3 + pairing constraints

    = 4      PNOF4 + pairing constraints

    = 5      PNOF5
                      
    = 6      PNOF6
                      
    = 7      PNOF7
    
    = 8      GNOF (Default)
                      
Ista:        Use Static version of PNOF7 if IPNOF=7

    = 0      PNOF7 (Default)
                      
    = 1      PNOF7s (useful in perturbative calculations with the NOF-MP2 method)

Imod:        Select versions of GNOF

    = 0      GNOF (Default)

    = 1      GNOFm

HighSpin:    Spin-uncompensated calculation type

    = F      Spin-Multiplet state (Ms=0) (Default)

    = T      High-spin uncompensated state (Ms=S)                      
                      
NCWO:        Number of coupled weakly occupied NOs per strongly occupied = Nc -> PNOFi(Nc)

    = 1,2,3,...
                      
    =-1      NCWO = NVIR/NDOC (Default)

    NVIR: Number of Hartre-Fock virtual molecular orbitals, now weakly occupied

    NDOC: Number of strongly occupied molecular orbitals

Convergence criteria in NOF calculation
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

NTHRESHL:    Convergence of the Lagrange multipliers, THRESHL=10.0**(-NTHRESHL)

    = 4      (Default)

NTHRESHE:    Convergence of the total energy, THRESHE=10.0**(-NTHRESHE)

    = 8      (Default)

Options for the orbital optimization
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

MAXLOOP:     Maximum Iteration Number for the SCF ITERATION cycle in each ITCALL

    = 10     (Default)

Note: In the case of IORBOPT=1 (iterative diagonalizations), MAXLOOP is fixed, while if IORBOPT=2 (orbital rotations) MAXLOOP changes during optimization to decrease the energy in each outer iteration.

Specific Options for IORBOPT=1
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

    The straightforward iterative scheme fails to converge very often due to the values of some off-diagonal elements Fki. The latters must be suffciently small and of the same order of magnitude. A variable factor scales Fki. We establish an upper bound B, in such a way that when the absolute value of the matrix element Fki is greater than B, it is scaled by a factor Cki (F'ki = Cki*Fki ), as to satisfy ABS(Fki) <= B.

SCALING:     A variable factor scales Fki

    = T      (Default)

NZEROS:      Initial number of ZEROS in Fij [ B = 10.0**(1-NZEROS) ]

The scaling factor varies until the number of ZEROS (.000##) is equal for all elements Fij

    = 0      (Default)

NZEROSm:     Maximum number of zeros in Fij [ B = 10.0**(1-NZEROSm) ]

    = 5      (Default)

NZEROSr:     Number of zeros in Fij to restart automatically the calculation [ B = 10.0**(1-NZEROSr) ]

    = 2      (Default)
                      
AUTOZEROS:   The code select automatically values for NZEROS, NZEROSm & NZEROSr.
                   
    = T      (Default)

Note: Override previously selected values

ITZITER:      Number of Iterations for constant scaling

    = 10     (Default)

DIIS:        Direct Inversion in the Iterative Subspace in the orbital optimization if DUMEL < THDIIS every NDIIS loops

    = T      (Default)

NTHDIIS:     Energy threshold to begin DIIS [ THDIIS = 10.0**(-NTHDIIS) ]

    = 3      (Default)

NDIIS:       Number of considered loops to interpolate the generalized Fock matrix in the DIIS

    = 5      (Default)

PERDIIS:     Periodic DIIS

    = T      Apply DIIS every NDIIS (Default)
                      
    = F      DIIS is always applied after NDIIS

Options for perturbative calculations
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

OIMP2:       Orbital Invariant MP2 [ For more info on NOF-MP2 see PRA 98, 022504, 2018 ]

    = F      (Default)
                     
NO1PT2:      Frozen natural orbitals in OIMP2. Maximum index of NOs with Occupation = 1

   = -1      = NO1 (Default)
                      
   = 0       All natural orbitals are considered
                      
   = Value   The user specifies how many natural orbitals are frozen                   

SC2MCPT:     SC2-MCPT perturbation theory is used to correct the PNOF5 Energy.

    = F      (Default)

Note: Two outputs PNOF5-SC2-MCPT and PNOF5-PT2

NEX:         Number of excluded coupled orbitals in the PNOF5-PT2 calculation

    = 0      All NOs are included (Default)


Restart options for GAMMA, C, diagonal F, and nuclear coordinates
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

RESTART:     Restart from GCF file 

    = F      corresponds to INPUTGAMMA=0,INPUTC=0,INPUTFMIUG=0,INPUTCXYZ=0 (Default)
                      
    = T      corresponds to INPUTGAMMA=1,INPUTC=1,INPUTFMIUG=1,INPUTCXYZ=1

INPUTGAMMA:   Guess for GAMMA variables (determine the Occupation Numbers)

    = 0      Close Fermi-Dirac Distribution (Default)
                      
    = 1      Input from GCF file

INPUTC:      Guess for coefficient matrix (Natural Orbitals)

     = 0     Use Hcore or Hartree-Fock Eigenvectors (Default)
                      
     = 1     Input from GCF file

INPUTFMIUG:   Guess for diagonal elements of the symmetric F matrix (FMIUG0)

     = 0      Use single diagonalization of Lagragian (Default)
                      
     = 1      Input from GCF file

INPUTCXYZ:    Read nuclear coordinates

     = 0      From the input file
                      
     = 1      From GCF file
                      
Output options
^^^^^^^^^^^^^^

NPRINT:       Output option

      = 0     Short Printing (Default)
                      
      = 1     Output at initial and final iterations
                      
      = 2     Output everything at each iteration
      
IAIMPAC:       Write information into a WFN file for the AIMPAC program

      = 0      Don't write (Default)

      = 1      Write into WFN file 
                      
IFCHK:         Write information into Formatted Checkpoint (FCHK) file for visualization software (UNIT 19)
 
      = 0      Don't write
                      
      = 1      Write into FCHK file (Default)
                      
MOLDEN:        Write information into MLD file for the MOLDEN PROGRAM (UNIT 17)

      = 0      Don't write

      = 1      Write into MLD file (Default)

NOUTRDM:       Print option for atomic RDMs

      = 0      Don't print (Default)

      = 1      Print atomic RDMs in 1DM and 2DM files

NTHRESHDM:     THRESHDM = 10.0**(-NTHRESHDM)

      = 6      (Default)

NSQT:          Print OPTION for 2DM file

      = 0      Formatted file

      = 1      Unformatted file (Default)

NOUTCJK:       Print option for CJ12 and CK12

      = 0      No output (Default)

      = 1      Print CJ12 and CK12 in file 'CJK'

NTHRESHCJK:    THRESHCJK = 10.0**(-NTHRESHCJK)

      = 6      (Default)

NOUTTijab:     Print option for Tijab

      = 0      No output (Default)

      = 1      Print Tijab in file 'Tijab'

NTHRESHTijab:  THRESHTijab=10.0**(-NTHRESHTijab)

      = 6      (Default)

APSG:          Open an APSG file for printing the coefficient matrix ($VEC-$END) and the expansion coefficients of the APSG generating wavefunction.

      = F      No output (Default)

NTHAPSG:       Threshold for APSG expansion coefficients THAPSG = 10.0**(-NTHAPSG)

      = 10     (Default)


The following options require NPRINT > 0 to take effect
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

IWRITEC:      Output option for the coefficient matrix

      = 0      Not do it (Default)
                      
      = 1      Do it

IMULPOP:       Mulliken population analysis

      = 0      Not do it (Default)
                      
      = 1      Do it

PRINTLAG:      Output option for the lagrange multipliers

      = F      Not do it (Default)

DIAGLAG:       Diagonalize Lagrange multipliers. Print new 1e- Energies, Canonical MOs, and new diagonal elements of the 1RDM

      = F      Not do it (Default)

IEKT:          Calculate the Ionization Potentials using the Extended Koopmans' Theorem (EKT)

      = 0      Not do it (Default)

      = 1      Do it

Options related to orthonormality of Natural Orbitals
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

ORTHO:         Orthogonalize the initial orbitals

      = F      No 
                      
      = T      Yes (Default)

CHKORTHO:       Check the orthonormality of the MOs

      = F      No (Default)
                      
      = T      Yes

*******
&INPDYN
*******

velflag:   Flag to make constant velocity dynamics

    = F    (Default)

dt:        Time step in fs

    = 1    (Default)

tmax:      Propagation time in fs

    = 100  (Default)
                          
ngcf:      number of GCF files to use in calculation

    = 1    (Default)

Vxyz:      Initial velocities per atom     

    = 0.0  

resflag:   Restart MD calculation

    = F    (Default)

snapshot   Save MLD file in snapshot-t.mld

    = F    (Default)

****************
Additional Notes
****************

By default, DoNOF employs the conjugate gradient (CG) method implemented in the "SUMSL" open-source routine to perform the energy optimization with respect to the GAMMA variables (occupation numbers), and the nuclear coordinates if RUNTYP='OPTGEO'. For more details on SUMSL, see the following references:

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

Geometry Optimization
^^^^^^^^^^^^^^^^^^^^^

If RUNTYP='OPTGEO' is set, DoNOF automatically sets IRHF=0 and OIMP2=F at the beginning of the calculation.

GCF: All information required to restart any calculation is printed in a file called GCF during the iterative procedure. At the end of the calculation this file is renamed to "name-of-the-molecule.gcf" by our supplied run scripts. It is worth noting that at the end of the GCF the nuclear coordinates are printed. The latter are read at the beginning of the calculation (so the ones from the .inp file are ignored) only if explicitly required by the user, by setting INPUTCXYZ=1 or if RESTART=T in $NOFINP. This option is particularly useful if the calculation stops unexpectedly during the geometry optimization procedure (RUNTYP='OPTGEO'). If that is the case, run a new calculation setting INPUTCXYZ=1 to converge the energy from the last obtained geometry.

In geometry optimization calculations (RUNTYP='OPTGEO'), you will note that a file named CGGRAD is created during the calculation. Once the calculation ends it is renamed to "name-of-the-molecule.cgo" by our supplied run scripts. This file contains information about the geometry optimization procedure carried out by using the conjugate gradient method, as well as the Hessian and harmonic vibrational frequencies at the solution point. Recall that the Hessian is computed by numerical differentiation of the analytic energy gradients, so numerical precision of reported harmonic vibrational frequencies is limited and, apriori, they should be taken only qualitatively.

Symmetry
^^^^^^^^

In DoNOF point-group symmetry is not employed, so C1 symmetry is assumed for any molecular system.



