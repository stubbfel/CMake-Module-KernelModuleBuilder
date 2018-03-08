cmake_minimum_required(VERSION 2.6)
include("../BuildKernelModule.cmake")

project ("example_modules")

set(CMAKE_C_FLAGS  "${CMAKE_CXX_FLAGS} -Wall -Wextra -Werror -pedantic -Weverything")
if(NOT KERNEL_DIR)
    Set(KERNEL_DIR "/lib/modules/${CMAKE_SYSTEM_VERSION}/build" )
endif()

# create LKMPG examples

## find example folder
file(GLOB LKMPG_Folders
    "${PROJECT_SOURCE_DIR}/LKMPG/[0-9][0-9][0-9].*"
    "${PROJECT_SOURCE_DIR}/LKMPG/[0-9][0-9].*"
    "${PROJECT_SOURCE_DIR}/LKMPG/[0-9].*")
list(GET LKMPG_Folders 0 LKMPG_Folder)
set(LKMPG_Example_Folder "${LKMPG_Folder}/examples/")

include_directories("${LKMPG_Example_Folder}")

## enable debug mode
add_definitions(-DDEBUG)

## create each c file as own module
file(GLOB LKMPG_files  "${LKMPG_Example_Folder}/*.c")
foreach(module_file ${LKMPG_files})
    string(REGEX MATCH "^.+\\.c$" match_file ${module_file})
    if(NOT ${match_file})
        file(RELATIVE_PATH rel_file "${LKMPG_Example_Folder}" ${module_file} )
        string(REPLACE ".c" "" module_name ${rel_file})
        add_module("${module_name}" "${module_file}" "${KERNEL_DIR}")
    endif()
endforeach()

