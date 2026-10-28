# Speed Evaluation — V1

An experimental Isaac Lab / Pi0.5 single-process vectorized evaluator for the simulated sink-and-bowl task. This is a preserved research prototype, not a validated replacement for the serial evaluation pipeline.

## Contents

- `code/`: vectorized environment loop, batched policy and per-environment RTC/assist code, CPU checks and benchmark utilities.
- `reference/`: frozen reference helpers from the original evaluation. These contain machine-specific paths and require adaptation to your own environment; they are not a turnkey deployment.
- `data/bowl/`: numerical initial-state fixtures, position manifest, policy normalization/configuration, and per-case pickup/placement results. HDF5 fixtures contain initial robot/object state, not image sequences. `mixed50/` is the later retained-40-plus-10 position set; do not mix it with original scores.
- `docs/FINAL_RESULTS.md`: original experiments, timing and limitations. Some historical links or host paths are archival references.

## Evaluation contract and limitations

The V1 prototype preserves the historical sink task's RTC I=2/J=2/K=2, 25 Hz control, 0.004 s physics step with 10 substeps, scoring and optional physical fixed-joint grasp assist. Weights, training images, scene assets, container images and training checkpoints are **not** included. They must be supplied separately and matched to the configuration and norm used for the run. No robot commands are issued by these offline artifacts alone.

The N2 prototype showed a 1.34× throughput result in a small comparison, but trajectories were not equivalent; notably case 7020 differed substantially in peak lift. These results do not establish equivalence or generalizable throughput, and should not be combined with earlier official scores. See the detailed report before reusing results. Auxiliary placement can be marked successful before the fixed-joint releases; raw placement and actual release must be reported separately.

Initial-state fixtures include case IDs 7001–7050 plus a reference demo; the region-2 fixture holds IDs 7101–7124. CSVs record original scoring and pickup ≥5 cm in separate files. The later `mixed50` fixture retains 7001–7040 and adds 8101–8110; those new positions were not yet scored in the recorded migration attempt. The files are evaluation fixtures/results, not the complete bowl training dataset.

## Reuse

Inspect `docs/README.md`, `code/evaluate_vectorized.py`, `code/vector_runtime.py`, `code/batched_rtc.py`, and the reference files before adapting paths or launching. Run CPU-only checks in a compatible environment first. A full Isaac Sim/Isaac Lab runtime, assets, correct model weights and assigned GPU are needed for actual rollout. The newer Arena 0.3 migration is separate and is not included as a verified implementation here.
