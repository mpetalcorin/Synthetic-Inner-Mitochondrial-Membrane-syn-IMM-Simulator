# Model Card, syn-IMM computational simulator
## Model details
- **Model name:** Synthetic Inner Mitochondrial Membrane (syn-IMM) Simulator
- **Model type:** Mechanistic, dynamical systems model, ordinary difference equations at fixed timestep, with optional Monte Carlo sampling.
- **Core states:**
  - Baseline notebook, Δψ proxy, exported ATP.
  - Extension notebook, Δψ (mV), ΔpH (pH units), Δp (mV), CoQ redox pool fraction (QH2), supercomplex fraction S(t).
- **Primary outputs:** Δψ, ΔpH, Δp, ATP synthesis rate, exported ATP rate, accumulated ATP, CoQ redox state, supercomplex fraction.
## Intended use
- Hypothesis testing about which IMM modules dominate performance, cardiolipin dependence, leak sensitivity, and transport limitations.
- Building intuition for design tradeoffs in a synthetic membrane context.
- Generating figures and tables for conceptual, educational, or proposal work.

## Out of scope
- Predicting absolute rates in a specific experimental preparation without re-calibration.
- Replacing biophysical, structural, or kinetic measurements in real membranes.
- Any wet-lab design or execution guidance.

## Training data
This is not a trained statistical model, there is no training dataset. Parameters are chosen by calibration to ranges reported in PubMed-indexed literature and by internal consistency checks.

## Key scientific assumptions
1. **Δp partition** is approximated by Δp (mV) = Δψ + 60·ΔpH, a widely used Nernst conversion. Perry et al., 2011. https://pmc.ncbi.nlm.nih.gov/articles/PMC3115691/
2. **Cardiolipin dependence** is represented as a functional modifier of organization and supercomplex stability, consistent with cardiolipin’s requirement for supercomplex formation in classic reconstitution and stability studies. Zhang et al., 2002. https://pubmed.ncbi.nlm.nih.gov/12364341/
3. **ATP synthase dependence on pmf** is modeled as a steep nonlinear function of Δp, capturing the experimentally observed threshold-like behavior of ATP synthesis vs driving force in reconstituted systems, the exact curve is parameterized for plausibility. Kaim and Dimroth, 1998. https://pubmed.ncbi.nlm.nih.gov/9738451/
4. **CoQ pool** is finite and introduces redox buffering and saturation effects, with pool sizes anchored to tissue-scale measurements. Burger et al., 2020. https://pmc.ncbi.nlm.nih.gov/articles/PMC6975167/
5. **Supercomplex fraction S(t)** is a kinetic state with CL-dependent k_on and k_off, used as a minimal abstraction of dynamic organization, not a structural resolution model. Zhang et al., 2002. https://pubmed.ncbi.nlm.nih.gov/12364341/

## Evaluation
We use pragmatic acceptance tests rather than formal predictive accuracy.

### Qualitative acceptance criteria
- Stable Δψ and Δp in physiological ranges under low leak, and collapse under high leak.
- ATP output increases with improved coupling, increased ATP synthase capacity, and favorable cardiolipin range, and decreases with increased leak or transport limitation.
- CoQ redox pool shows saturating behavior, qh2 approaches 1 when oxidation is limiting, approaches 0 when reduction is limiting.
- Supercomplex fraction increases with cardiolipin and affects throughput in the expected direction.

### Quantitative sanity checks (typical targets)
- Δψ ~150–180 mV range is a common physiological reference. Brand and Nicholls, 2011. https://pmc.ncbi.nlm.nih.gov/articles/PMC3076726/
- Cardiolipin in IMM is frequently reported around 15–20% of phospholipids. Pennington et al., 2019. https://pmc.ncbi.nlm.nih.gov/articles/PMC6482085/

## Limitations
- Lumped kinetics, no explicit Complex I, III, IV mechanistic intermediates, and no explicit proton stoichiometry mapping to Δψ and ΔpH beyond a simplified gain model.
- No explicit ROS generation, and no explicit cytochrome c pool dynamics.
- Supercomplex state S(t) is a coarse abstraction, not a structural model.
- Parameter uncertainty is large across organisms, tissues, detergents, and reconstitution methods, Monte Carlo exploration is provided to handle uncertainty qualitatively.

## Ethical and safety notes
This model is intended for benign scientific use, education, and research planning. It does not provide experimental assembly protocols.

## References, PubMed indexed
- Anderson, S., et al. (1981). Sequence and organization of the human mitochondrial genome. Nature. https://pubmed.ncbi.nlm.nih.gov/7219534/
- Zhang, M., Mileykovskaya, E., & Dowhan, W. (2002). Cardiolipin is required for supercomplex formation. J Biol Chem. https://pubmed.ncbi.nlm.nih.gov/12364341/
- Blum, T. B., et al. (2019). ATP synthase dimers induce curvature and rows. PNAS. https://pubmed.ncbi.nlm.nih.gov/30760595/
- Perry, C. G. R., et al. (2011). Bioenergetic partitioning, Δψ and ΔpH, and Nernst conversion context. https://pmc.ncbi.nlm.nih.gov/articles/PMC3115691/
- Burger, N., et al. (2020). Coenzyme Q, tissue pools and quantification. https://pmc.ncbi.nlm.nih.gov/articles/PMC6975167/
- Brand, M. D., & Nicholls, D. G. (2011). Assessing mitochondrial dysfunction and Δψ context. https://pmc.ncbi.nlm.nih.gov/articles/PMC3076726/
- Pennington, E. R., et al. (2019). Cardiolipin composition and IMM context. https://pmc.ncbi.nlm.nih.gov/articles/PMC6482085/
- Kaim, G., & Dimroth, P. (1998). ATP synthesis dependence on driving force in proteoliposomes. https://pubmed.ncbi.nlm.nih.gov/9738451/
- Burger, N., et al. (2020). CoQ pools. https://pmc.ncbi.nlm.nih.gov/articles/PMC6975167/
- Kreiter, J., et al. (2020). ANT transport benchmark in reconstitution. https://pmc.ncbi.nlm.nih.gov/articles/PMC7277544/

