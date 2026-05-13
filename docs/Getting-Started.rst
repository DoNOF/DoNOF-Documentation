Getting Started
=====

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

Current DoNOFsw repositories already include the standard run wrappers. If your input is
``filename.inp``, use::

    ./run_donofg filename
    ./run_donofompg filename
    ./run_donofmpig filename

For molecular dynamics jobs, use::

    ./run_donofg_dyn filename
    ./run_donofompg_dyn filename
    ./run_donofmpig_dyn filename

The wrappers handle usual file naming for output and restart files (for example ``.out`` and
``.gcf``).

Local documentation preview
^^^^^^^^^^^^^^^^^^^^^^^^^^^

In the documentation repository, a helper script is provided to rebuild and preview docs locally::

    ./preview_docs_local.sh

Then open::

    http://127.0.0.1:8000/intro.html


