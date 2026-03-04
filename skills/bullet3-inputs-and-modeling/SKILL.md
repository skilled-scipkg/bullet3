---
name: bullet3-inputs-and-modeling
description: Use this skill for Bullet3/PyBullet model ingestion and parameterization, including URDF/SDF/MJCF loading, procedural shape creation, and asset-path/modeling triage.
---

# bullet3: Inputs and Modeling

## High-Signal Playbook
### Route conditions
- Use `bullet3-api-and-scripting` for generic API loop/control questions outside modeling specifics.
- Use `bullet3-build-and-install` when model loading fails due install/build environment issues.
- Use `bullet3-simulation-workflows` for full scenario orchestration once models are loading.
- Use `bullet3-test` for OpenCL/performance validation, not modeling semantics.

### Triage questions
1. Which format is used: URDF, SDF, MJCF, `.bullet`, or procedural shapes?
2. Are assets local to `pybullet_data`, repo paths, or remote server filesystem?
3. Is the body static (`mass=0`) or dynamic, and are inertia/mass assumptions explicit?
4. Are default joint motors intended or should joints be freely driven?
5. Do you need reduced coordinates (default) or experimental maximal coordinates?
6. Are concave meshes being used on moving bodies (unsupported pattern)?

### Canonical workflow
1. Start from Quickstart sections for `loadURDF`, `loadSDF`, `loadMJCF`, `createCollisionShape`, and `createMultiBody`.
2. Register data path (`pybullet_data.getDataPath()`) or provide explicit absolute asset paths.
3. Load model and verify non-negative body ids.
4. Inspect joints (`getNumJoints`, `getJointInfo`) and set explicit motor modes.
5. If procedural, create collision/visual shapes and then instantiate with `createMultiBody`.
6. Apply dynamics overrides (`changeDynamics`) only after body creation and joint checks.
7. Validate contact/pose behavior with short deterministic step loops.
8. Escalate to URDF parser/importer sources for parse/flag-specific behavior.

### Minimal working example
```python
import pybullet as p
import pybullet_data

p.connect(p.DIRECT)
p.setAdditionalSearchPath(pybullet_data.getDataPath())
robot = p.loadURDF("r2d2.urdf", [0, 0, 1], useFixedBase=False)
shape = p.createCollisionShape(p.GEOM_BOX, halfExtents=[0.2, 0.2, 0.2])
box = p.createMultiBody(baseMass=1.0, baseCollisionShapeIndex=shape, basePosition=[1, 0, 1])
for _ in range(120):
    p.stepSimulation()
print("robot", robot, "box", box)
p.disconnect()
```

### Pitfalls and fixes
- Relative file not found: set additional search path or pass absolute path resolved on server side.
- Robot doesn’t move as expected: disable/reconfigure default joint motors via `setJointMotorControl2`.
- Dynamic concave mesh instability: use concave-trimesh only for static terrain-like bodies.
- Unexpected inertia/behavior: set appropriate URDF flags if you need inertia from file.
- Maximal coordinates confusion: keep default reduced-coordinate mode unless explicitly needed.
- Mixed asset roots in scripts: standardize path handling (`pybullet_data` vs repo-relative paths).

### Convergence and validation checks
- All model load calls return valid non-negative ids.
- Joint count and names match expected robot schema.
- Bodies settle/fall plausibly under gravity in a short deterministic run.
- Contact behavior appears for intended collision pairs.
- Reloading same asset path in a fresh simulation yields consistent ids/order and behavior.

## Scope
- Handle model file loading, procedural body creation, and model parameterization.
- Prioritize documented loader semantics before parser internals.

## Primary documentation references
- `README.md`
- `docs/pybullet_quickstart_guide/PyBulletQuickstartGuide.md.html`
- `examples/pybullet/gym/pybullet_data/__init__.py`
- `examples/pybullet/gym/pybullet_data/differential/modelorigin.txt`
- `examples/pybullet/examples/createObstacleCourse.py`
- `examples/pybullet/examples/createMultiBodyLinks.py`
- `examples/pybullet/examples/createVisualShape.py`

## Workflow
- Start with the primary references above.
- If details are missing, inspect `references/doc_map.md`.
- Escalate to `references/source_map.md` for parser/importer/source behavior.
- Cite file paths used for each modeling choice.

## Tutorials and examples
- `examples/pybullet/examples`
- `examples/pybullet/gym/pybullet_data`

## Test references
- `examples/pybullet/unittests/unittests.py`
- `examples/pybullet/unittests/userDataTest.py`

## Optional deeper inspection
- `examples/Importers/ImportURDFDemo`
- `examples/SharedMemory`
- `src`

## Source entry points for unresolved issues
- `examples/Importers/ImportURDFDemo/BulletUrdfImporter.cpp` (URDF file resolution and import flags)
- `examples/Importers/ImportURDFDemo/UrdfParser.cpp` (URDF XML parsing defaults and transform handling)
- `examples/Importers/ImportURDFDemo/URDF2Bullet.cpp` (URDF-to-Bullet conversion path)
- `examples/pybullet/pybullet.c` (`loadURDF`, `loadSDF`, `loadMJCF`, `createCollisionShape`, `createMultiBody` bindings)
- `examples/SharedMemory/PhysicsServerCommandProcessor.cpp` (server-side load command handling)
- `examples/pybullet/gym/pybullet_data/__init__.py` (data-path helper)
- `examples/pybullet/gym/pybullet_data/r2d2.urdf` (canonical robot asset)
- `examples/pybullet/gym/pybullet_data/plane.urdf` (baseline ground asset)
- Prefer targeted search: `rg -n "loadURDF|createCollisionShape|createMultiBody|URDF_USE_" examples/pybullet/pybullet.c examples/Importers/ImportURDFDemo`.
