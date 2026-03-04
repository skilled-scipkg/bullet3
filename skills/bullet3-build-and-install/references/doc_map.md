# bullet3 documentation map: Build and Install

Curated docs-first map for build, packaging, and install triage.

Total docs grouped in this topic: 12

## File inventory
- `README.md` | scope: recommended install paths, platform notes, CMake/premake commands, PyBullet quickstart pointers.
- `docs/latex/building.tex` | scope: canonical premake/CMake flows across platforms.
- `docs/latex/helloworld.tex` | scope: first compile/link/run validation target.
- `CMakeLists.txt` | scope: global build options and install toggles.
- `examples/pybullet/CMakeLists.txt` | scope: PyBullet target, platform link differences, install destination.
- `examples/CMakeLists.txt` | scope: demo subtree activation and PyBullet subdir gating.
- `examples/ExampleBrowser/CMakeLists.txt` | scope: GUI/OpenGL deps and app target wiring.
- `examples/HelloWorld/CMakeLists.txt` | scope: minimal C++ executable and link order.
- `test/CMakeLists.txt` | scope: unit-test subtree activation.
- `build_cmake_pybullet_double.sh` | scope: known-good Linux/macOS CMake flags and pybullet symlink setup.
- `build_visual_studio_vr_pybullet_double.bat` | scope: premake + Python autodiscovery + VS workflow.
- `setup.py` | scope: setuptools extension build, platform flags, packaged data.
