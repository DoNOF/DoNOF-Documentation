########
Examples
########

The official examples are maintained in the DoNOFsw repository:

- https://github.com/DoNOF/DoNOFsw/tree/master/examples

Current example set
-------------------

- ``0-energy-RI.inp``: single-point energy with RI integrals
- ``1-energy-Full.inp``: single-point energy with full ERIs
- ``2-optimize-geom.inp``: geometry optimization
- ``3-grad-nuc.inp``: analytic nuclear gradient
- ``4-hess-nuc.inp``: numerical Hessian from analytic gradients
- ``5-optimize-geom.inp`` (+ ``5-optimize-geom.gcf``): restart-style optimization
- ``6-dyn1.inp`` (+ ``6-dyn1.gcf``): molecular dynamics run
- ``7-dyn2.inp`` (+ ``7-dyn2.gcf``): molecular dynamics variant
- ``8-erpa.inp``: ERPA calculation
- ``9-nlop.inp``: nonlinear optical properties

Minimal single-point example
----------------------------

::

    &INPRUN RUNTYP='ENERGY' MULT=1 ICHARG=0 /
    $DATA
    Water
    aug-cc-pVDZ
    O 8.0  0.000000  0.000000  0.000000
    H 1.0  0.000000  0.757000  0.587000
    H 1.0  0.000000 -0.757000  0.587000
    $END
    &NOFINP IPNOF=8 /

Dynamics reminder
-----------------

For ``RUNTYP='DYN'``, include ``&INPDYN`` and provide a valid ``GCF`` file.
