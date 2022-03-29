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

    = 'ENERGY'   single-point energy calculation (Default)

    = 'GRAD'   energy + gradients with respect to nuclear coordinates

    = 'OPTGEO'  optimize the molecular geometry
    
    = 'HESS'   compute numerical hessian from analytic gradients
    
MULT:      Multiplicity of the electronic state

    = 1      singlet (Default)

    = 2,3,... doublet, triplet, and so on

ICHARG:    Molecular charge

    = 0  Neutral Molecule (Default)
    
IECP:      Effective Core Potentials 

    = 0    (Default) All electron calculation
    
    = 1    Read ECP potentials in the $ECP group

IEMOM:     Calculation of electrostatic moments

    = 1      calculate dipole moments (Default)

    = 2      also calculate quadrupole moments

    = 3      also calculate octopole moments

UNITS:     Distance units (Any angles must be in degrees)

    = ANGS   Angstroms (Default)

    = BOHR   Bohr atomic units

EVEC:      An array of the three x,y,z components of the applied electric field, in a.u. (1 a.u. = 1 Hartree/e*Bohr = 5.1422082(15)d+11 V/m)

    = 0.0D0  (Default)
    
DONTW:     Do not write 2e- integrals on the disk (Unit=1)

    = T      (Default)
    
ERITYP:    Typ of ERIs used in calculations

    = FULL   4c ERIs (Default)
    
    = RI     3c/2c ERIs for Resolution of the Identity (RI) App.
    
    = MIX    3c/2c ERIs for Resolution of the Identity (RI) App. once converged change to 4c ERIs (FULL)

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
^^^^^^^^

The &INPRUN namelist specifies the run type and other fundamental job options. These options are controlled by the following keywords:

RUNTYP:    Specifies the run calculation

The &INPHUB namelist specifies the options fot the Hubbard Model:

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

    = 1000   (DEFAULT)


Type of calculation
^^^^^^^^^^^^^^^^^^^

ICOEF:       Energy Optimization with respect to Coefficient Matrix (Natural Orbitals)

    = 0      Optimize only with respect to Gamma variables that determine the occupation numbers
                      
    = 1      Optimize with respect to Gammas and Coefficient matrix (DEFAULT)
                      
    = 2      Optimize only by the orbitals keeping fixed the occupation numbers
                      
    = 3      Optimize by all occupations and core-fragment orbitals. The rest of fragment orbitals remain frozen

IEINI:       Calculate only the initial energy

    = 0      (DEFAULT)

NO1:         MAX. index of NOs with Occupation equal to 1.0

    = -1     Consider Core NOs (DEFAULT)
                      
    = 0      All NOs are considered
                      
    = Value  User specifies how many NOs have OCC equal to 1.0


HARTREE-FOCK
^^^^^^^^^^^^

 RHF:        Restricted Hartree-Fock Calculation
 
    = T      (Default)

NCONVRHF:    RHF-SCF Density Convergence Criteria CONVRHFDM=10.0**(-NCONVRHF)

    = 5      (Default)
    
MAXITRHF:    Maximum number of RHF-SCF iterations

    = 100    (Default)
    
HFDAMP:      Damping of the Fock matrix

    = T      (Default)
    
HFEXTRAP:    Extrapolation of the Fock matrix

    = T      (Default)

HFID:        Use the Iterative Diagonalization Method to generate the HF Orbitals

    = F      (DEFAULT)

NTHRESHEID:  Convergence of the total energy, THRESHEID=10.0**(-NTHRESHEID)
                     
    = 6      (DEFAULT)

MAXITID:     Maximum number of external iterations
                     
    = 30     (DEFAULT)
                      
KOOPMANS:    Calculate IPs using Koopmans' Theorem

    = 0      (DEFAULT)

PNOF Selection
^^^^^^^^^^^^^^

IPNOF:       Type of Natural Orbital Functional (see section "NOF approximations")

    = 3      PNOF3 + pairing constraints

    = 4      PNOF4 + pairing constraints

    = 5      PNOF5
                      
    = 6      PNOF6
                      
    = 7      PNOF7 (DEFAULT)
    
    = 8      GNOF
                      
