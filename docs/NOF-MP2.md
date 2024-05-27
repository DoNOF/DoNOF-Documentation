# NOF-MP2

```{margin} Article
[`Phys. Rev. Lett. 119(6), 063002 (2017).`](https://doi.org/10.1103/PhysRevLett.119.063002)

[`Phys. Rev. A 98(2), 022504 (2018).`](https://doi.org/10.1103/PhysRevA.98.022504)

[`Phys. Rev. A 100(3), 032508 (2019).`](https://doi.org/10.1103/PhysRevA.100.032508)
```

In order to activate the NOF-MP2 calculation in DoNOF, set (in the input file):

~~~
    $NOFINP OIMP2=T IPNOF=7 Ista=1 /
~~~

Note that static PNOF7 (PNOF7s) is the best option to carry out NOF-MP2 calculations. 
The latter is specified by the Ista=1 keyword in the input file. 
Nevertheless, you can use PNOF7 or other functional to generate the reference orbitals.

Current NOFs based on electron pairing take into account most of the
non-dynamical effects, and also an important part of the dynamical
electron correlation corresponding to the intrapair interactions.
Consequently, electron-pairing-based NOFs produce
results that are in good agreement with accurate wavefunction-based
methods for small systems, where electron correlation effects are
almost entirely intrapair. When the number of pairs increases, NOF
values deteriorate especially in those regions where dynamic correlation
prevails. It is therefore mandatory to add the inter-pair dynamic
electron correlation to improve calculations.

The second-order Møller--Plesset (MP2) perturbation theory is the
simplest way of properly incorporating dynamic correlation effects.
In DoNOF, the recently proposed NOF-MP2 method can be used to obtain a good balance
of both static (non-dynamic) and dynamic electron correlation. The
zeroth-order Hamiltonian is constructed from a closed-shell-like Fock
operator that contains a HF density matrix with doubly
and singly occupied orbitals. The electronic energy
is then calculated by the expression

$$
    E=\tilde{E}_{hf}+E^{corr}=\tilde{E}_{hf}+E^{sta}+E^{dyn}
$$

$$
    \tilde{E}_{hf}=2\sum\limits _{g=1}^{\mathrm{N}_{\Omega}}\mathcal{H}_{gg}+\sum_{f,g=1}^{\mathrm{N}_{\Omega}}\left(2\mathcal{J}_{fg}-\mathcal{K}_{fg}\right)-\sum_{g=\frac{\mathrm{N_{II}}}{2}+1}^{\mathrm{N}_{\Omega}}\frac{\mathcal{J}_{gg}}{4}
$$

$$
    \begin{array}{c}E^{sta}=\sum\limits _{g=1}^{\mathrm{N_{II}/2}}\sum\limits _{q\neq p}\sqrt{\Lambda_{q}\Lambda_{p}}\,\Pi_{qp}\mathcal{\,K}_{pq}-4\sum\limits _{f\neq g}^{\mathrm{\mathrm{N}_{\Omega}}}\sum\limits _{p\in\Omega_{f}}\sum\limits _{q\in\Omega_{g}}\Phi_{q}^{2}\Phi_{p}^{2}\mathcal{K}_{pq}\end{array}
$$

$$
    E^{dyn}=\sum\limits _{g,f=1}^{\mathrm{\mathrm{N}_{\Omega}}}\;\sum\limits _{p,q>\mathrm{N}_{\Omega}}^{\mathrm{N}_{B}}A_{g}A_{f}\left\langle gf\right|\left.pq\right\rangle \left[2T_{pq}^{gf}\right.\left.-T_{pq}^{fg}\right]
$$
    
$$
    A_{g}=\left\{ \begin{array}{c}1\,,\quad1\leq g\leq\frac{\mathrm{N_{II}}}{2}\qquad\\\frac{\mathrm{1}}{2},\:\frac{\mathrm{N_{II}}}{2}<g\leq\mathrm{N}_{\Omega}\end{array}\right.
$$
