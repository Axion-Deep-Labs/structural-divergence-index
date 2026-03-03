# Structural Divergence Index (SDI)

**Predicting fine-tuning degradation from model structure, not benchmarks.**

SDI is a composite metric that quantifies geometric and spectral shifts between a base model and its fine-tuned variant. It predicts performance degradation without running full benchmark suites, requiring only lightweight probe inference.

## The Problem

Fine-tuning foundation models introduces unpredictable behavioral regressions. A single benchmark pass on a 7B parameter model takes hours of GPU time. Organizations running dozens of fine-tunes per week cannot evaluate every candidate before deployment. Degraded models reach production.

## How SDI Works

SDI combines four complementary structural signals:

| Signal | Method | What It Measures |
|--------|--------|-----------------|
| Spectral Divergence | SVD per layer before/after fine-tuning | Structural deformation of learned transformations |
| Representation Drift | CKA on a 1,000-sample probe set | Internal representation shifts |
| Curvature Shift | Hutchinson Hessian trace estimates | Sharp-to-flat transitions affecting generalization |
| Weight Geometry | Normalized per-layer L2 distance | Raw magnitude of parameter shift |

**Output:** A single risk score (0-1) predicting likelihood and severity of capability degradation.

**Computation time:** Under 10 minutes for models up to 7B parameters.

## Scientific Foundation

SDI builds on independently replicated results from the research literature:

- **Martin & Mahoney (2021).** Implicit self-regularization in deep neural networks. *JMLR*.
- **Kornblith et al. (2019).** Similarity of neural network representations revisited. *ICML*.
- **Keskar et al. (2017).** On large-batch training for deep learning: sharp minima. *ICLR*.
- **Li et al. (2018).** Visualizing the loss landscape of neural nets. *NeurIPS*.
- **Aghajanyan et al. (2021).** Intrinsic dimensionality explains the effectiveness of language model fine-tuning. *ACL*.

No novel theoretical claims required. The innovation is engineering known signals into a validated predictive governance tool.

## Phase I: Validation (NSF SBIR, $305K, 9 months)

**Objective 1:** Define and formalize SDI. Reproducible computation pipeline, open-source.

**Objective 2:** Build a dataset of 50+ fine-tune pairs across 5 model families (Llama, Mistral, Phi, Gemma, Qwen). Domain, instruction, and deliberately degraded fine-tunes.

**Objective 3:** Validate predictive correlation.
- Benchmarks: MMLU (capability), IFEval (instruction following), ToxiGen (safety), TruthfulQA (hallucination)
- Success: Spearman rho >= 0.7 between SDI and degradation magnitude
- False negative rate < 15% for high-regression cases

## Phase II: Product ($1.25M, 2 years)

- Months 1-6: Composite Structural Risk Score with threshold classifier
- Months 6-12: Cloud API (upload models, receive SDI + risk report)
- Months 12-18: Enterprise features (audit logs, model lineage, SOC 2, on-prem)
- Months 18-24: Regulated industry pilots, Series A preparation

## Status

Phase I R&D plan complete. NSF SBIR application in preparation.

## Team

**Axion Deep Labs, Inc.**

- Joshua Gutierrez, CEO & Founder (PI)
- Crystal Gutierrez, Chairperson

## License

MIT

## Contact

labs@axiondeep.com

## Related Projects

- [PERSIST](https://github.com/Axion-Deep-Labs/persist-topological-forgetting) — Topological signatures of knowledge persistence
- [DRIFT](https://github.com/Axion-Deep-Labs/drift-quantum-degradation) — Quantum circuit stability under iteration
- [PHI](https://github.com/Axion-Deep-Labs/phi-integrated-information) — Integrated information across architectures
- [GENESIS](https://github.com/Axion-Deep-Labs/genesis-capacity-scaling) — Information capacity scaling laws
