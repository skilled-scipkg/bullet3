---
name: bullet3-api-and-scripting
description: Use this skill for PyBullet and Bullet C-API scripting workflows, including connection modes, simulation stepping, robot control loops, and Python environment integration.
---

# bullet3: API and Scripting

## High-Signal Playbook
### Route conditions
- Use `bullet3-build-and-install` when import/build/toolchain setup is the blocker.
- Use `bullet3-inputs-and-modeling` for URDF/SDF/MJCF modeling semantics and asset authoring choices.
- Use `bullet3-simulation-workflows` for full scenario pipelines and reproducibility across demos.
- Use `bullet3-test` for OpenCL/multithreading performance validation.

### Triage questions
1. Which connection mode is required: `DIRECT`, `GUI`, `SHARED_MEMORY`, `UDP`, or `TCP`?
2. Is the task headless batch simulation, interactive GUI control, or remote server control?
3. Are assets loaded from `pybullet_data` or custom absolute/relative paths?
4. Are joint motors expected to move freely or controlled explicitly?
5. Is determinism required (`stepSimulation`) or wall-clock progression (`setRealTimeSimulation`)?
6. Is this pure PyBullet script usage or gym/pybullet_envs integration?

### Canonical workflow
1. Start from the Quickstart API contract in `docs/pybullet_quickstart_guide/PyBulletQuickstartGuide.md.html`.
2. Connect (`p.connect(...)`) and validate non-negative client id.
3. Register asset root (`p.setAdditionalSearchPath(pybullet_data.getDataPath())`) if using bundled models.
4. Load a basic world (`plane.urdf`, robot/object URDF) and set gravity.
5. Use `stepSimulation` loop for deterministic stepping; only use real-time mode when interactivity is intended.
6. For articulated systems, set motor mode explicitly (`setJointMotorControl2`) before expecting movement.
7. For gym integration, confirm environment registration/import path via `pybullet_envs` and run a short reset/step loop.
8. Escalate to source map when behavior depends on transport/client/server internals.

### Minimal working example
```python
import pybullet as p
import pybullet_data

cid = p.connect(p.DIRECT)
assert cid >= 0
p.setAdditionalSearchPath(pybullet_data.getDataPath())
p.setGravity(0, 0, -10)
plane = p.loadURDF("plane.urdf")
robot = p.loadURDF("r2d2.urdf", [0, 0, 1])
for _ in range(240):
    p.stepSimulation()
print("plane", plane, "robot", robot)
p.disconnect()
```

### Pitfalls and fixes
- `DIRECT` mode has no OpenGL/VR GUI features: use `GUI` or remote GUI server when visualization is required.
- `setRealTimeSimulation(1)` in `DIRECT` mode does not advance physics autonomously.
- `loadURDF` fails with relative paths: set additional search path or use absolute paths.
- Robot joints seem locked: default joint motors are enabled; set control mode/targets explicitly.
- Multiple GUI connections fail: only one local in-process GUI server is allowed.
- Shared-memory/TCP/UDP mismatch: align host/port/key and API bitness (32/64-bit compatibility constraints).

### Convergence and validation checks
- `p.getConnectionInfo()` reports expected connection method and `isConnected=1`.
- `p.loadURDF(...)` returns non-negative ids.
- `p.getBasePositionAndOrientation()` changes as expected after stepping.
- A short gym reset/step loop (`env.reset(); env.step(action)`) runs without import errors.
- `p.disconnect()` transitions connection status cleanly.

## Scope
- Handle runtime Python API behavior and client/server scripting workflows.
- Keep docs-first; inspect C/C++ bindings only when API docs are insufficient.

## Primary documentation references
- `README.md`
- `docs/pybullet_quickstart_guide/PyBulletQuickstartGuide.md.html`
- `docs/pybullet_quickstartguide.pdf`
- `examples/pybullet/examples/hello_pybullet.py`
- `examples/pybullet/gym/pybullet_envs/minitaur/envs/README.md`
- `examples/pybullet/unittests/unittests.py`
- `examples/pybullet/unittests/saveRestoreStateTest.py`

## Workflow
- Start with the primary references above.
- If details are missing, inspect `references/doc_map.md`.
- Escalate to `references/source_map.md` for function-level behavior or transport internals.
- Cite exact API/doc file paths used.

## Tutorials and examples
- `examples/pybullet/examples`
- `examples/pybullet/gym/pybullet_envs/examples`

## Test references
- `examples/pybullet/unittests/unittests.py`
- `examples/pybullet/unittests/saveRestoreStateTest.py`
- `examples/pybullet/unittests/userDataTest.py`

## Optional deeper inspection
- `examples/SharedMemory`
- `examples/Importers`
- `src`

## Source entry points for unresolved issues
- `examples/pybullet/pybullet.c` (Python binding methods: connect/loadURDF/step/setJointMotorControl2/createMultiBody/getCameraImage)
- `examples/SharedMemory/PhysicsClientC_API.cpp` (client command construction and submission paths)
- `examples/SharedMemory/PhysicsServerCommandProcessor.cpp` (server-side command handling and world stepping)
- `examples/Importers/ImportURDFDemo/BulletUrdfImporter.cpp` (URDF load pipeline from file to runtime objects)
- `examples/Importers/ImportURDFDemo/UrdfParser.cpp` (URDF parse behavior and defaults)
- `examples/pybullet/gym/pybullet_envs/__init__.py` (env registration catalog)
- `examples/pybullet/gym/pybullet_envs/env_bases.py` (gym environment lifecycle and render flow)
- Prefer targeted search: `rg -n "pybullet_connect|loadURDF|setRealTimeSimulation|setJointMotorControl2|createMultiBody" examples/pybullet/pybullet.c`.
