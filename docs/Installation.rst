#########################
Download and Installation
#########################

DoNOF is open-source, so you can download the source files from GitHub: https://github.com/imitxelena003/DoNOF. For trial or simple purposes, an executable of DoNOF can be also download from GitHub.

In the following, we describe in detail the procedure to install DoNOF in your computer. First download the source files from GitHub, or simply clone this repository in your computer. Then, create the next directories:

sources --> It should contain all source files, as well as the makefile

objects --> It should contain two subdirectories, named 'serial' and 'mpi'

exe --> It will contain the executable files created after the compilation

Also, it is convenient (but not mandatory) to create the next directories:

examples --> It sould contain examples of DoNOF calculations

backup --> It will contain the backups of DoNOF

scripts --> It should contain scripts to run DoNOF in serial and in many cores

doc --> It should contain documentation for DoNOF, indeed you can generate a PDF file from this webpage to dowload and save in this directory

An example of a simple makefile is given below.::

    ########################################################################
    # Makefile for DoNOF program (Date: March 2020)
    ########################################################################
    PROG=$(HOME)/DoNOF/github/DoNOF
    SOU=$(PROG)/sources
    OBJ1=$(PROG)/objects/serial
    OBJ2=$(PROG)/objects/mpi
    EXC=$(PROG)/exe
    BACKUP=$(PROG)/backup
    SCR=$(PROG)/scripts
    EXAMP=$(PROG)/examples
    DOC=$(PROG)/doc/
    Cln=/bin/rm -rf
    #
    SFLAGSO0 = -i8 -r8 -fpp -static -O0
    SFLAGSw  = -i8 -r8 -fpp -static -O0 -warn all,nodeclarations
    SFLAGSb  = -i8 -r8 -fpp -static -O0 -CB
    SFLAGSO3 = -i8 -r8 -fpp -static -O3
    SFLAGSO4 = -i8 -r8 -fpp -static -Ofast
    F90      = ifort $(SFLAGSO0)
    #
    PFLAGSO0 = -DMPI -i8 -r8 -fpp -O0
    PFLAGSw  = -DMPI -i8 -r8 -fpp -Ofast -warn all,nodeclarations
    PFLAGSb  = -DMPI -i8 -r8 -fpp -Ofast -CB
    PFLAGSO3 = -DMPI -i8 -r8 -fpp -O3
    PFLAGSO4 = -DMPI -i8 -r8 -fpp -Ofast
    MPIF90   = mpiifort $(PFLAGSO0)
    #
    ########################################################################

    all: serial mpi

    ########################################################################

    serial:
            cd $(OBJ1)&& $(Cln) *.o *genmod*
        
            cd $(SOU) && $(F90) -c donof1.f donof2.f90 
                
            cd $(SOU) && $(F90) -o donof.x donof1.o donof2.o 
        
    # move exe and object files
        
            mv $(SOU)/donof.x  $(EXC)/donof.x
        
            make mvfiles1
    # clean
            cd $(SOU) && $(Cln) *genmod*

    ########################################################################

    mpi:

            cd $(OBJ2)&& $(Cln) *.o *genmod*
        
            cd $(SOU) && $(MPIF90) -c donof1.f donof2.f90
        
            cd $(SOU) && $(MPIF90) -o donofmpi.x donof1.o donof2.o
        
    # move exe and object files
        
            mv $(SOU)/donofmpi.x  $(EXC)/donofmpi.x
        
            make mvfiles2
        
    # clean
            cd $(SOU) && $(Cln) *genmod*
    #
    mvfiles1:
            mv $(SOU)/donof1.o      $(OBJ1)/donof1.o
            mv $(SOU)/donof2.o      $(OBJ1)/donof2.o
    #
    mvfiles2:
            mv $(SOU)/donof1.o      $(OBJ2)/donof1.o
            mv $(SOU)/donof2.o      $(OBJ2)/donof2.o
        
    ###############################################################################
    #
    tar:    
            cd $(BACKUP)/ && tar -zPcvf DoNOF_2020.03.tar.gz               \
                                        $(SOU) $(DOC) $(EXAMP) $(SCR)
    #
    ###############################################################################


There is an example in the git repository too. Note that we are using an INTEL compiler, which can be found in the official webpage https://software.intel.com

In the near future, we'd like to open the possibility to use GCC, the GNU compiler collection, so any collaboration to make this real will be appreciated.
