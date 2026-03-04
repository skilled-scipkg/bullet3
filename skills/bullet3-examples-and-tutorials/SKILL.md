---
name: bullet3-examples-and-tutorials
description: Use this skill to route users to high-value Bullet3 examples and tutorials across C++ demos, PyBullet scripts, gym environments, and deep-mimic references.
---

# bullet3: Examples and Tutorials

## High-Signal Playbook
### Route conditions
- Use `bullet3-build-and-install` when examples cannot be built/launched/imported.
- Use `bullet3-api-and-scripting` for detailed function-level PyBullet API semantics.
- Use `bullet3-simulation-workflows` for full reproducible run pipelines.
- Use `bullet3-inputs-and-modeling` for URDF/SDF/MJCF modeling and asset authoring decisions.

### Triage questions
1. Which example family is needed: C++ core demos, PyBullet scripts, gym envs, or deep-mimic?
2. Is the goal conceptual learning, runnable baseline, or regression/performance check?
3. Is GUI rendering required, or should examples run headless in `DIRECT` mode?
4. Are external deps required (`gym`, `ruamel.yaml`, RL libs)?
5. Does the user need minimal snippets or full multi-file scene workflows?
6. What validation signal is expected (console output, visual behavior, reward trace)?

### Canonical workflow
1. Start with minimal C++ lifecycle (`examples/HelloWorld/HelloWorld.cpp`, `docs/latex/helloworld.tex`).
2. Move to interactive browser demos (`App_ExampleBrowser`) for constraints/rigid-body exploration.
3. Run minimal Python script (`examples/pybullet/examples/hello_pybullet.py`).
4. Expand to scene-building scripts (`examples/pybullet/examples/constraint.py`, `examples/pybullet/examples/createObstacleCourse.py`, `examples/pybullet/examples/racecar.py`, `examples/pybullet/examples/minitaur.py`).
5. For gym robotics paths, use `examples/pybullet/gym/pybullet_envs/examples/*`.
6. For motion imitation paths, follow `examples/pybullet/gym/pybullet_envs/deep_mimic/mocap/README.md` and `examples/pybullet/gym/pybullet_envs/deep_mimic/testrl.py`.
7. Use unittests as sanity checks when examples are adapted.
8. Escalate to source map for behavior details not explained by docs/examples.

### Minimal working example
```bash
python examples/pybullet/examples/hello_pybullet.py
python examples/pybullet/examples/constraint.py
python examples/pybullet/gym/pybullet_envs/examples/minitaur_gym_env_example.py --env 0
python examples/pybullet/gym/pybullet_envs/deep_mimic/testrl.py --arg_file run_humanoid3d_walk_args.txt
```

### Pitfalls and fixes
- Mistaking license/third-party docs for runnable tutorials: focus on executable scripts and tutorial docs first.
- Missing deps for env examples: install prerequisites noted in env README files.
- CWD-sensitive assets: run from repo root or normalize paths/search paths.
- Real-time vs deterministic confusion: example scripts vary; set stepping mode deliberately.
- Deep-mimic data mismatch: ensure arg files and referenced motion/model files exist.
- ExampleBrowser demo name mismatch with CLI: use exact names from registry.

### Convergence and validation checks
- HelloWorld demo shows expected falling-body position updates.
- PyBullet hello/constraint scripts run multiple frames without exceptions.
- Gym example performs `reset`/`step` loop and emits finite observations/rewards.
- Deep-mimic test loop prints `motion_file=...` and periodic `total_reward=...` resets.
- Adapted scripts still pass minimal unit checks (`examples/pybullet/unittests`).

## Scope
- Route users quickly to realistic, runnable examples with minimal setup ambiguity.
- Prefer executable references over broad narrative docs.

## Primary documentation references
- `README.md`
- `docs/latex/helloworld.tex`
- `docs/pybullet_quickstart_guide/PyBulletQuickstartGuide.md.html`
- `examples/TwoJoint/README.md`
- `examples/pybullet/gym/pybullet_envs/deep_mimic/mocap/README.md`
- `examples/pybullet/examples/hello_pybullet.py`
- `examples/pybullet/examples/constraint.py`
- `examples/pybullet/examples/createObstacleCourse.py`
- `examples/pybullet/gym/pybullet_envs/examples/minitaur_gym_env_example.py`

## Workflow
- Start with the primary references above.
- If details are missing, inspect `references/doc_map.md`.
- Escalate to `references/source_map.md` for implementation-level demo behavior.
- Cite exact file paths for chosen examples.

## Tutorials and examples
- `examples/HelloWorld`
- `examples/BasicDemo`
- `examples/Tutorial`
- `examples/Constraints`
- `examples/RigidBody`
- `examples/pybullet/examples`
- `examples/pybullet/gym/pybullet_envs/examples`

## Test references
- `examples/pybullet/unittests/unittests.py`
- `examples/pybullet/unittests/saveRestoreStateTest.py`

## Optional deeper inspection
- `examples/ExampleBrowser`
- `examples/SharedMemory`
- `src`

## Source entry points for unresolved issues
- `examples/HelloWorld/HelloWorld.cpp` (minimal C++ simulation lifecycle)
- `examples/BasicDemo/BasicExample.cpp` (small GUI-oriented rigid-body baseline)
- `examples/Constraints/ConstraintDemo.cpp` (constraint behavior gallery)
- `examples/Tutorial/Tutorial.cpp` (physics concepts rendered in tutorial format)
- `examples/RigidBody/KinematicRigidBodyExample.cpp` (kinematic + dynamic interaction pattern)
- `examples/ExampleBrowser/ExampleEntries.cpp` (official demo list and menu names)
- `examples/pybullet/examples/hello_pybullet.py` (minimal Python baseline)
- `examples/pybullet/examples/createObstacleCourse.py` (procedural scene script)
- `examples/pybullet/gym/pybullet_envs/examples/minitaur_gym_env_example.py` (robotics env example)
- `examples/pybullet/gym/pybullet_envs/deep_mimic/testrl.py` (deep-mimic policy test loop)
- Prefer targeted search: `rg -n "CreateFunc|start_demo_name|Minitaur|DeepMimic|stepSimulation" examples`.
