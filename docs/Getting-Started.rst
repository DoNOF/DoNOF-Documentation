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

You can found in DoNOF GitHub repository the scripts we usually employ to run the program, inluding those necessary after INTEL or GCC compilation.

A very simple serial running script may read as::

    #!/bin/csh -f

    if (-f $1.gcf) mv -f $1.gcf GCF

    if (-f $1.fra) mv -f $1.fra FRAG

    nice +18 $PATH-TO-EXECUTABLE/donof.x < $1.inp > $1.out
    
    if (-f FCHK) mv -f FCHK $1.fchk

    if (-f MLD)then
     cp -f MLD $1.mld
     if (-f XYZ)then
      cat MLD XYZ > $1.mld
      rm -f XYZ
     endif
     rm -f MLD
    endif

    if (-f WFN) mv -f WFN $1.wfn

    if (-f APSG) mv -f APSG $1.pun

    if (-f 1DM) mv -f 1DM $1.1dm

    if (-f fort.14) mv -f fort.14 $1.1dm

    if (-f 2DM) mv -f 2DM $1.2dm

    if (-f fort.15) mv -f fort.15 $1.2dm

    if (-f N2DM) mv -f N2DM $1.n2dm

    if (-f CJK) mv -f CJK $1.cjk

    if (-f CND) mv -f CND $1.cnd

    if (-f Tijab) mv -f Tijab $1.2mp

    if (-f FRAG) mv -f FRAG $1.fra

    if(-f GCFe)then
     mv -f GCFe $1.gcf
     rm -f GCF
    else if(-f GCF)then
     mv -f GCF $1.gcf
    endif

    if (-f CGGRAD) mv -f CGGRAD $1.cgo

    if (-f CGM) rm -f CGM

    if (-f BFST) rm -f BFST

    if (-f fort.1) rm -f fort.1



