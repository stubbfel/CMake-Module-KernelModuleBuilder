# CMake-Module-KernelModuleBuilder

With this cmake module the user can build/create/describe kernel modules in a CMakeLists.txt, in the way like a usespace executable or lib. E.g. see the CMakeLists.txt in example folder.

* `include_directories` - "Add include directories to the build." -> https://cmake.org/cmake/help/latest/command/include_directories.html
    * this cmake module will use the include entries from the `INCLUDE_DIRECTORIES` property (https://cmake.org/cmake/help/latest/prop_dir/INCLUDE_DIRECTORIES.html) of the `${CMAKE_CURRENT_SOURCE_DIR}` directory (https://cmake.org/cmake/help/latest/variable/CMAKE_CURRENT_SOURCE_DIR.html)
* `add_definitions` - "Adds -D define flags to the compilation of source files." -> https://cmake.org/cmake/help/latest/command/add_definitions.html
    * this cmake module will use the definition entries from the `COMPILE_DEFINITIONS` property (https://cmake.org/cmake/help/latest/prop_dir/COMPILE_DEFINITIONS.html) of the `${CMAKE_CURRENT_SOURCE_DIR}` directory (https://cmake.org/cmake/help/latest/variable/CMAKE_CURRENT_SOURCE_DIR.html)
* `add_module` - "create a kernel module target"
    * `function(add_module module_name module_files kernel_dir)`
        * `module_name` - name of the module and target
        * `module_files` - the source and object files of the moudles
        * `kernel_dir` - path to kernelt build enviroment