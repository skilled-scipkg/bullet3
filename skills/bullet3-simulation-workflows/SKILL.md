---
name: bullet3-simulation-workflows
description: Use this skill for end-to-end Bullet3 simulation execution flow, from minimal hello-world scenes to complex demo and PyBullet workflow runs, with reproducibility checks.
---

# bullet3: Simulation Workflows

## High-Signal Playbook
### Route conditions
- Use `bullet3-build-and-install` if binaries/modules do not build or import.
- Use `bullet3-api-and-scripting` for low-level API usage details and transport behavior.
- Use `bullet3-inputs-and-modeling` for URDF/SDF/MJCF modeling and asset semantics.
- Use `bullet3-test` for OpenCL/multithreading validation and perf triage.

### Triage questions
1. Is the workflow C++ demo app, PyBullet script, or gym/deep-mimic pipeline?
2. Do you need deterministic replay or interactive real-time behavior?
3. Which scene complexity tier is needed: hello-world, rigid-body constraints, or RL/mocap runs?
4. Which assets are required (URDF/SDF, motion files, terrain files, trained policy files)?
5. Are you validating physics correctness, rendering behavior, or throughput?
6. What is the expected artifact: console trace, GUI behavior, saved state/log, or reward curve?

### Canonical workflow
1. Start with `docs/latex/helloworld.tex` and `examples/HelloWorld/HelloWorld.cpp` for baseline world lifecycle.
2. Confirm build output launches `App_HelloWorld` and/or `App_ExampleBrowser`.
3. Progress to constraint and rigid-body demos (`examples/Constraints`, `examples/RigidBody`, `examples/Tutorial`).
4. For scripted flows, run `examples/pybullet/examples/hello_pybullet.py` and then richer scene scripts (for example `createObstacleCourse.py`, `constraint.py`).
5. For robotics RL paths, run env examples under `examples/pybullet/gym/pybullet_envs/examples`.
6. For deep-mimic motion workflows, use arg files under `examples/pybullet/gym/pybullet_data/args` with `examples/pybullet/gym/pybullet_envs/deep_mimic/testrl.py`.
7. Use save/restore tests (`saveRestoreStateTest.py`) for repeatability checks.
8. Escalate to source entry points when demo behavior differs from expectations.

### Minimal working example
```bash
./bin/App_HelloWorld
python examples/pybullet/examples/hello_pybullet.py
python examples/pybullet/examples/createObstacleCourse.py
python examples/pybullet/gym/pybullet_envs/deep_mimic/testrl.py --arg_file run_humanoid3d_walk_args.txt
```

### Pitfalls and fixes
- Axis confusion between demos: C++ examples often use Y-up (`setGravity(0,-10,0)`), many PyBullet scripts use Z-up (`setGravity(0,0,-10)`).
- Non-deterministic stepping: avoid relying on real-time mode when deterministic replay is required.
- Asset lookup failures: register search path (`pybullet_data.getDataPath()`) or use explicit file paths.
- DeepMimic arg file mismatch: use valid files from `examples/pybullet/gym/pybullet_data/args` and ensure referenced model/motion files exist.
- ExampleBrowser demo mismatch: `--start_demo_name` requires exact demo label.
- Overly complex first run: start with HelloWorld, then add constraints/motors/rendering incrementally.

### Convergence and validation checks
- Falling-body trajectory appears in HelloWorld output and is monotonic under gravity.
- Constraint demos remain stable (no immediate explosions) with default timesteps.
- PyBullet scripts return non-negative body ids and run multiple simulation steps.
- Save/restore tests reproduce state snapshots with no diff.
- DeepMimic test loop prints `motion_file=...` and finite `total_reward=...` cycles.

## Scope
- Handle runbook-level simulation flow from minimal startup to realistic scenes.
- Keep answers procedural and reproducibility-focused.

## Primary documentation references
- `README.md`
- `docs/latex/helloworld.tex`
- `docs/latex/intro.tex`
- `examples/HelloWorld/HelloWorld.cpp`
- `examples/Constraints/ConstraintDemo.cpp`
- `examples/Tutorial/Dof6ConstraintTutorial.cpp`
- `examples/RigidBody/KinematicRigidBodyExample.cpp`
- `examples/pybullet/examples/hello_pybullet.py`
- `examples/pybullet/examples/createObstacleCourse.py`
- `examples/pybullet/gym/pybullet_envs/deep_mimic/testrl.py`
- `examples/pybullet/gym/pybullet_data/args/run_humanoid3d_backflip_args.txt`

## Workflow
- Start with primary references.
- If details are missing, inspect `references/doc_map.md`.
- Use `references/source_map.md` for implementation-level stepping/constraint behaviors.
- Cite exact file paths for workflow choices.

## Tutorials and examples
- `examples/HelloWorld`
- `examples/Tutorial`
- `examples/RigidBody`
- `examples/Constraints`
- `examples/pybullet/examples`
- `examples/pybullet/gym/pybullet_envs/examples`

## Test references
- `examples/pybullet/unittests/saveRestoreStateTest.py`
- `examples/pybullet/unittests/unittests.py`

## Optional deeper inspection
- `examples/ExampleBrowser`
- `examples/SharedMemory`
- `src`

## Source entry points for unresolved issues
- `examples/HelloWorld/HelloWorld.cpp` (minimal world create/step/cleanup lifecycle)
- `examples/Constraints/ConstraintDemo.cpp` (constraint setup and parameterized demos)
- `examples/Tutorial/Dof6ConstraintTutorial.cpp` (6DoF spring/solver tuning patterns)
- `examples/RigidBody/KinematicRigidBodyExample.cpp` (kinematic body update callback behavior)
- `examples/ExampleBrowser/OpenGLExampleBrowser.cpp` (CLI routing, `--start_demo_name`, fixed timestep)
- `examples/ExampleBrowser/ExampleEntries.cpp` (demo catalog and menu labels)
- `examples/pybullet/examples/createObstacleCourse.py` (procedural scene construction)
- `examples/pybullet/gym/pybullet_envs/deep_mimic/testrl.py` (arg-file driven runtime loop)
- `examples/pybullet/gym/pybullet_data/args/*.txt` (canonical run/train parameter bundles)
- Prefer targeted search: `rg -n "stepSimulation|setRealTimeSimulation|start_demo_name|motion_file|num_sim_substeps" examples`.
