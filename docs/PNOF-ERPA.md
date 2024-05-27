# Excited States

```{margin} Article
[`J. Chem. Theory Comput. 20(5), 2140–2151 (2024).`](https://doi.org/10.1021/acs.jctc.3c01194)
```

## Input

You can run an excited state calculation using the `ERPA='T'` in the `&NOFINP` as in the following example:

:::{admonition} Example Input
~~~
 &INPRUN RUNTYP='ENERGY' MULT=1 ICHARG=0 ERITYP='RI' /
 $DATA
 Hydrogen Molecule (H2)
 cc-pVDZ
H  1.0  0.0000     0.0000    0.0000
H  1.0  0.0000     0.0000    0.7414
 $END
 &NOFINP IPNOF=8 IORBOPT=4 ERPA="T"/
~~~
:::
