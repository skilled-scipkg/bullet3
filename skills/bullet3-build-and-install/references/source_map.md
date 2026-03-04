# bullet3 source map: Build and Install

Use this map after exhausting `doc_map.md`.

## Topic query tokens
- `BUILD_PYBULLET`
- `BUILD_PYBULLET_NUMPY`
- `USE_DOUBLE_PRECISION`
- `BUILD_EGL`
- `BULLET2_MULTITHREADING`
- `BUILD_UNIT_TESTS`
- `BUILD_SHARED_LIBS`
- `PYTHON_INCLUDE_DIR`
- `PYTHON_LIBRARY`
- `INSTALL_LIBS`

## Fast source navigation
- `rg -n "BUILD_PYBULLET|BUILD_EGL|USE_DOUBLE_PRECISION|BULLET2_MULTITHREADING|BUILD_UNIT_TESTS" CMakeLists.txt`
- `rg -n "PYTHON|NUMPY|BT_USE_EGL|package_data" setup.py examples/pybullet/CMakeLists.txt`
- `rg -n "OPENGL|TARGET_LINK_LIBRARIES|ADD_EXECUTABLE\(App_ExampleBrowser" examples/ExampleBrowser/CMakeLists.txt`

## Suggested source entry points
- `CMakeLists.txt` | focus: top-level options and platform branches.
- `examples/pybullet/CMakeLists.txt` | focus: Python extension target and install location.
- `setup.py` | focus: setuptools extension compile flags and packaged resource files.
- `build_cmake_pybullet_double.sh` | focus: repeatable cmake invocation + post-build pybullet symlinks.
- `build_visual_studio_vr_pybullet_double.bat` | focus: premake feature flags and Python include/lib selection.
- `build_visual_studio_vr_pybullet_double_cmake.bat` | focus: VS generator and explicit Python library wiring.
- `build_visual_studio_vr_pybullet_double_dynamic.bat` | focus: dynamic-runtime premake profile.
- `examples/ExampleBrowser/CMakeLists.txt` | focus: OpenGL and app target dependency graph.
- `examples/CMakeLists.txt` | focus: demo and pybullet subtree inclusion logic.
- `test/CMakeLists.txt` | focus: test subprojects enabled by `BUILD_UNIT_TESTS`.
