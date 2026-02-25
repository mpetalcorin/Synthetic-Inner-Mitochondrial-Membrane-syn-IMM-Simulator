# Synthetic-Inner-Mitochondrial-Membrane-syn-IMM-Simulator
models a cardiolipin-tunable inner mitochondrial membrane with Δψ–ΔpH partitioning, CoQ redox pool dynamics, and supercomplex assembly kinetics to predict Δp stability and ATP output.

# README.md

# Synthetic Inner Mitochondrial Membrane (syn-IMM), computational reconstitution, and analysis

This repository contains **computational modelling** of a **synthetic inner mitochondrial membrane (syn-IMM)** as a modular system coupling electron transport, proton motive force, and ATP synthesis. The work is intended for **in silico hypothesis testing, benchmarking, and sensitivity analysis**, it **does not** provide wet-lab assembly instructions.

## What is modeled

The syn-IMM model is organized as modules that mirror the inner mitochondrial membrane.

1. Respiratory electron flux (Complex I → III → IV) as a controllable throughput.
2. Proton motive force as a state variable, initially as a Δψ proxy, then extended to **separate Δψ and ΔpH**.
3. ATP synthase, converting Δp into ATP with a nonlinear dependence.
4. Cardiolipin as a tunable lipid variable that influences organization and stability.
5. Optional transport modules (ANT, PiC) that gate external ATP detectability.
6. Extension module adds an explicit **CoQ redox pool** and **supercomplex assembly fraction S(t)** with cardiolipin-dependent kinetics.

## Repository structure

- `notebooks/`
  - `synthetic_IMM_simulation.ipynb`, baseline syn-IMM dynamic model, Δψ proxy, ATP output, perturbations, sensitivity.
  - `synthetic_IMM_multistate_extension.ipynb`, multi-state Δψ–ΔpH model, CoQ pool dynamics, supercomplex state S(t), CL-dependent assembly.
- `docs/`
  - `modelcard.md`, model purpose, intended use, limitations, evaluation.
  - `datasheet.md`, dataset description, simulation parameter sources, provenance.
- `figures/`
  - Generated plots (if you export figures).
- `results/`
  - Tables, metrics, Monte Carlo outputs (if you export results).

## How to run

### Requirements
- Python ≥ 3.10
- numpy, pandas, matplotlib, nbformat (optional, for notebook generation)

### Quick start
1. Create an environment, install dependencies.
2. Open the notebooks in VS Code.
3. Run all cells from top to bottom.

## Outputs you should expect

From `synthetic_IMM_simulation.ipynb`:
- Time series of Δψ proxy, ATP synthesis rate, exported ATP accumulation.
- Perturbation comparisons (low cardiolipin, high leak, ANT limitation, low ATP synthase).
- Cardiolipin performance sweeps and Monte Carlo sensitivity analysis.

From `synthetic_IMM_multistate_extension.ipynb`:
- Separate Δψ and ΔpH trajectories, and Δp = Δψ + 60·ΔpH (mV).
- CoQ redox pool fraction (QH2) dynamics and saturation effects.
- Supercomplex assembly fraction S(t) dynamics and cardiolipin dependence.
- Heatmaps for cardiolipin × leak tradeoffs on Δp, ATP output, and S.

## Scientific grounding, PubMed indexed sources used as benchmarks

Representative anchors used for parameter ranges and design logic:
- Human mtDNA encodes 13 OXPHOS membrane subunits, foundational for defining the mtDNA-coded IMM core. Anderson et al., 1981, Nature. https://www.nature.com/articles/290457a0
- Cardiolipin is required for, or strongly promotes, respiratory supercomplex stability. Zhang et al., 2002, J Biol Chem. https://www.jbc.org/article/S0021-9258(19)71687-1/fulltext
- ATP synthase dimer rows induce membrane curvature in reconstituted systems. Blum et al., 2019, PNAS. https://www.pnas.org/doi/10.1073/pnas.1816556116
- Nernst conversion for Δp partitioning and typical pmf components. Perry et al., 2011. https://www.tandfonline.com/doi/full/10.2144/000113610
- Tissue-scale CoQ pool measurements in nmol per mg protein. Burger et al., 2020. https://www.sciencedirect.com/science/article/pii/S0891584919315655
- Reconstituted ANT transport capacity benchmarks. Kreiter et al., 2020. https://www.mdpi.com/2218-273X/10/5/685

## Safety and scope

This repository is **computational**. It does not include experimental protocols, nor does it provide instructions for constructing biological systems.

## Citation

Petalcorin, M.I.R. (2026). A Computational Synthetic Inner Mitochondrial Membrane Platform that Couples Cardiolipin-Dependent Supercomplex Kinetics, Coenzyme Q Redox Pool Dynamics, and Partitioned Proton Motive Force (Δψ and ΔpH). GitHub. https://github.com/mpetalcorin/Synthetic-Inner-Mitochondrial-Membrane-syn-IMM-Simulator

## License
MIT 
