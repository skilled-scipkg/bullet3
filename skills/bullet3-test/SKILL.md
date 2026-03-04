---
name: bullet3-test
description: Use this skill for Bullet3 OpenCL and multithreading validation, including platform prerequisites, runtime checks, and performance-focused troubleshooting.
---

# bullet3: Test

## High-Signal Playbook
### Route conditions
- Use `bullet3-build-and-install` if OpenCL/multithread targets are not compiling.
- Use `bullet3-simulation-workflows` for general scene runbooks unrelated to OpenCL/threading.
- Use `bullet3-api-and-scripting` for PyBullet API usage questions.
- Keep docs-first: start with `README.md` and `docs/latex/intro.tex` before kernel/source deep dives.

### Triage questions
1. Is OpenCL required, and do you have a discrete GPU with updated OpenCL drivers?
2. Are you validating initialization only, kernel compilation, or full OpenCL demo runtime?
3. Do you need CPU OpenCL fallback (`--allow_opencl_cpu`) for diagnostics?
4. Is the target run path gtest/premake tests, ExampleBrowser OpenCL demos, or both?
5. Is multithreading behavior required (`BT_THREADSAFE`/multithread demo availability)?
6. Is the issue functional correctness (crash/failure) or performance regression?

### Canonical workflow
1. Confirm prerequisites in `README.md` (OpenCL is experimental and driver-sensitive).
2. Build with tests/demos enabled (`BUILD_UNIT_TESTS`, `BUILD_BULLET2_DEMOS`, `BUILD_BULLET3`).
3. Use `test/OpenCL/BasicInitialize/testInitOpenCL.cpp` expectations as baseline (`numPlatforms > 0`, context/queue creation).
4. Use `test/OpenCL/AllBullet3Kernels/*` compile tests to isolate kernel-level driver failures.
5. Run ExampleBrowser with `--enable_experimental_opencl` to expose OpenCL demo entries.
6. Validate multithreaded behavior via `MultiThreading` and `Multithreaded Demo` entries.
7. If failing, inspect OpenCL context creation and selected platform/device path.
8. Escalate to source map for kernel pipeline or scheduler internals.

### Minimal working example
```bash
cmake -S . -B build -DBUILD_BULLET3=ON -DBUILD_UNIT_TESTS=ON -DBUILD_BULLET2_DEMOS=ON
cmake --build build -j
./bin/App_ExampleBrowser --enable_experimental_opencl --start_demo_name="Pair Bench"
./bin/App_ExampleBrowser --start_demo_name="Multithreaded Demo"
```

### Pitfalls and fixes
- `No OpenCL capable GPU found`: install vendor OpenCL driver/runtime and verify platform visibility.
- Kernel compile failures on specific drivers: run individual `AllBullet3Kernels` tests to identify failing kernel family.
- OpenCL demos missing in UI: pass `--enable_experimental_opencl`.
- CPU OpenCL performance/compatibility issues: only use CPU mode for diagnostics, not performance conclusions.
- Multithreaded demo absent: confirm threaded build flags and scheduler support.
- GPU scene OOM/assert in OpenCL demos: reduce object counts or renderer capacity.

### Convergence and validation checks
- OpenCL init path reports `Num Platforms > 0` and at least one device.
- Basic queue/context creation succeeds (no non-success OpenCL error codes).
- ExampleBrowser shows OpenCL category and runs `Pair Bench`/`Box-Box` without immediate failure.
- Multithread demos advance with stable stepping and no deadlock.
- Repeated runs give consistent pass/fail pattern on same driver/hardware.

## Scope
- Handle OpenCL and multithread test/risk triage for Bullet3.
- Prioritize deterministic diagnostics over broad tuning advice.

## Primary documentation references
- `README.md`
- `docs/latex/intro.tex`
- `docs/GPU_rigidbody_using_OpenCL.pdf`
- `test/OpenCL/BasicInitialize/testInitOpenCL.cpp`
- `test/OpenCL/AllBullet3Kernels/initCL.h`
- `test/OpenCL/AllBullet3Kernels/testCompileBullet3BroadphaseKernels.cpp`
- `examples/ExampleBrowser/OpenGLExampleBrowser.cpp`
- `examples/ExampleBrowser/ExampleEntries.cpp`
- `examples/MultiThreadedDemo/MultiThreadedDemo.cpp`
- `examples/MultiThreading/main.cpp`

## Workflow
- Start with docs and test harness references above.
- If details are missing, inspect `references/doc_map.md`.
- Use `references/source_map.md` for platform/device selection and kernel execution internals.
- Cite exact file paths for each diagnosis claim.

## Tutorials and examples
- `examples/OpenCL`
- `examples/MultiThreadedDemo`
- `examples/MultiThreading`
- `examples/ExampleBrowser`

## Test references
- `test/OpenCL/BasicInitialize`
- `test/OpenCL/AllBullet3Kernels`
- `test/OpenCL/ParallelPrimitives`
- `test/OpenCL/RadixSortBenchmark`

## Optional deeper inspection
- `src/Bullet3OpenCL`
- `src/LinearMath`
- `examples/OpenCL/CommonOpenCL`

## Source entry points for unresolved issues
- `src/Bullet3OpenCL/Initialize/b3OpenCLUtils.cpp` (platform/device/context setup and error paths)
- `src/Bullet3OpenCL/CMakeLists.txt` (OpenCL target composition and linkage behavior)
- `test/OpenCL/BasicInitialize/testInitOpenCL.cpp` (expected OpenCL init assertions)
- `test/OpenCL/AllBullet3Kernels/initCL.h` (CLI device/platform selection and CPU OpenCL toggle)
- `test/OpenCL/AllBullet3Kernels/testCompileBullet3BroadphaseKernels.cpp` (kernel compile smoke coverage)
- `examples/OpenCL/rigidbody/GpuRigidBodyDemo.cpp` (OpenCL rigid-body pipeline setup and step loop)
- `examples/OpenCL/CommonOpenCL/CommonOpenCLBase.h` (context/queue lifecycle in demos)
- `examples/ExampleBrowser/OpenGLExampleBrowser.cpp` (enabling experimental OpenCL and CLI flags)
- `examples/MultiThreadedDemo/MultiThreadedDemo.cpp` (threaded rigid-body benchmark scene)
- `examples/MultiThreading/main.cpp` (cross-platform thread support primitives)
- Prefer targeted search: `rg -n "enable_experimental_opencl|createContextFromType|BT_THREADSAFE|stepSimulation" examples src test/OpenCL`.