Ista:        Use Static version of PNOF7

    = 0      PNOF7 (DEFAULT)
                      
    = 1      PNOF7s
                      
HighSpin:    Spin-uncompensated calculation type

    = F      (DEFAULT) Multiple state (Ms=0)

    = T      High-spin uncompensated state (Ms=S)                      
                      
NCWO:        Number of coupled weakly occupied MOs per strongly occupied = Nc -> PNOFi(Nc)

    = 1      (DEFAULT)
                      
    = 2,3,...
                      
    =-1      NCWO = NVIR/NDOC where
             NVIR: Number of HF virtual MOs (OCC=0), 
             NDOC: Number of strongly occupied MOs

Convergence criteria in NOF calculation
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

For more info see section 3 in Comp. Phys. Comm. 259, 107651 (2021), Code Ocean Capsule; arXiv:2004.06142 [physics.comp-ph] by Piris and Mitxelena

NTHRESHL:    Convergence of the Lagrange multipliers, THRESHL=10.0**(-NTHRESHL)

    = 3      (DEFAULT)

NTHRESHE:    Convergence of the total energy, THRESHE=10.0**(-NTHRESHE)

    = 4      (DEFAULT)

NTHRESHEC:   Convergence of the total energy (ORBOPT), THRESHEC=10.0**(-NTHRESHEC)

    = 10     (DEFAULT)

NTHRESHEN:   Convergence of the total energy (OCCOPT), THRESHEN=10.0**(-NTHRESHEN)

    = 10     (DEFAULT)

Options for the orbital optimization program (ID method)
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

For more info and computational details see section 3 in arXiv:004.06142 [physics.chem-ph] by Piris and Mitxelena

