# Geometry Optimization

You can run a single point energy calculation using the `RUNTYP='OPTGEO'` in the `&INPRUN` as in the following example:

:::{admonition} Example Input
~~~
 &INPRUN RUNTYP='OPTGEO' MULT=1 ICHARG=0/
 $DATA
 Water (H2O)
 cc-pVDZ
O  8.0  0.0000     0.0000    0.1173
H  1.0  0.0000     0.7572   -0.4692
H  1.0  0.0000    -0.7572   -0.4692
 $END
 &NOFINP IPNOF=8 /
~~~
:::
