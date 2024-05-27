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

You can perform excited state calculations via the extended random phase approximation (ERPA) by using the 2RDM provided by the PNOF5, PNOF7 and GNOF functionals, with the advantage of having a ground state with static and dynamic electron correlation. The ERPA equations comes from solving the Rowe equation:

$$
    \bra{\psi_0}[\delta \mathcal{O}_\nu,[\hat{H},\mathcal{O}_\nu^\dagger]]\ket{\psi_0} = \omega_\nu \bra{\psi_0}[\delta \mathcal{O}_\nu,\mathcal{O}_\nu^\dagger]\ket{\psi_0}
$$
with a given excitation operator.

ERPA0:

The excitation operator is given by

$$
 \mathcal{O}^\dagger = \sum_{p>q}^{N/2} X_{pq} (a_{p_{\alpha}}^\dagger a_{q_{\alpha}} + a_{p_{\beta}}^\dagger a_{q_{\beta}})
+ \sum_{p>q}^{N/2} Y_{pq} (a_{q_{\alpha}}^\dagger a_{p_{\alpha}} + a_{q_{\beta}}^\dagger a_{p_{\beta}})
$$

and the equation to solve is

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

The excitation operator is given by

$$
 \mathcal{O}^\dagger = \sum_{p>q}^{N/2} X_{pq} (a_{p_{\alpha}}^\dagger a_{q_{\alpha}} + a_{p_{\beta}}^\dagger a_{q_{\beta}})
+ \sum_{p>q}^{N/2} Y_{pq} (a_{q_{\alpha}}^\dagger a_{p_{\alpha}} + a_{q_{\beta}}^\dagger a_{p_{\beta}})\\
+ \sum_{p}^{N/2} Z_{p} (a_{p_{\alpha}}^\dagger a_{p_{\alpha}} + a_{p_{\beta}}^\dagger a_{p_{\beta}})
$$

and the equation to solve is

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
        0 & 0 & 0
    \end{pmatrix}    
    \begin{pmatrix}
        X_{pq}\\
        Y_{pq}\\
        Z_{p}
    \end{pmatrix}
$$

ERPA2:

The excitation operator is given by

$$
 \mathcal{O}^\dagger = \sum_{p>q}^{N/2} X_{pq} (a_{p_{\alpha}}^\dagger a_{q_{\alpha}} + a_{p_{\beta}}^\dagger a_{q_{\beta}})
+ \sum_{p>q}^{N/2} Y_{pq} (a_{q_{\alpha}}^\dagger a_{p_{\alpha}} + a_{q_{\beta}}^\dagger a_{p_{\beta}})\\
+ \sum_{p}^{N/2} Z_{p} (a_{p_{\alpha}}^\dagger a_{p_{\alpha}} + a_{p_{\beta}}^\dagger a_{p_{\beta}}) \\
+ \sum_{pq}^{N/2} D_{pq} a_{p_{\beta}}^\dagger a_{q_{\beta}} a_{p_{\alpha}}^\dagger a_{q_{\alpha}}
$$

and the equation to solve is

$$
    \begin{pmatrix}
        A_{srqp} & B_{srqp} & \left(\frac{c_s}{2c_p(c_r+c_s)}\right) A_{srpp}\\
        B_{rspq} & A_{rspq} & \left(\frac{c_r}{2c_p(c_r+c_s)}\right) B_{rspp}\\
        \left(\frac{1}{c_r}\right)A_{rrpq} & \left(\frac{1}{c_r}\right)B_{rrqp} & \left(\frac{1}{4c_p c_r}\right)A_{rrpp}
    \end{pmatrix}    
    \begin{pmatrix}
        X_{pq}\\
        Y_{pq}\\
        V_{p}
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
        V_{p}
    \end{pmatrix}
$$

with $A_{rspq}=B_{rsqp}$ given by
$$
    A_{rspq} &=& h_{sq} \delta_{pr} (n_p - n_s) + h_{pr} \delta_{sq} (n_q - n_r) \\
    &+& \sum_{tu} (\braket{qt}{su} - \braket{qt}{us}) \mathrm{D}_{ptru}^{\alpha\alpha\alpha\alpha}
    + \sum_{tu} (\braket{pt}{ru} - \braket{pt}{ur}) \mathrm{D}_{qtsu}^{\alpha\alpha\alpha\alpha} \\
    &+& \sum_{tu} \braket{qt}{su} \mathrm{D}_{ptru}^{\alpha\beta\alpha\beta} + \sum_{tu} \braket{qt}{us} \mathrm{D}_{ptur}^{\alpha\beta\alpha\beta}
    + \sum_{tu} \braket{pt}{ru} \mathrm{D}_{qtsu}^{\alpha\beta\alpha\beta} + \sum_{tu} \braket{pt}{ur} \mathrm{D}_{qtus}^{\alpha\beta\alpha\beta} \\
    &+& \sum_{tu} \braket{ps}{ut}\mathrm{D}_{qrtu}^{\alpha\alpha\alpha\alpha} - \sum_{tu} \braket{ps}{tu}\mathrm{D}_{qrtu}^{\alpha\beta\alpha\beta}
    + \sum_{tu} \braket{qr}{ut}\mathrm{D}_{pstu}^{\alpha\alpha\alpha\alpha} - \sum_{tu} \braket{qr}{tu}\mathrm{D}_{pstu}^{\alpha\beta\alpha\beta} \\
    &+& \delta_{qs} \sum_{tuv} \braket{pt}{vu}\mathrm{D}_{rtuv}^{\alpha\alpha\alpha\alpha} - \delta_{qs} \sum_{tuv} \braket{pt}{uv}\mathrm{D}_{rtuv}^{\alpha\beta\alpha\beta} \\
    &+& \delta_{pr} \sum_{tuv} \braket{qt}{vu}\mathrm{D}_{stuv}^{\alpha\alpha\alpha\alpha} - \delta_{pr} \sum_{tuv} \braket{qt}{uv}\mathrm{D}_{stuv}^{\alpha\beta\alpha\beta}
$$

and

$$
c_p = \pm \sqrt{n_p}
$$

under the PNOF convention of a `+\sqrt{n_p}` for strongly occupied orbitals and `-\sqrt{n_p}` for weakly occupied orbitals.
