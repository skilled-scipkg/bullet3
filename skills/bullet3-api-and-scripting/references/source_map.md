# bullet3 source map: API and Scripting

Use this map only after exhausting `doc_map.md`.

## Topic query tokens
- `connect`
- `disconnect`
- `loadURDF`
- `stepSimulation`
- `setRealTimeSimulation`
- `setJointMotorControl2`
- `createMultiBody`
- `getCameraImage`
- `SHARED_MEMORY`
- `TCP`
- `UDP`

## Fast source navigation
- `rg -n "pybullet_connectPhysicsServer|pybullet_loadURDF|pybullet_stepSimulation|pybullet_setRealTimeSimulation|pybullet_setJointMotorControl2|pybullet_createMultiBody" examples/pybullet/pybullet.c`
- `rg -n "CMD_LOAD_URDF|CMD_STEP_FORWARD_SIMULATION|setGravity|loadURDF|loadSDF|loadMJCF" examples/SharedMemory/PhysicsClientC_API.cpp examples/SharedMemory/PhysicsServerCommandProcessor.cpp`
- `rg -n "register\(|entry_point|BulletEnv" examples/pybullet/gym/pybullet_envs/__init__.py`

## Suggested source entry points
- `examples/pybullet/pybullet.c` | focus: Python binding argument parsing and command dispatch.
- `examples/SharedMemory/PhysicsClientC_API.cpp` | focus: client-side command builder functions.
- `examples/SharedMemory/PhysicsServerCommandProcessor.cpp` | focus: server command execution and world stepping.
- `examples/SharedMemory/PhysicsServerExample.cpp` | focus: server loop, shared-memory key handling, real-time stepping path.
- `examples/Importers/ImportURDFDemo/BulletUrdfImporter.cpp` | focus: URDF file resolution and import flags.
- `examples/Importers/ImportURDFDemo/UrdfParser.cpp` | focus: transform/material parsing and user-data tags.
- `examples/pybullet/examples/hello_pybullet.py` | focus: minimal API call order.
- `examples/pybullet/gym/pybullet_envs/__init__.py` | focus: available gym IDs and entry points.
- `examples/pybullet/gym/pybullet_envs/env_bases.py` | focus: env reset/render/physics-client lifecycle.
- `examples/pybullet/unittests/unittests.py` | focus: expected API invariants in direct/shared-memory modes.
