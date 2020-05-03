#########################
Download and Installation
#########################

DoNOF is open-source, so you can download the source files from GitHub: https://github.com/DoNOF. For trial or simple purposes, an executable of DoNOF can be also download from GitHub. The specific machine and compiler used to generate the latter are specified in the repo.

In the following, we describe in detail the procedure to install DoNOF in your computer. First download the source files from GitHub, or simply clone this repository in your computer. Then, enter the new directory and type "make" to create the executables for DoNOF. If you do not have INTEL compilers, type 'make serialg' in order to create a serial executable with gfortran.

An example our simple makefile is given below::

    ########################################################################
    # Makefile for DoNOF program (Date: April 2020)
    ########################################################################
    
    # Intel Fortran
    F90 = ifort -i8 -r8 -fpp -static -Ofast
    MPIF90 = mpiifort -DMPI -r8 -i8 -fpp -Ofast

    # GNU Fortran
    SFLAGS = -fdefault-integer-8 -fdefault-real-8 -cpp -O3 -ffpe-summary=none
    F90g = gfortran $(SFLAGS)
    
    ########################################################################

    all: serial mpi serialg

    ########################################################################

    serial:

        $(F90) -o donof.x donof1.f donof2.f90 

    ########################################################################

    mpi:

        $(MPIF90) -o donofmpi.x donof1.f donof2.f90

    ########################################################################

    serialg:

        $(F90g) -o donofgnu.x donof1.f donof2.f90 

    ########################################################################


Note that we are using an INTEL compiler, which can be found in the official webpage https://software.intel.com. If we restrict to the GNU Fortran compiler, DoNOF can be used only in serial after compilation with gfortran. In our experience, DoNOF works much better with INTEL, so we strongly recommend the latter in order to improve the performance of DoNOF.

In the near future, we would like to open the possibility to use GCC in order to compile DoNOF for parallel execution, so any collaboration to make this real will be appreciated.
