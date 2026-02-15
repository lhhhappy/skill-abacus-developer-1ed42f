# Abacus-Developer Skill

A comprehensive skill for using Abacus (formerly ABACUS) - a powerful DFT (Density Functional Theory) software package for materials science and computational chemistry.

---

## What is Abacus?

Abacus is an open-source DFT software developed by Peking University. It enables accurate calculations of:
- Electronic structure
- Energy optimization
- Molecular dynamics
- Properties of materials

---

## Quick Start

### Prerequisites

- Linux system (recommended: Ubuntu 20.04+)
- C++ compiler (GCC 9.0+)
- FFTW3 library
- OpenMPI or ScaLAPACK (for parallel computing)

### Basic Calculation Workflow

```bash
# 1. Prepare input file (INPUT)
# 2. Run the calculation
mpirun -np 4 abacus > log.txt

# 3. Analyze output files
# - RUNNING-1.ecs: Electron density
# - OUT.ABACUS: Final energy and forces
```

---

## Input File Structure

### Basic INPUT Example

```
INPUT_PARAMETERS
calculation scf          # scf, relax, md
ntype 1
atom_file STRU
ecutwfc 80             # Plane wave cutoff (Ry)
mixing_type Pulay
mixing_beta 0.7
scf_thr 1.0e-6         # Convergence threshold
max_iter 100
```

### Structure File (STRU)

```
ATOMIC_SPECIES
C 12.01 C.upf

ATOMIC_POSITIONS
Cartesian
C 0.0 0.0 0.0
C 1.5 0.0 0.0

LATTICE_CONSTANT
5.0
```

---

## Common Calculations

### 1. Structure Optimization

```
calculation relax
force_thr 1.0e-3
```

### 2. Molecular Dynamics

```
calculation md
md_type NVT
md_nstep 100
md_dt 1.0
```

### 3. Band Structure

```
calculation nscf
init_chg file
```

---

## Pseudopotentials

Download from ABACUS website:
```bash
# Recommended pseudopotentials
wget https://github.com/abacusmodeler/abacus-pseudopot/tree/main/SSSP_efficiency
```

---

## Output Analysis

### Key Files

| File | Description |
|------|-------------|
| OUT.ABACUS | Summary of calculation results |
| running_scf.log | Detailed SCF iteration log |
| SPIN1_CHG.cube | Charge density (for visualization) |
| KPT | k-point information |

### Energy Analysis

```bash
# Extract final energy
grep "total energy" OUT.ABACUS
```

---

## Advanced Features

### DFT+U (Hubbard U)

```
dft_plus_u true
lda_plus_u_kind 1
hubbard_u {"C": 4.0}
```

### Van der Waals Correction

```
vdw_method d3_bj
vdw_s6 0.75
```

---

## Common Errors & Solutions

### "Too few k-points"
→ Increase k-point density in KPT file

### "Pseudopotential not found"
→ Check pseudopotential path in STRU file

### "Memory overflow"
→ Reduce ecutwfc or use smaller basis set

---

## Integration with Other Tools

### Visualization (VESTA)

```bash
# Convert charge density to VESTA format
python abacus2vesta.py SPIN1_CHG.cube
```

### High-Throughput Calculations

Use ASE (Atomic Simulation Environment):

```python
from ase.calculators.abacus import Abacus

calc = Abacus(path='/path/to/abacus',
              nproc=4,
              pseudo_dir='./')

atoms.set_calculator(calc)
energy = atoms.get_potential_energy()
```

---

## References

- Official Docs: https://abacus.deepmodeling.com/
- GitHub: https://github.com/abacusmodeler/abacus-develop
- Forum: https://github.com/abacusmodeler/abacus-develop/discussions
