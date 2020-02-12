Input Options
=====
The simplest input.::

    $nofinp

The &INPRUN namelist specifies the run type, use of core potentials,
the atomic basis, and similar fundamental job options. These options
are controlled by the following keywords:

RUNTYP:  specifies the run calculation

    ENERGY   1) single-point energy calculation (Default)

    GRAD     2) energy + gradients with respect to nuclear coord.

    OPTGEO   3) optimize the molecular geometry
    
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

UNITS:     Distance units (Any angles must be in degrees)

    = ANGS   Angstroms (Default)

    = BOHR   Bohr atomic units

EVEC:     An array of the three x,y,z components of the applied electric field, in a.u. (1 a.u. = 1 Hartree/e*bohr = 5.1422082(15)d+11 V/m)

    = ZERO   (Default)

DONTW:    Do not write 2e- integrals on the disk (Unit=1)

    = F   (Default)
    
    = T
    
    
The &NOFINP namelist specifies the type of PNOF calculation, options
for the iterative diagonalization method, perturbative corrections,
input and output, and similar fundamental job options. These options
are controlled by the following keywords:
    

Examples
^^^^

Single-point

Hartree-Fock

Geometry Optimization

Convergence