MAXLOOP:     Maximum Iteration Number for the SCF ITERATION cycle in each ITCALL

    = 30     (DEFAULT)

    The straightforward iterative scheme fails to converge very often due to the values of some off-diagonal elements Fki. The latters must be suffciently small and of the same order of magnitude. A variable factor scales Fki. We establish an upper bound B, in such a way that when the absolute value of the matrix element Fki is greater than B, it is scaled by a factor Cki (F'ki = Cki*Fki ), as to satisfy ABS(Fki) <= B.

SCALING:     A variable factor scales Fki

    = T      (DEFAULT)

NZEROS:      B = 10.0**(1-NZEROS). Initial number of ZEROS in Fij. The scaling factor varies until the number of ZEROS (.000##) is equal for all elements Fij

    = 0      ; B = 10.0 (DEFAULT)

NZEROSm:     B = 10.0**(1-NZEROSm). Maximum number of zeros in Fij

    = 5      ; B = 10.0 (DEFAULT)

NZEROSr:     B = 10.0**(1-NZEROSr). Number of zeros in Fij to restart automatically the calculation

    = 2      ; B = 10.0 (DEFAULT)
                      
AUTOZEROS:   The code select automatically values for NZEROS, NZEROSm & NZEROSr. 

             Note: Override previously selected values
                   
    = T      (Default)

ITZITER:      Number of Iterations for constant scaling

    = 10     (DEFAULT)

DIIS:        Direct Inversion in the Iterative Subspace in the orbital optimization if DUMEL < THDIIS every NDIIS loops

    = T      (DEFAULT)

NTHDIIS:     Energy threshold to begin DIIS

    = 3      ; THDIIS = 10.0**(-NTHDIIS) (DEFAULT)

NDIIS:       Number of considered loops to interpolate the generalized Fock matrix in the DIIS

    = 5      (DEFAULT)

PERDIIS:     Periodic DIIS

    = T      ; Apply DIIS every NDIIS (DEFAULT)
                      
    = F      ; DIIS is always applied after NDIIS

Options for perturbative calculations
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

For more info see [PRA 98, 022504 (2018)]

OIMP2:       NOF - Orbital Invariant MP2

    = F       (DEFAULT)
                     
NO1PT2:      Frozen MOs in perturbative calculations. Maximum index of NOs with Occupation = 1

   = -1      = NO1 (DEFAULT)
                      
   = 0       ; All NOs are considered
                      
   = Value   User specifies how many NOs are frozen                   

SC2MCPT:     SC2-MCPT perturbation theory is used to correct the PNOF5 Energy. Two outputs: PNOF5-SC2-MCPT and PNOF5-PT2

    = F      (DEFAULT)

NEX:         Number of excluded coupled orbitals in the PNOF5-PT2 calculation

    = 0      ; All NOs are included (DEFAULT)


Restart options for GAMMA, C, diagonal F, and nuclear coordinates
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

RESTART:     Restart from GCF file (DEFAULT=F)

    = F      ; corresponds to INPUTGAMMA=0,INPUTC=0,INPUTFMIUG=0,INPUTCXYZ=0
                      
    = T      ; corresponds to INPUTGAMMA=1,INPUTC=1,INPUTFMIUG=1,INPUTCXYZ=1

INPUTGAMMA:   Guess for GAMMA variables (determine the Occupation Numbers)

    = 0      ; Close Fermi-Dirac Distribution (DEFAULT)
                      
    = 1      ; Input from GCF file

INPUTC:      Guess for coefficient matrix (Natural Orbitals)

     = 0     ; Use HCORE or HF Eigenvectors (DEFAULT)
                      
     = 1      ; Input from GCF file

INPUTFMIUG:   Guess for diagonal elements of the symmetric F matrix (FMIUG0)

     = 0      ; Use single diagonalization of Lagragian (DEFAULT)
                      
     = 1      ; Input from GCF file

INPUTCXYZ:    Read nuclear coordinates (Cxyz)

     = 0      ; From Input file
                      
     = 1      ; From GCF file
                      
Output options
^^^^^^^^^^^^^^

NPRINT:       Output option

      = 0     ; Short Printing (DEFAULT)
                      
      = 1     ; Output at initial and final iterations
                      
      = 2     ; Output everything at each iteration
      
IAIMPAC:       Write information into a WFN file (UNIT 7) for the AIMPAC program

      = 0      ; Not do it

      = 1      ; Do it (DEFAULT)
                      
IFCHK:         Write information into Formatted Checkpoint (FCHK) file for visualization software (UNIT 19)
 
      = 0      ; Don't write
                      
      = 1      ; Write into FCHK file (Default)
                      
MOLDEN:        Write information into MLD file for the MOLDEN PROGRAM (UNIT 17)

      = 0      ; Don't write

      = 1      ; Write into MLD file (Default)

NOUTRDM:       Print option for atomic RDMs

      = 0      ; Not do it (DEFAULT)

      = 1      ; Print atomic RDMs in 1DM and 2DM files

NTHRESHDM:     THRESHDM = 10.0**(-NTHRESHDM)

      = 6      (DEFAULT)

NSQT:          Print OPTION for 2DM file

      = 0      ; Formatted file

      = 1      ; Unformatted file (DEFAULT)

NOUTCJK:       Print option for CJ12 and CK12

      = 0      ; No output (DEFAULT)

      = 1      ; Print CJ12 and CK12 in file 'CJK'

NTHRESHCJK:    THRESHCJK = 10.0**(-NTHRESHCJK)

      = 6      (DEFAULT)

NOUTTijab:     Print option for Tijab

      = 0      ; No output (DEFAULT)

      = 1      ; Print Tijab in file 'Tijab'

NTHRESHTijab:   THRESHTijab=10.0**(-NTHRESHTijab)

      = 6      (DEFAULT)

APSG:           Open an APSG file for printing the coefficient matrix ($VEC-$END) and the expansion coefficients of the APSG generating wavefunction.

      = F      ; No output (DEFAULT)

NTHAPSG:        Threshold for APSG expansion coefficients THAPSG = 10.0**(-NTHAPSG)

      = 10     (DEFAULT)

Note: the following options require NPRINT > 0 to take effect      

IWRITEC:      Output option for the coefficient matrix

      = 0     ;  Not do it (DEFAULT)
                      
      = 1     ;  Do it

IMULPOP:       Mulliken population analysis

      = 0      ; Not do it (DEFAULT)
                      
      = 1      ; Do it

PRINTLAG:      Output option for the lagrange multipliers

      = F      ; Not do it (DEFAULT)

DIAGLAG:       Diagonalize Lagrange multipliers. Print new 1e- Energies, Canonical MOs, and new diagonal elements of the 1RDM

      = F      ; Not do it (DEFAULT)

IEKT:          Calculate the Ionization Potentials using the Extended Koopmans' Theorem (EKT)

      = 0      ; Not do it (DEFAULT)

      = 1      ; Do it

Options related to orthonormality of Natural Orbitals
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

ORTHO:         Orthogonalize the initial orbitals

      = F      ; No 
                      
      = T      ; Yes (DEFAULT)

CHKORTHO:       Check the orthonormality of the MOs

      = F      ; No (DEFAULT)
                      
      = T      ; Yes


Options related to frozen coordinates in geometry optimization
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

See also "Additional notes" section

FROZEN:         Is there any fixed coordinate

     = F      (DEFAULT)

IFROZEN:       By pairs, what coordinate of which atom, e.g. 2,5,1,1 means "y" coordinate of atom 5 and "x" coor of atom 1 to freeze. MAXIMUM of frozen coordinates = 10

      = 0      (DEFAULT)
                      
Options for optimization program
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

ICGMETHOD:     Define the conjugate gradient method in routines OCCOPTr, CALTijabIsym and OPTIMIZE

     = 1       ; Use SUMSL in CGOCUPSUMSLr,OPTSUMSL, SparseSymLinearSystem_CG (DEFAULT)

     = 2       ; Use NAG routines E04DGF in OPTCGNAG,CGOCUPNAGr; and F11JEF in SparseSymLinearSystem_NAG       

     = 3       ; Use LBFGS in OPTLBFGS, LBFGSOCUPr

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

Alternatively, we have also implemented the LBFGS algorithm written by J. Nocedal (see http://users.iems.northwestern.edu/~nocedal/lbfgs.html). This method is activated by setting ICGMETHOD = 3. In our experience, LBFGS works fine for occupation optimization, whereas it must be employed carefully for geometry optimization.

Finally, if you have the NAG library installed, you can use the corresponding subroutines to perform optimizations by setting ICGMETHOD = 2.

Geometry Optimization
^^^^^^^^^^^^^^^^^^^^^

If RUNTYP='OPTGEO' is set, DoNOF automatically sets RHF=F, HFID=F and OIMP2=F at the beginning of the calculation.

It is strongly recommended to set ICGMETHOD=1 (DEFAULT) or ICGMETHOD=2 if you possess the NAG library. In fact, the latter has proven to be much more accurate than LBFGS for this task. The LBFGS algorithm has been employed before in quantum chemistry programs to optimize the geometry (see http://openmopac.net/Manual/lbfgs.html). Since LBFGS employs very low memory it is recommended only if a large number of variables is to be optimized. Nevertheless, LBFGS may not work accurately if low-energy interactions are significant in your system.

RUNTYP='OPTGEO' may be a computationally demanding task for any ICGMETHOD option. Nevertheless, we have demonstrated (JCP 146, 014102 (2017)) that PNOF approximations produce similar equilibrium geometries for perfect pairing or larger coupling options (i.e. NCWO>1). Therefore, for RUNTYP='OPTGEO' is recommended to employ the minimum value of NCWO, that is, run a single-point calculation and check in the output how many weakly-occupied-orbitals have significant occupancies in each subspace. For example, if there are three weakly-occupied-orbitals with non-negligible occupations in each subspace, it will be enough to set NCWO=3 in the RUNTYP='OPTGEO' calculation. This can save a large amount of computational time and produce similar equilibrium geometries to those that would be obtained by considering all orbitals correlated with a large basis set.

GCF: All information required to restart any calculation is printed in a file called GCF during the iterative procedure. At the end of the calculation this file is renamed to "name-of-the-molecule.gcf" by our supplied run scripts. It is worth noting that at the end of the GCF the nuclear coordinates are printed. The latter are read at the beginning of the calculation (so the ones from the .inp file are ignored) only if explicitly required by the user, by setting INPUTCXYZ=1 or if RESTART=T in $NOFINP. This option is particularly useful if the calculation stops unexpectedly during the geometry optimization procedure (RUNTYP='OPTGEO'). If that is the case, run a new calculation setting INPUTCXYZ=1 to converge the energy from the last obtained geometry.

In geometry optimization calculations (RUNTYP='OPTGEO'), you will note that a file named CGGRAD is created during the calculation. Once the calculation ends it is renamed to "name-of-the-molecule.cgo" by our supplied run scripts. This file contains information about the geometry optimization procedure carried out by using the conjugate gradient method (set in the input file by ICGMETHOD), as well as the Hessian and harmonic vibrational frequencies at the solution point. Recall that the Hessian is computed by numerical differentiation of the analytic energy gradients (see details at I. Mitxelena et al. Adv Quant. Chem. ISSN 0065-3276 (2019)), so numerical precision of reported harmonic vibrational frequencies is limited and, apriori, they should be taken only qualitatively.

You may notice in the $NOFINP section that a keyword FROZEN is used to fix nuclear coordinates during geometry optimization. This is done in cartesians, though it is recommended, for obvious reasons, doing it by using internal coordinates. For the moment this has not been implemented in DoNOF yet. Therefore, we recommend the user to employ FROZEN carefully.

New algorithms and numerical methods for carrying out these optimizations are welcome, so we encourage new collaborations to work on this task.

Dependencies
^^^^^^^^^^^^

By setting ICGMETHOD=2 in the input file, DoNOF uses the Conjugate Gradient (CG) algorithm coded in NAG library for optimization of the GAMMA variables, as well as nuclear coordinates (if RUNTYP='OPTGEO'). If the user prefers to use NAG subroutines (https://www.nag.co.uk/content/nag-library), you must uncomment all lines in the code preceded by '!nag' and link DoNOF code with NAG library. Accordingly, the following routines are called by DoNOF: E04DGF, E04UEF, E04UCF, and F11JEF. The latter is required for perturbative calculations, while the other routines are required for optimization processes.

Dissociation
^^^^^^^^^^^^

Molecular dissociation is considered the main still unresolved problem of DFT, but of fundamental interest for quantum chemistry. PNOF methods are able to reproduce benchmark potential energy curves of molecular bond dissociation. Nevertheless, this calculation is tricky and must be carried out carefully. In fact, different solutions may arise during the dissociation process depending on the electron correlation present in your system. Computationally it is convenient to converge a single-point calculation, and then start the dissociation process manually by setting: RESTART=F INPUTGAMMA=1 INPUTC=1 INPUTFMIUG=1 ORTHO=T. The restart option allows to use the previous solution, however, we have to avoid reading nuclear geometry from previous point. Since RESTART=T automatically fixes INPUTCXYZ=1, we must employ RESTART=F and specify what we want to read from GCF file, e.g. occupations (INPUTGAMMA=1), orbital coefficients (INPUTC=1), and diagonal elements of pseudofockian (INPUTFMIUG=1).

Symmetry
^^^^^^^^

In DoNOF point-group symmetry is not employed, so C1 symmetry is assumed for any molecular system.

WFN file
^^^^^^^^

The WFN file contains the necessary info to study the output data by using external programs, such as AIMPAC. Note that in this WFN file the energy is referred to as "HF energy", but it really corresponds to the PNOF energy.

MLD file
^^^^^^^^

The MLD file contains the necessary info to study the output data by using the MOLDEN post processing program of molecular and electronic structure (https://www3.cmbi.umcn.nl/molden/)

Numerical Precision
^^^^^^^^^^^^^^^^^^^

You may notice that different numerical precision is shown for each quantity (orbitals, energy, occupancies, etc) in the output file. The latter is done according to the trustworthy precision inherent to NOF methods. On the contrary, for other purposes is more convenient to employ as much digits as possible.


