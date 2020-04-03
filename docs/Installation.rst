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

There is an example in the git repository too.
