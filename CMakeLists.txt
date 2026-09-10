cmake_minimum_required(VERSION 3.20)
project(GoodMsg CXX)

set(CMAKE_CXX_STANDARD 17)

set(CMAKE_CXX_FLAGS "")
set(CMAKE_C_FLAGS "")
set(CMAKE_EXE_LINKER_FLAGS "")

add_executable(GoodMsg main.cpp resource.rc)

target_link_options(GoodMsg PRIVATE
        -mwindows
        -static-libgcc
        -static-libstdc++
)

# Finds the exact folder where CLion keeps libwinpthread-1.dll
get_filename_component(COMPILER_DIR ${CMAKE_CXX_COMPILER} DIRECTORY)

add_custom_command(TARGET GoodMsg POST_BUILD
        COMMAND ${CMAKE_COMMAND} -E copy_if_different
        "${COMPILER_DIR}/libwinpthread-1.dll"
        $<TARGET_FILE_DIR:GoodMsg>
        COMMENT "Copying required runtime DLL to output directory..."
)