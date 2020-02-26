Input Options
=====
The simplest input.::

    $nofinp

The &INPRUN namelist specifies the run type, use of core potentials,
the atomic basis, and similar fundamental job options. These options
are controlled by the following keywords:

RUNTYP  specifies the run calculation

     ENERGY  1) single-point energy calculation (Default)

     GRAD   2) energy + gradients with respect to nuclear coord.

     OPTGEO 3) optimize the molecular geometry
    


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

