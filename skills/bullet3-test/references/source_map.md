# bullet3 source map: Test

Use this map only after exhausting `doc_map.md`.

## Topic query tokens
- `createContextFromType`
- `getNumPlatforms`
- `compileCLKernelFromString`
- `enable_experimental_opencl`
- `allow_opencl_cpu`
- `BT_THREADSAFE`
- `Multithreaded Demo`
- `stepSimulation`
- `radix sort`
- `parallel primitives`

## Fast source navigation
- `rg -n "createContextFromType|getNumPlatforms|getNumDevices|compileCLKernelFromString" src/Bullet3OpenCL test/OpenCL`
- `rg -n "enable_experimental_opencl|initOpenCLExampleEntries|OpenCL \(experimental\)" examples/ExampleBrowser`
- `rg -n "Multithreaded Demo|BT_THREADSAFE|runTask|waitForAllTasks" examples/MultiThreadedDemo examples/MultiThreading src/LinearMath`

## Suggested source entry points
- `src/Bullet3OpenCL/Initialize/b3OpenCLUtils.cpp` | focus: platform enumeration and context creation failure points.
- `src/Bullet3OpenCL/CMakeLists.txt` | focus: OpenCL library target and install/link behavior.
- `src/Bullet3OpenCL/RigidBody/b3GpuRigidBodyPipeline.cpp` | focus: GPU rigid-body step pipeline.
- `test/OpenCL/BasicInitialize/testInitOpenCL.cpp` | focus: minimum expected OpenCL capabilities.
- `test/OpenCL/AllBullet3Kernels/initCL.h` | focus: device/platform command-line overrides.
- `test/OpenCL/AllBullet3Kernels/testCompileBullet3BroadphaseKernels.cpp` | focus: kernel-by-kernel compile checks.
- `examples/OpenCL/rigidbody/GpuRigidBodyDemo.cpp` | focus: demo initialization, scene setup, and runtime update path.
- `examples/OpenCL/CommonOpenCL/CommonOpenCLBase.h` | focus: OpenCL init/teardown lifecycle used by demos.
- `examples/ExampleBrowser/OpenGLExampleBrowser.cpp` | focus: OpenCL feature gating and startup flags.
- `examples/MultiThreadedDemo/MultiThreadedDemo.cpp` | focus: threaded scene setup, stepping, and benchmark controls.
- `examples/MultiThreading/main.cpp` | focus: bare thread-support API behavior.
