# bullet3 documentation map: Test

Curated docs-first map for OpenCL and multithread validation.

Total docs grouped in this topic: 10

## File inventory
- `README.md` | scope: OpenCL requirements, limitations, and expectations.
- `docs/latex/intro.tex` | scope: ExampleBrowser OpenCL status and `--enable_experimental_opencl` note.
- `docs/GPU_rigidbody_using_OpenCL.pdf` | scope: GPU rigid-body architecture context.
- `test/OpenCL/BasicInitialize/testInitOpenCL.cpp` | scope: baseline OpenCL initialization assertions.
- `test/OpenCL/AllBullet3Kernels/initCL.h` | scope: CLI control for platform/device/cpu-opencl selection.
- `test/OpenCL/AllBullet3Kernels/testCompileBullet3BroadphaseKernels.cpp` | scope: broadphase kernel compile checks.
- `examples/ExampleBrowser/OpenGLExampleBrowser.cpp` | scope: runtime OpenCL feature flag handling.
- `examples/ExampleBrowser/ExampleEntries.cpp` | scope: OpenCL and multithread demo registry.
- `examples/MultiThreadedDemo/MultiThreadedDemo.cpp` | scope: high-load threaded demo behavior.
- `examples/MultiThreading/main.cpp` | scope: thread support primitive usage sample.
