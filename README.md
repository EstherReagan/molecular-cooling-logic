# Thermo-Responsive Viscosity Collapse in Iron Coordination Complexes

**Status:** Preliminary theoretical proposal. **No experimental data. Not validated.**

## Overview

This repository contains a reproducible analysis of a proposed microfluidic cooling system using temperature-responsive iron coordination complexes in ionic liquids. The work presents:

1. **Viscosity Model**: A sigmoid function (Eq. 3 from the draft) fitted to calculated values
2. **Thermodynamic Framework**: Low-spin ↔ high-spin equilibrium (Gibbs energy)
3. **Flow Analysis**: Reynolds number and Nusselt number analysis
4. **Power Balance**: Proposed energy recovery equation

**Important caveat**: All numerical results are derived from a theoretical model. The original draft contains:
- An **unidentified iron complex** ([Fe(pybza)₃]²⁺ is not a recognized compound)
- **Missing material properties** (ionic conductivity, electrode geometry, flow parameters)
- **Unsupported claims** (32.4 W/cm² power, "zero-latency" response)
- **No experimental validation**

This code is provided to enable independent verification of model calculations and to facilitate future experimental work.

## Key Finding: Reproducibility Audit

The viscosity model (Eq. 3) successfully reproduces all values in Table 1 with a single fitted parameter: **β = 0.30 K⁻¹**. This parameter was not stated in the original draft and is derived here.

**Voltage values in Table 1** do not follow from any equation in the draft and cannot be independently calculated.

## Installation

### Requirements
- Python 3.9+
- pip or conda

### Setup

```bash
git clone https://github.com/user/molecular-logic-cooling-model.git
cd molecular-logic-cooling-model

# Create virtual environment
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate

# Install dependencies
pip install -r requirements.txt

# Install package in editable mode
pip install -e .
```

## Running the Code

### Reproduce Viscosity Model

```bash
python scripts/fit_sigmoid_model.py
```
Output: Fits Eq. 3 to draft Table 1 values and reports residuals.

### Calculate Reynolds Numbers

```bash
python scripts/reynolds_analysis.py --temp 25 70 85 100 120 \
  --velocity 1.0 --diameter_um 200 --density 1000
```
Output: Re values across temperature range.

### Run Tests

```bash
pytest tests/ -v
```

### Generate Figures

```bash
python scripts/generate_figures.py
```
Output: PDF and PNG figures saved to `manuscript/figures/`

### Compile LaTeX Manuscript

```bash
cd manuscript
pdflatex manuscript.tex
bibtex manuscript
pdflatex manuscript.tex
pdflatex manuscript.tex
cd ..
```

## Repository Structure

- **`src/`**: Core library functions (models, unit conversions, validation)
- **`scripts/`**: Standalone analysis scripts (each can be run independently)
- **`tests/`**: pytest test suite with unit tests and dimensional consistency checks
- **`data/`**: CSV files with draft values and reproduced results
- **`manuscript/`**: LaTeX source and compiled PDF
- **`docs/`**: Documentation of gaps, limitations, missing parameters

## Key Results

### Viscosity Model Validation

| T (°C) | Draft Value (mPa·s) | Calculated (mPa·s) | Residual |
|--------|---------------------|-------------------|----------|
| 25     | 145.00              | 145.00            | 0.00     |
| 70     | 143.46              | 143.46            | 0.00     |
| 85     | 75.00               | 75.00             | 0.00     |
| 100    | 6.54                | 6.54              | 0.00     |
| 120    | 5.00                | 5.00              | 0.00     |

**Conclusion**: Table 1 viscosity values are perfectly reproduced by Eq. 3 with **β = 0.30 K⁻¹**.

### Voltage Values Cannot Be Reproduced

Table 1 lists voltage values (0.0000, 0.1272, 0.5040, 1.0479, 1.3300 V), but:
- No equation in the draft directly computes these
- Proposed Eq. 2 (Seebeck) requires undefined parameters (α, ΔS_SCO)
- **Status**: Cannot be independently calculated

## Critical Issues Needing Resolution

1. **Iron complex identity**: [Fe(pybza)₃]²⁺ is not a standard compound. Requires:
   - IUPAC name
   - Synthesis reference
   - OR correction to a known complex (e.g., [Fe(bpy)₃]²⁺)

2. **Material properties missing**:
   - Ionic conductivity σ_eff of IL + iron complex
   - Thermal conductivity λ
   - Specific heat capacity c_p
   - Electrode geometry (d_electrode)

3. **Flow regime unknown**:
   - Channel hydraulic diameter D_h
   - Volumetric flow rate Q
   - Actual Reynolds number Re (cannot verify if Nusselt correlation applies)

4. **Seebeck coefficient**:
   - Eq. 2 lacks derivation
   - Parameter α undefined
   - ΔS_SCO not calculated

5. **Power output (32.4 W/cm²)**:
   - No calculation path shown
   - All five parameters in Eq. 6 are unspecified or unknown

## Statement of Limitations

- **This is a theoretical proposal, not an experimental validation.**
- No spin-crossover kinetics data provided.
- No cycling data (claimed 10⁶ reversible cycles).
- No actual microfluidic device built or tested.
- Response time to thermal transient is not quantified.
- The term "zero-latency" in the original draft is physically impossible.

## Next Steps for Experimental Validation

1. Identify the iron complex (or confirm if it is a novel ligand)
2. Measure viscosity-temperature profile experimentally (DSC, rotational rheometry)
3. Characterize spin-crossover transition (SQUID, UV-Vis, NMR)
4. Measure ionic conductivity of the fluid mixture
5. Design and fabricate microfluidic channels; measure heat transfer
6. Perform thermal response time experiments

## Citation

If you use this code or reproduce these calculations, cite:

```bibtex
@software{divya2024molecular,
  author = {Divya, Esther},
  title = {Thermo-Responsive Viscosity Collapse in Iron Coordination Complexes: Reproducible Analysis},
  year = {2024},
  url = {https://github.com/user/molecular-logic-cooling-model}
}
```

## License

This work is provided under the MIT License. See `LICENSE` file.

## Contact

Esther Divya  
esther.reaganragnar12@proton.me

---

**Last updated**: [Date]  
**Status**: Unvalidated theoretical proposal suitable for motivating experimental work.
