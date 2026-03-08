# FlexAID (template fork)

Flexible Artificial Intelligence Docking – **personal template fork** of the NRGlab FlexAID repository.[^nrglab][^flexaid]

[^nrglab]: https://github.com/NRGlab
[^flexaid]: https://github.com/NRGlab/FlexAID

This repository tracks the C/C++ FlexAID code with a CMake build system and is intended primarily as a **development sandbox** and template for derivative work (e.g. NRGsuite integration, modernized branches such as FlexAIDdS). For production use, prefer the upstream NRGlab repository.

---

## 1. Upstream reference

Canonical FlexAID code and documentation:

- NRGlab/FlexAID: https://github.com/NRGlab/FlexAID
- NRGsuite GUI: https://github.com/NRGlab/NRGsuite
- NRGlab resources: https://biophys.umontreal.ca/nrg/resources.html

Everything below mirrors the upstream build and usage model.

---

## 2. Getting the CMake/C++ version

```bash
git clone --branch flexaid-cpp https://github.com/lmorency/FlexAID.git
cd FlexAID
mkdir build && cd build
cmake .. -DCMAKE_BUILD_TYPE=Release
cmake --build . --target FlexAID -j 4
```

Result: `FlexAID` executable in `build/`.

---

## 3. Inputs via ProcessLigand

Use `processligand-py` from NRGlab to generate `.inp` and `.inp.pdb` files and, optionally, binding‑site sphere files (`*_sph_*.pdb`).

```bash
pip install processligand-py
```

Important convention (as in upstream): set `atom_index=90000` for the ligand so FlexAID can recognize it in the config.

---

## 4. Config & GA files (summary)

This fork follows the same config/GA interface as NRGlab/FlexAID:

- **Required config keys** (minimal):
  - `INPLIG`, `PDBNAM`, `METOPT`, `OPTIMZ`, `RNGOPT`
- **Optional config keys**:
  - `FLEXSC`, `RMSDST`, `MAXRES`, `CLUSTA`, `NRGOUT`, `STATEP`, `TEMPOP`, etc.
- **GA file**:
  - `NUMCHROM`, `NUMGENER`, `MUTARATE`, `CROSRATE`, `POPINIMT`, `FITMODEL`, `REPMODEL`, …

For concrete examples, consult the upstream README and `WRK/` examples in either repository.

---

## 5. Running FlexAID

```bash
./FlexAID \
  -c /absolute/path/to/config.txt \
  -g /absolute/path/to/ga.txt
```

Behavior is identical to NRGlab/FlexAID; differences you introduce in this fork (experiments, instrumentation, etc.) should be documented in your commits and, if needed, in this README.

---

## 6. License and citation

This fork inherits the **Apache 2.0** license from upstream.

Please cite the original FlexAID and NRGsuite papers when appropriate:

- Gaudreault & Najmanovich (2015), *J. Chem. Inf. Model.*
- Gaudreault, Morency & Najmanovich (2015), *Bioinformatics*.
