# Single Point Energy

You can run a single point energy calculation USING THE `RUNTYP='ENERGY'` in the `&INPRUN` as in the following example:

~~~
 &INPRUN RUNTYP='ENERGY' MULT=1 ICHARG=0 ERITYP='FULL' /
 $DATA
 Water (H2O)
 cc-pVDZ
O  8.0  0.0000     0.0000    0.1173
H  1.0  0.0000     0.7572   -0.4692
H  1.0  0.0000    -0.7572   -0.4692
 $END
 &NOFINP IPNOF=8 /
~~~

## Input Sections

### `&INPRUN`

You can identify the following information inside the `&INPRUN` directive:
- `RUNTYP`: ENERGY for the single point NOF calculation
- `MULT`: The spin multiplicity.
- `ICHARG`: The charge of the system
- `ERITYP`:
  - `FULL`: For using four center integrals
  - `RI`: For using the resolution of the identity approximation
  - `MIX`: For automatically performin an RI calculation followed by a restart with FULL.  

### `$DATA`

You can identify the following information inside the `$DATA` block of this example:
- `title`: Water (H2O)
- `basis name`: cc-pVDZ
- `XYZ geometry`: Notice that the atomic number of each atom is indicated.

### `&NOFINP`

You can identify the following information inside the `&NOFINP` directive:
- `IPNOF`: 5 (PNOF5) | 7 (PNOF7) | 8 (GNOF)
