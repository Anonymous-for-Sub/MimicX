# Motion Tracking and Simulation Backends

## Protocol

Twelve prepared motion references are evaluated under nominal and perturbed
conditions. Three native methods share two training seeds and matched
warmstarts: continuous BeyondMimic/MjLab tracking, Static Search, and MimicX.
Each continuation uses 3,000 PPO updates; candidates are evaluated at six slots.
Final evaluation uses three independent repeats per condition and training seed.
Released SONIC uses three executions per condition without additional training.

Completion means finishing the full motion under the evaluation protocol, not
meeting every tracking-precision threshold. The task-level tables retain
all 12 motions and both conditions, including incomplete executions. Undefined
full-horizon metrics are not replaced by common-prefix errors.

- [All task-level measurements](assets/results/motion-study/all_tasks.csv)
- [Four-method metrics and definitions](assets/results/motion-study/four_methods.md)
- [Measured training-phase costs](assets/results/motion-study/native_phase_costs.csv)

The displayed four-method clips use a shared fixed camera and full reference
clock. Each is one nominal execution; aggregate reductions use all six native
nominal evaluations, rather than only the displayed trial.

## Isaac

MuJoCo/MjLab is used for the 12-motion comparison. The native Isaac Lab backend
has separately completed one-motion training, checkpoint save/reload/resume,
rollout and refinement validation. This backend validation does not change the
simulator or metric definitions of the 12-motion comparison.

## Method

MimicX uses execution errors to coordinate bounded tracking-objective changes
and failure-window practice, followed by policy continuation and repeated
verification against the current policy. The selected policy enters the next
feedback pass. See the [method guide](METHOD.md).
