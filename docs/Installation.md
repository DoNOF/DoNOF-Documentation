# Download and Installation

DoNOF is open-source, so you can download the single source file from GitHub: https://github.com/DoNOF/DoNOFsw/

In the following, we describe in detail the procedure to install DoNOF in your computer. First download the source file (donof.f90) from GitHub, or simply clone this repository in your computer. Then, enter the new directory and type "make" to create the executables for DoNOF. Intel and GNU Fortran compilers can be used to create a serial and mpi executables.

The program depends on the lapack library so you must also download the 'lapack.f' file from our repository. If you already have this library installed on your computer and prefer to use it, you don't need the 'lapack.f' file, but you do need to incorporate the necessary options into the Makefile for a successful DoNOF build.

## Installation

**Requisites.** You need a FORTRAN compiler, either gfortran or ifort. Optionally, you may want to install OpenMPI for parallel execution.

1. Clone the code with
~~~
git clone https://github.com/DoNOF/DoNOFsw
~~~

2. Go inside the DoNOFsw folder (`cd DoNOFsw`) and compile with `make [option]`. For example:
~~~
make serialg # gfortran serial -> /exe/DoNOFg.x
~~~

Other options are:
~~~
make mpig    # gfortran mpi    -> /exe/DoNOFmpig.x
make mping   # gfortran mpi (for recent linux versions)
make serial  # ifort serial    -> /exe/DoNOF.x
make mpi     # ifort mpi       -> /exe/DoNOFmpi.x
~~~

3. The executable will be placed inside /exe

## Execution

Several input files can be found inside /examples. A basic single point calculation with the GNOF functional looks like the following:
~~~
 &INPRUN RUNTYP='ENERGY' MULT=1 ICHARG=0 ERITYP='FULL' /
 $DATA
 Water (H2O)
 cc-pVDZ
O  8.0  0.0000     0.0000    0.1173
H  1.0  0.0000     0.7572   -0.4692
H  1.0  0.0000    -0.7572   -0.4692
 $END
 &NOFINP IPNOF=8 /
~~~

If the input is placed in a file called filename.inp, it can be executed with
~~~
./run_donofg filename     # gfortran serial
~~~
the output will be placed in filename.out.

Other options for execution are:
~~~
./run_donofmpig filename  # gfortran mpi
./run_donof     filename  # ifort serial
./run_donofmpi  filename  # ifort mpi
~~~

## Capabilities

The &INPRUN and &NOFINP namelists specify the input and output, and the fundamental job options.

The functional is controlled through **IPNOF=N** in &NOFINP, with N the number of the functional. For example, INPOF=7 indicates to use PNOF7. GNOF is indicated with IPNOF=8.

Current capabilities include:
- **RUNTYP = ENERGY** - Single-point Energy (Default)
- **RUNTYP = GRAD** - Energy + Gradients with respect to nuclear coord
- **RUNTYP = OPTGEO** - Geometry Optimization
- **RUNTYP = HESS** - Numerical Hessian
- **RUNTYP = DYN** - Born-Oppenheimer on-the-fly molecular dynamics

Other common options include excited states calculation (**ERPA=T**) and NOF-MBPT calculations (**MBPT=T**).
