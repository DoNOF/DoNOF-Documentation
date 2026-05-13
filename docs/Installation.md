# Download and Installation

## Requirements

- A Fortran compiler compatible with the project `Makefile` (currently `gfortran`)
- `libcint`
- `OpenMPI` (only if MPI execution is needed)
- BLAS and LAPACK libraries

Install `libcint` (example):

```bash
git clone https://github.com/sunqm/libcint.git
cd libcint
mkdir build && cd build
cmake -DCMAKE_INSTALL_PREFIX:PATH=/usr/local/lib ..
sudo make install
```

## Clone and Build

```bash
git clone https://github.com/DoNOF/DoNOFsw
cd DoNOFsw
```

Build targets currently available:

```bash
make serialg   # exe/DoNOFg.x
make ompg      # exe/DoNOFompg.x
make mpig      # exe/DoNOFmpig.x
```

## Execution

Input examples are provided in `examples/`.

If the input is `filename.inp`, run with:

```bash
./run_donofg filename
./run_donofompg filename
./run_donofmpig filename
./run_donofg_dyn filename
./run_donofompg_dyn filename
./run_donofmpig_dyn filename
```

The output is written to `filename.out`.

## Notes

- Main input control is provided by `&INPRUN` and `&NOFINP`.
- Molecular dynamics (`RUNTYP='DYN'`) additionally uses `&INPDYN`.
- Current defaults include `IPNOF=8` (GNOF), `ERITYP='RI'`, `USELIB=.TRUE.`, and `GTYP='SPH'`.
