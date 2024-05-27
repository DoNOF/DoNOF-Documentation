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

You can perform excited state calculations via the extended random phase approximation (ERPA) by using the 2RDM provided by the PNOF5, PNOF7 and GNOF functionals, with the advantage of having a ground state with static and dynamic electron correlation. The equations to solve are:

ERPA0:
$$
    \begin{pmatrix}
        A_{srqp} & B_{srqp}\\
        B_{rspq} & A_{rspq}
    \end{pmatrix}    
    \begin{pmatrix}
        X_{pq}\\
        Y_{pq}
    \end{pmatrix}    
    =
    \omega_\nu
    \begin{pmatrix}
        (n_s - n_r) & 0\\
        0 & -(n_s - n_r)
    \end{pmatrix}    
    \begin{pmatrix}
        X_{pq}\\
        Y_{pq}
    \end{pmatrix}
$$

ERPA1:
$$
    \begin{pmatrix}
        A_{srqp} & B_{srqp} & A_{srpp}\\
        B_{rspq} & A_{rspq} & B_{rspp}\\
        A_{rrpq} & B_{rrqp} & A_{rrpp}
    \end{pmatrix}    
    \begin{pmatrix}
        X_{pq}\\
        Y_{pq}\\
        Z_{p}
    \end{pmatrix}    
    =
    \omega_\nu
    \begin{pmatrix}
        (n_s - n_r) & 0 & 0\\
        0 & -(n_s - n_r) & 0 \\
        0 & 0 & 1
    \end{pmatrix}    
    \begin{pmatrix}
        X_{pq}\\
        Y_{pq}\\
        Z_{p}
    \end{pmatrix}
$$
