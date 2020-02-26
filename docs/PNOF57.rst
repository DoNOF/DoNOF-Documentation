PNOF5 and PNOF7
=====

The non-relativistic electronic energy can be written as an explicit functional of the 1- and 2-order reduced density matrices (RDM)

.. math::

    E_{el}[\Gamma,D]=\sum_{ik}\Gamma_{ki}h_{ki}+\sum_{ijkl}D_{kl,ij}\langle kl|ij\rangle
    
In practical applications of NOFT we approximate the 2RDM in terms of the natural occupation numbers

.. math::

    E_{el}[\left\{ n_{i},\phi_{i}\right\}]=\sum\limits _{i}n_{i}\mathcal{H}_{ii}+\sum\limits _{ijkl}D[n_{i},n_{j},n_{k},n_{l}]\left\langle kl|ij\right\rangle
    
DoNOF contains three approximations that give up to the NOFs named as PNOF5, PNOF6, and PNOF7. Corresponding formulas are given below

PNOF5 (JCP 134, 164102 (2011)):

.. math::

    E_{el}^{pnof5}={\displaystyle \sum\limits _{g=1}^{\mathrm{N}/2 E_{g}+{\displaystyle \sum\limits _{f\neq g}^{\mathrm{N}/2}}E_{fg}

.. math::

    E_{fg}={\displaystyle \sum\limits _{p\in\Omega_{f}}\sum\limits _{q\in\Omega_{g}}}\left[n_{q}n_{p}\left(2\mathcal{J}_{pq}-\mathcal{K}_{pq}\right)\right]

.. math::
    
    E_{g}={\displaystyle \sum\limits _{p\in\Omega_{g}}}n_{p}\left(2\mathcal{H}_{pp}+\mathcal{J}_{pp}\right)+{\displaystyle \sum\limits _{q,p\in\Omega_{g},q\neq p}}\Pi_{qp}^{g}\mathcal{L}_{pq}

PNOF7 (PRL 119, 063002 (2017); EPJB 91, 109 (2018)):
    
.. math::

E_{el}^{pnof7}=E_{el}^{pnof5}+\sum\limits _{f\neq g}^{\mathrm{N}/2}\sum\limits _{p\in\Omega_{f}}\sum\limits _{q\in\Omega_{g}}\Pi_{qp}^{\Phi}\mathcal{L}_{pq}
.. math::
    \left|\Pi_{qp}\right|\leq\Phi_{q}\Phi_{p}
.. math::
    \Phi_{q}=\sqrt{n_{q}h_{q}}

    
PNOF6 (JCP 141, 044107 (2014)):

.. math::



n_{\mathrm{offset}} = \sum_{k=0}^{N-1} s_k n_k

