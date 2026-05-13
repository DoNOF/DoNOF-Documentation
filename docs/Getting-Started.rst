Getting Started
===============

All PNOF options have default values (see "Input Options" section),
so for a given system defined in the $INPRUN part of the input,
it only remains necessary to put::

    &NOFINP /

An input for single-point energy calculation of Hydrogen atom with minimal basis set reads as::

   &INPRUN RUNTYP='ENERGY' MULT=1 ICHARG=0 /
   $DATA
   H atom: STO-2G basis set calculation
   
   H  1.0  0.00 0.00 0.00
   S   2
     1         1.309756377       0.4301284983
     2         0.2331359749      0.6789135305

   $END
   &NOFINP /
   
or even simpler if the file containing the basis set (basis-name.bas) is in the directory where the calculation is performed ($PWD), in $HOME/DoNOFsw/basis/, $HOME/DoNOF/basis/ directories, or if you indicate the site where it is located, that is, PATH/basis-name.bas. In that case an input for single-point energy calculation of Hydrogen atom with sto-2g.bas basis-set file reads as::
   
   &INPRUN RUNTYP='ENERGY' MULT=1 ICHARG=0 /
   $DATA
   H atom: STO-2G basis set calculation
   sto-2g
   H  1.0  0.00 0.00 0.00
   $END
   &NOFINP /

In each calculation many files are generated. Imagine the previous input corresponds to hydrogen.inp,
then we will obtain after a single-point calculation:

hydrogen.out --> file containing general output data corresponding to the NOF calculation

hydrogen.gcf --> file containing info needed to restart any calculation from the output of this one

hydrogen.wfn --> file containing wave-function info for AIMPAC program, among others.

Running script
^^^^^^^^^^^^^^

In the DoNOF GitHub repository you can find the scripts we usually use to run the program.

A common usage pattern is::

    ./run_donofg filename
    ./run_donofompg filename
    ./run_donofmpig filename

For molecular dynamics jobs::

    ./run_donofg_dyn filename
    ./run_donofompg_dyn filename
    ./run_donofmpig_dyn filename

The wrappers handle the standard output and restart files (for example ``filename.out`` and
``filename.gcf``).
