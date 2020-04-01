Getting Started
=====
The simplest input.::

    $nofinp

generates files like input.out input.gcf

Running script
^^^^^^^^^^^^^^

You can found in DoNOF GitHub repository the scripts we usually employ to run the program.

However, a very simple serial running script could be.::

    #!/bin/csh -f

    if (-f $1.gcf) mv -f $1.gcf GCF

    if (-f $1.fra) mv -f $1.fra FRAG

    nice +18 ~/Programs/DoNOF/DoNOF/exe/donof.x < $1.inp > $1.out

    if (-f WFN) mv -f WFN $1.wfn

    if (-f APSG) mv -f APSG $1.pun

    if (-f 1DM) mv -f 1DM $1.1dm

    if (-f 2DM) mv -f 2DM $1.2dm

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

    if (-f BFST) rm -f BFST

    if (-f fort.1) rm -f fort.1



