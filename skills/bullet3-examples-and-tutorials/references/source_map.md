# bullet3 source map: Examples and Tutorials

Use this map only after exhausting `doc_map.md`.

## Topic query tokens
- `HelloWorld`
- `ConstraintDemo`
- `Dof6`
- `Kinematic`
- `ExampleEntries`
- `start_demo_name`
- `Minitaur`
- `DeepMimic`
- `Racecar`
- `stepSimulation`

## Fast source navigation
- `rg -n "B3_STANDALONE_EXAMPLE|CreateFunc|ExampleEntry" examples/HelloWorld examples/Constraints examples/Tutorial examples/RigidBody examples/ExampleBrowser`
- `rg -n "connect\(|loadURDF|setJointMotorControl2|stepSimulation" examples/pybullet/examples`
- `rg -n "env\.step|gym\.make|arg_file|motion_file" examples/pybullet/gym/pybullet_envs`

## Suggested source entry points
- `examples/HelloWorld/HelloWorld.cpp` | focus: minimal lifecycle and expected simulation output pattern.
- `examples/BasicDemo/BasicExample.cpp` | focus: compact dynamic-world baseline.
- `examples/Constraints/ConstraintDemo.cpp` | focus: constraint setup variations and limit parameters.
- `examples/Tutorial/Tutorial.cpp` | focus: educational physics implementation patterns.
- `examples/Tutorial/Dof6ConstraintTutorial.cpp` | focus: solver/constraint tuning examples.
- `examples/RigidBody/KinematicRigidBodyExample.cpp` | focus: kinematic pre-tick updates.
- `examples/ExampleBrowser/ExampleEntries.cpp` | focus: authoritative demo names for routing/CLI selection.
- `examples/pybullet/examples/hello_pybullet.py` | focus: minimal scripting baseline.
- `examples/pybullet/examples/createObstacleCourse.py` | focus: richer procedural scene example.
- `examples/pybullet/gym/pybullet_envs/examples/minitaur_gym_env_example.py` | focus: gym robotics entry path.
- `examples/pybullet/gym/pybullet_envs/deep_mimic/testrl.py` | focus: deep-mimic run loop from arg files.
