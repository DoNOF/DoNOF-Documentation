#########################################
Electron-pairing-based NOF for Multiplets
#########################################

The non-relativistic electronic energy can be written as an explicit functional of the 1- and 2-order reduced density matrices (RDM)

.. math::

    E_{el}[\Gamma,D]=\sum_{ik}\Gamma_{ki}h_{ki}+\sum_{ijkl}D_{kl,ij}\langle kl|ij\rangle
    
where

.. math::

    \Gamma_{ki}={\displaystyle \dfrac{1}{2S+1}{\textstyle {\displaystyle \sum_{M_{s}=-S}^{S}}}}\left\langle SM_{s}\right|\hat{a}_{k}^{\dagger}\hat{a}_{i}\left|SM_{s}\right\rangle

.. math::

    D_{kl,ij}={\displaystyle {\textstyle {\displaystyle \dfrac{1}{2\left(2S+1\right)}\sum_{M_{s}=-S}^{S}}}}\left\langle SM_{s}\right|\hat{a}_{k}^{\dagger}\hat{a}_{l}^{\dagger}\hat{a}_{j}\hat{a}_{i}\left|SM_{s}\right\rangle
    
In practical applications of NOFT we approximate the 2RDM in terms of the natural occupation numbers

.. math::

    E_{el}[\left\{ n_{i},\phi_{i}\right\}]=\sum\limits _{i}n_{i}\mathcal{H}_{ii}+\sum\limits _{ijkl}D[n_{i},n_{j},n_{k},n_{l}]\left\langle kl|ij\right\rangle

In our electron-pair-based NOF the orbital space is divided into disjoint orbital subspaces. See details at PRA 100, 032508 (2019). Then the energy can be written as

.. math::

    E=\sum\limits _{g=1}^{\frac{\mathrm{N_{II}}}{2}}E_{g}+\sum_{g=\frac{\mathrm{N_{II}}}{2}+1}^{\mathrm{N}_{\Omega}}\mathcal{H}_{gg}+\sum\limits _{f,g=1;f\neq g}^{\mathrm{N}_{\Omega}}E_{fg}

.. math::

    E_{g}=2\sum\limits _{p\in\Omega_{g}}n_{p}\mathcal{H}_{pp}+\sum\limits _{q,p\in\Omega_{g}}\Pi_{qp}\mathcal{K}_{pq}\,,\;\Omega{}_{g}\in\Omega_{\mathrm{II}}

.. math::

    E_{fg}=\sum\limits _{p\in\Omega_{f}}\sum\limits _{q\in\Omega_{g}}\left[n_{q}n_{p}\left(2\mathcal{J}_{pq}-\mathcal{K}_{pq}\right)-\Phi_{q}\Phi_{p}\mathcal{K}_{pq}\right]

DoNOF contains three approximations that give up to the NOFs named as PNOF5, PNOF7, and PNOF6 (in the input file we choose one or another by setting ICOEF=5, ICOEF=7, and ICOEF=6, respectively). For more info see the refs. cited for each approximation.

PNOF5
-----

(JCP 134, 164102 (2011))

PNOF5 is an independent-pair model. It is a pure N-representable NOF, since it corresponds to an APSG wavefunction with fixed phases (see JCP 139, 234109 (2013)).

.. math::

    E_{el}^{pnof5}={\displaystyle \sum\limits _{g=1}^{\mathrm{N}/2} E_{g}}+{\displaystyle \sum\limits _{f\neq g}^{\mathrm{N}/2}}E_{fg}

.. math::

    E_{fg}={\displaystyle \sum\limits _{p\in\Omega_{f}}\sum\limits _{q\in\Omega_{g}}}\left[n_{q}n_{p}\left(2\mathcal{J}_{pq}-\mathcal{K}_{pq}\right)\right]

