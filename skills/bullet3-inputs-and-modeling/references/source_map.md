# bullet3 source map: Inputs and Modeling

Use this map only after exhausting `doc_map.md`.

## Topic query tokens
- `loadURDF`
- `loadSDF`
- `loadMJCF`
- `createCollisionShape`
- `createVisualShape`
- `createMultiBody`
- `URDF_USE_INERTIA_FROM_FILE`
- `useMaximalCoordinates`
- `findResourcePath`
- `user-data`

## Fast source navigation
- `rg -n "pybullet_loadURDF|pybullet_createMultiBody|createCollisionShape|createVisualShape" examples/pybullet/pybullet.c`
- `rg -n "loadURDF|findResourcePath|CUF_|parseTransform|user-data" examples/Importers/ImportURDFDemo`
- `rg -n "CMD_LOAD_URDF|CMD_LOAD_SDF|CMD_LOAD_MJCF" examples/SharedMemory/PhysicsServerCommandProcessor.cpp examples/SharedMemory/PhysicsClientC_API.cpp`

## Suggested source entry points
- `examples/pybullet/pybullet.c` | focus: Python binding arguments/flags for all loader and shape APIs.
- `examples/Importers/ImportURDFDemo/BulletUrdfImporter.cpp` | focus: path resolution and URDF import flag handling.
- `examples/Importers/ImportURDFDemo/UrdfParser.cpp` | focus: transform/material/user-data parsing behavior.
- `examples/Importers/ImportURDFDemo/URDF2Bullet.cpp` | focus: body/joint conversion from parsed URDF model.
- `examples/SharedMemory/PhysicsClientC_API.cpp` | focus: client command init for URDF/SDF/MJCF loading.
- `examples/SharedMemory/PhysicsServerCommandProcessor.cpp` | focus: server-side model load execution.
- `examples/pybullet/examples/createMultiBodyLinks.py` | focus: practical createMultiBody parameter wiring.
- `examples/pybullet/examples/createVisualShape.py` | focus: visual shape + material setup path.
- `examples/pybullet/gym/pybullet_data/r2d2.urdf` | focus: baseline articulated model for loader tests.
- `examples/pybullet/gym/pybullet_data/plane.urdf` | focus: static collision baseline model.
