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

You can perform excited state calculations via the extended random phase approximation (ERPA) by using the 2RDM provided by the PNOF5, PNOF7 and GNOF functionals, with the advantage of having a ground state with static and dynamic electron correlation. The equation to solve corresponds to:

\begin{multline}
    \begin{pmatrix}
        A_{srqp} & B_{srqp} & \color{Blue} \color{OliveGreen}\left(\frac{c_s}{2c_p(c_r+c_s)}\right) \color{Blue}A_{srpp}\\
        B_{rspq} & A_{rspq} & \color{OliveGreen}\left(\frac{c_r}{2c_p(c_r+c_s)}\right)\color{Blue}B_{rspp}\\
        \color{OliveGreen}\left(\frac{1}{c_r}\right)\color{Blue}A_{rrpq} & \color{OliveGreen}\left(\frac{1}{c_r}\right)\color{Blue}B_{rrqp} & \color{OliveGreen}\left(\frac{1}{4c_p c_r}\right)\color{Blue}A_{rrpp}
    \end{pmatrix}    
    \begin{pmatrix}
        X_{pq}\\
        Y_{pq}\\
        \color{Blue}Z_{p}\color{black}{|}\color{OliveGreen}V_{p}
    \end{pmatrix}    
    \\=
    {\boldsymbol{\omega}}_{\boldsymbol{\nu}}
    \begin{pmatrix}
        (n_s - n_r) & 0 & \color{Blue}0\\
        0 & -(n_s - n_r) & \color{Blue}0 \\
        \color{Blue}0 & \color{Blue}0 & \color{Blue}{0}\color{black}{|}\color{OliveGreen}{1}
    \end{pmatrix}    
    \begin{pmatrix}
        X_{pq}\\
        Y_{pq}\\
        \color{Blue}Z_{p}\color{black}{|}\color{OliveGreen}V_{p}
    \end{pmatrix} \nonumber
\end{multline}