.. math::
    
    E_{g}={\displaystyle \sum\limits _{p\in\Omega_{g}}}n_{p}\left(2\mathcal{H}_{pp}+\mathcal{J}_{pp}\right)+{\displaystyle \sum\limits _{q,p\in\Omega_{g},q\neq p}}\Pi_{qp}^{g}\mathcal{L}_{pq}
    
.. math::

    \begin{array}{c}\\\Pi_{qp}^{g}=\left\{ \begin{array}{cc}-\sqrt{n_{q}n_{p}}\,, & p=g\textrm{ or }q=g\\+\sqrt{n_{q}n_{p}}\,, & p,q>\mathrm{N}/2\end{array}\right.\;,\qquad\delta_{q\Omega_{g}}=\begin{cases}1, & q\in\Omega_{g}\\0, & q\notin\Omega_{g}\end{cases}\end{array}

PNOF7 
-----

(PRL 119, 063002 (2017); EPJB 91, 109 (2018))

PNOF7 introduces correlation between pairs of electrons through a term that explicitly contains particle-hole symmetry.

.. math::

    E_{el}^{pnof7}=E_{el}^{pnof5}+\sum\limits _{f\neq g}^{\mathrm{N}/2}\sum\limits _{p\in\Omega_{f}}\sum\limits_{q\in\Omega_{g}}\Pi_{qp}^{\Phi}\mathcal{L}_{pq}

.. math::

    \Pi_{qp}^{\Phi}=-\Phi_{q}\Phi_{p}

.. math::

    \Phi_{q}=\sqrt{n_{q}h_{q}}
    
PNOF6
-----

(JCP 141, 044107 (2014))

In the case of PNOF6, the only difference with respect to PNOF5 relies on the interaction between electrons that belong to different electron pairs. For PNOF6 this interaction is defined as

.. math::

    E_{fg}={\displaystyle \sum\limits _{p\in\Omega_{f}}\sum\limits _{q\in\Omega_{g}}}E_{pq}^{int}={\displaystyle \sum\limits _{p\in\Omega_{f}}\sum\limits _{q\in\Omega_{g}}}\left[\left(n_{q}n_{p}-\Delta_{qp}\right)\left(2\mathcal{J}_{pq}-\mathcal{K}_{pq}\right)+\Pi_{qp}\mathcal{L}_{pq}\right]

where

.. math::

    \begin{array}{cc|cc|cc}\Delta_{qp} &  & \Pi_{qp} &  &  & Orbitals\\\hline e^{-2S}h_{q}h_{p} &  & -e^{-S}\left(h_{q}h_{p}\right)^{\frac{1}{2}} &  &  & q\leq F,p\leq F\\{\frac{\gamma_{q}\gamma_{p}}{S_{\gamma}}} &  & -\Pi_{qp}^{\gamma} &  &  &\begin{array}{c}q\leq F,p>F\\q>F,p\leq F\end{array}\\e^{-2S}n_{q}n_{p} &  & e^{-S}\left(n_{q}n_{p}\right)^{\frac{1}{2}} &  &  &q>F,p>F\end{array}

.. math::

    \begin{array}{c}\gamma_{p}=n_{p}h_{p}+\alpha_{p}^{2}-\alpha_{p}S_{\alpha}\\\alpha_{p}=\begin{cases}e^{-S}h_{p}\,, & p\leq F\\e^{-S}n_{p}\,, & p>F\end{cases}\\\Pi_{qp}^{\gamma}=\left(n_{q}h_{p}+{\displaystyle \frac{\gamma_{q}\gamma_{p}}{S_{\gamma}}}\right)^{\frac{1}{2}}\left(h_{q}n_{p}+{\frac{\gamma_{q}\gamma_{p}}{S_{\gamma}}}\right)^{\frac{1}{2}}\\S={\displaystyle\sum_{q=F+1}^{F+FN_{c}}}n_{q},\quad S_{\alpha}={\sum_{q=F+1}^{F+FN_{c}}}\alpha_{q},\quad S_{\gamma}={\sum_{q=F+1}^{F+FN_{c}}}\gamma_{q}\end{array}
