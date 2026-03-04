# bullet3 source map: Simulation Workflows

Use this map after exhausting `doc_map.md`.

## Topic query tokens
- `stepSimulation`
- `fixed_timestep`
- `start_demo_name`
- `constraint`
- `kinematic`
- `saveState`
- `restoreState`
- `motion_file`
- `num_sim_substeps`
- `deterministicOverlappingPairs`

## Fast source navigation
- `rg -n "stepSimulation|setGravity|addRigidBody|addConstraint" examples/HelloWorld examples/Constraints examples/Tutorial examples/RigidBody`
- `rg -n "start_demo_name|fixed_timestep|enable_experimental_opencl" examples/ExampleBrowser/OpenGLExampleBrowser.cpp`
- `rg -n "arg_file|motion_file|num_sim_substeps|calc_reward|is_episode_end" examples/pybullet/gym/pybullet_envs/deep_mimic`

## Suggested source entry points
- `examples/HelloWorld/HelloWorld.cpp` | focus: reference lifecycle and cleanup order.
- `examples/Constraints/ConstraintDemo.cpp` | focus: hinge/slider/6DoF configuration patterns.
- `examples/Tutorial/Dof6ConstraintTutorial.cpp` | focus: solver variants and spring parameter effects.
- `examples/RigidBody/KinematicRigidBodyExample.cpp` | focus: pre-tick kinematic updates and dynamic body interaction.
- `examples/ExampleBrowser/OpenGLExampleBrowser.cpp` | focus: CLI arguments and runtime stepping options.
- `examples/ExampleBrowser/ExampleEntries.cpp` | focus: canonical demo names and categories.
- `examples/pybullet/examples/createObstacleCourse.py` | focus: procedural scene recipe with mixed shapes.
- `examples/pybullet/unittests/saveRestoreStateTest.py` | focus: deterministic snapshot/restore validation.
- `examples/pybullet/gym/pybullet_envs/deep_mimic/testrl.py` | focus: policy test loop and arg-file loading.
- `examples/pybullet/gym/pybullet_data/args/train_humanoid3d_run_args.txt` | focus: training-vs-run parameter deltas.
