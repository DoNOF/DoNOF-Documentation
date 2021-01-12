#########################
Download and Installation
#########################

DoNOF is open-source, so you can download the single source file from GitHub: https://github.com/DoNOF

In the following, we describe in detail the procedure to install DoNOF in your computer. First download the source file (donof.f90) from GitHub, or simply clone this repository in your computer. Then, enter the new directory and type "make" to create the executables for DoNOF. Intel and GNU Fortran compilers can be used to create a serial and mpi executables.

The program depends on the lapack library so you must also download the 'lapack.f' file from our repository. If you already have this library installed on your computer and prefer to use it, you don't need the 'lapack.f' file, but you do need to incorporate the necessary options into the Makefile for a successful DoNOF build.

An example our simple Makefile is given below::

###############################################################################################
#                      Makefile for DoNOF program (Date: January 2021)                        #
###############################################################################################

SFLAGS  = -i8 -r8 -fpp -O2 

# You can use -O3 with recent versions of the Intel Fortran compiler

F90     = ifort          $(SFLAGS)

MPIF90  = mpiifort -DMPI $(SFLAGS)

#

SFLAGSg = -fdefault-integer-8 -fdefault-real-8 -fdefault-double-8 -cpp -ffpe-summary=none -O3

F90g    = gfortran     $(SFLAGSg) 

MPIF90g = mpif90 -DMPI $(SFLAGSg)

#

###############################################################################################

all: serial mpi serialg mpig

#########################################################################

serial:
	$(F90) -o DoNOF.x donof.f90 lapack.f

mpi:
	$(MPIF90) -o DoNOFmpi.x donof.f90 lapack.f
	
serialg:
	$(F90g) -o DoNOFg.x donof.f90 lapack.f
	
mpig:
	$(MPIF90g) -o DoNOFmpig.x donof.f90 lapack.f
	

#########################################################################

