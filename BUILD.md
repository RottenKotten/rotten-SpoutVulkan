## Building

### Requirements

* Windows
* CMake 3.15+
* C++20 compatible compiler
* Vulkan SDK
* Git

Note: the Vulkan SDK is located using CMake’s standard discovery mechanisms, as is common in many other projects, while Spout2 is included as a submodule.

Clone recursively:

```bash
git clone --recursive https://github.com/RottenKotten/rotten-SpoutVulkan.git
cd rotten-SpoutVulkan
```

If the repository was cloned without submodules:

```bash
git submodule update --init --recursive
```

### Build with Visual Studio

Configure:

```powershell
cmake -S . -B build -G "Visual Studio 17 2022" -A x64
```

Build Debug:

```powershell
cmake --build build --config Debug
```

Build Release:

```powershell
cmake --build build --config Release
```

The resulting static library is built as:

```text
SpoutVulkan
```

### Build with Ninja

Configure:

```powershell
cmake -S . -B build -G Ninja -DCMAKE_BUILD_TYPE=Release
```

Build:

```powershell
cmake --build build
```

### Use from another CMake project

Add the repository as a subdirectory:

```cmake
add_subdirectory(path/to/rotten-SpoutVulkan)

target_link_libraries(MyTarget PRIVATE
    SpoutVulkan::SpoutVulkan
)
```

The library exposes its public headers automatically:

```cpp
#include <SpoutVK.h>
```

If the parent project already provides a `Spout_static` target, rotten-SpoutVulkan will reuse it instead of building its bundled Spout2 copy.
