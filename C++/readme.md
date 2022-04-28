# CLion toolchains

## Compiler
Use MS VS <= 2019, others are not suppurted. Don't forget to set x64/x86 architecture.

## CMake Toolchains
To include external libraries, use [vcpkg](https://github.com/microsoft/vcpkg) manager. To set it up (after `git clone`):
- Terminal: `vcpkg integrate install`
- Build, execution, deplyment -> CMake -> CMake options set to: `-DCMAKE_TOOLCHAIN_FILE=<path_to>/vcpkg/scripts/buildsystems/vcpkg.cmake`

## VulkanAPI development under CLion
I didn't find some useful guides for this subject (how to set up VulkanAPI for CLion). All of the guides are suitable for MS VS, but it requires some solution settings in VS. It's impossible to set with CLion toolchain.
To link your CMake project with VulkanAPI via CLion toolchain for VS, follow these steps:
- Set up `vcpkg` into your project
- Set architecture at Build, execution, deplyment -> Toolchains -> VS to x64
- Terminal commands (replace `[OS]` with your operating system):
  - `.\vcpkg install glfw3:x64-[OS]`
  - `.\vcpkg install glm:x64-[OS]`
  - `.\vcpkg install vulkan:x64-[OS]` (it's a port, requires VulkanSDK installed)
  - `.\vcpkg install vulkan-headers:x64-[OS]`
- Insert output vcpkg lines (such as `find_package()` and `target_link_libraries()`) to CMakeLists.txt
