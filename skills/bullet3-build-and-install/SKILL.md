---
name: bullet3-build-and-install
description: Use this skill for Bullet3/Bullet Physics build, install, and packaging work across CMake, premake, and PyBullet Python builds, including toolchain failure triage.
---

# bullet3: Build and Install

## High-Signal Playbook
### Route conditions
- Use `bullet3-api-and-scripting` for runtime Python API behavior (`connect`, `loadURDF`, control loops).
- Use `bullet3-simulation-workflows` for scene/run reproducibility tuning after binaries already build.
- Use `bullet3-test` for OpenCL and multithreading performance validation.
- Stay docs-first: `README.md` and `docs/latex/building.tex` before source-level CMake surgery.

### Triage questions
1. Which target are you building: C++ libs/demos, PyBullet module, or both?
2. Which OS/toolchain is in scope (Linux/macOS/Windows; GCC/Clang/MSVC)?
3. Do you need Python bindings from source (`BUILD_PYBULLET`) or just `pip install pybullet`?
4. Are OpenGL/VR/OpenCL features required, or is headless CPU simulation enough?
5. Are failures at configure time, compile/link time, or runtime import/load time?
6. Are you mixing premake and CMake outputs in one build directory?

### Canonical workflow
1. Confirm prerequisites from `README.md`: compiler, CMake, Python, and NumPy for PyBullet.
2. Pick one build system per build tree.
3. For Linux/macOS PyBullet builds, prefer CMake flow from `build_cmake_pybullet_double.sh` and `CMakeLists.txt`.
4. Configure with explicit options (for example `BUILD_PYBULLET`, `BUILD_PYBULLET_NUMPY`, `USE_DOUBLE_PRECISION`, `BUILD_UNIT_TESTS`).
5. Build and run a smoke binary (`App_HelloWorld` or `App_ExampleBrowser`).
6. Verify Python module load (`import pybullet`) and basic URDF load.
7. On Windows, use the provided batch scripts for premake/CMake bootstrap and Python include/lib wiring.
8. Escalate to `references/source_map.md` for option-level behavior or packaging edge cases.

### Minimal working example
```bash
cmake -S . -B build \
  -DBUILD_PYBULLET=ON \
  -DBUILD_PYBULLET_NUMPY=ON \
  -DUSE_DOUBLE_PRECISION=ON \
  -DCMAKE_BUILD_TYPE=Release
cmake --build build -j
python -c "import pybullet as p; c=p.connect(p.DIRECT); print(c); p.disconnect()"
```

### Pitfalls and fixes
- Linux PyBullet with premake-only flow: use CMake for PyBullet builds (`README.md` notes Linux mixed static/shared issues).
- Python mismatch in CMake: set matching include/lib (see `BUILD_PYBULLET` block in `CMakeLists.txt`).
- NumPy features missing: enable/install NumPy and `BUILD_PYBULLET_NUMPY`.
- OpenGL window/link failures: ensure OpenGL deps installed and detected (`examples/ExampleBrowser/CMakeLists.txt`).
- Windows VR/OpenVR DLL confusion: follow copy logic in `build_visual_studio_vr_pybullet_double*.bat`.
- Import works but assets fail: ensure `pybullet_data` and env packages are installed/symlinked (`build_cmake_pybullet_double.sh`, `setup.py`).

### Convergence and validation checks
- `App_ExampleBrowser` starts and can load a demo.
- `App_HelloWorld` runs and prints falling-body positions.
- `python -c "import pybullet"` succeeds in target environment.
- `p.loadURDF("plane.urdf")` returns non-negative id in a direct connection.
- Build flags in `CMakeCache.txt` match intent (`BUILD_PYBULLET`, `USE_DOUBLE_PRECISION`, optional EGL/OpenCL flags).

## Scope
- Handle Bullet3 build, installation, packaging, and toolchain setup issues.
- Prioritize documented build paths before custom edits.

## Primary documentation references
- `README.md`
- `docs/latex/building.tex`
- `docs/latex/helloworld.tex`
- `CMakeLists.txt`
- `examples/pybullet/CMakeLists.txt`
- `setup.py`
- `build_cmake_pybullet_double.sh`
- `build_visual_studio_vr_pybullet_double.bat`
- `build_visual_studio_vr_pybullet_double_cmake.bat`
- `build_visual_studio_vr_pybullet_double_dynamic.bat`

## Workflow
- Start with the primary references above.
- If details are missing, inspect `references/doc_map.md` for the complete topic document list.
- Use `references/source_map.md` only when docs/options are insufficient.
- Cite exact file paths used for build decisions.

## Tutorials and examples
- `examples/HelloWorld`
- `examples/BasicDemo`
- `examples/ExampleBrowser`

## Test references
- `test/CMakeLists.txt`
- `examples/pybullet/unittests/unittests.py`

## Optional deeper inspection
- `src`
- `Extras`
- `build3`

## Source entry points for unresolved issues
- `CMakeLists.txt` (global options: `BUILD_PYBULLET`, `BUILD_EGL`, `BULLET2_MULTITHREADING`, install toggles)
- `examples/pybullet/CMakeLists.txt` (PyBullet target wiring and platform link behavior)
- `setup.py` (wheel/sdist extension build flags and packaged data)
- `build_cmake_pybullet_double.sh` (known-good Linux/macOS CMake invocation)
- `build_visual_studio_vr_pybullet_double.bat` (premake + Python include/lib discovery)
- `build_visual_studio_vr_pybullet_double_cmake.bat` (VS CMake generator path)
- `build_visual_studio_vr_pybullet_double_dynamic.bat` (dynamic runtime premake profile)
- `examples/ExampleBrowser/CMakeLists.txt` (GUI/OpenGL dependencies and app target)
- Prefer targeted source search: `rg -n "BUILD_PYBULLET|USE_DOUBLE_PRECISION|BUILD_EGL|BULLET2_MULTITHREADING" CMakeLists.txt examples/pybullet/CMakeLists.txt setup.py`.
