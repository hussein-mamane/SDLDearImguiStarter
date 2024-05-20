cmake_minimum_required(VERSION 3.2)

project(sdlgui1)

cmake_policy(SET CMP0072 NEW)

set(SDL2_LIBRARIES SDL2)
set(IMGUI_LIBRARIES imgui)

set(IMGUI_PATH ${CMAKE_SOURCE_DIR}/imgui)
file(GLOB IMGUI_GLOB
        ${IMGUI_PATH}/imgui.h
        ${IMGUI_PATH}/imgui.cpp
        ${IMGUI_PATH}/imconfig.h
        ${IMGUI_PATH}/imgui_demo.cpp
        ${IMGUI_PATH}/imgui_draw.cpp
        ${IMGUI_PATH}/imgui_internal.h
        ${IMGUI_PATH}/imstb_rectpack.h
        ${IMGUI_PATH}/imstb_textedit.h
        ${IMGUI_PATH}/imstb_truetype.h
        ${IMGUI_PATH}/imgui_tables.cpp
        ${IMGUI_PATH}/imgui_widgets.cpp

        # specific bindings...
        ${IMGUI_PATH}/backends/imgui_impl_sdl2.h
        ${IMGUI_PATH}/backends/imgui_impl_sdl2.cpp
        ${IMGUI_PATH}/backends/imgui_impl_sdlrenderer2.h
        ${IMGUI_PATH}/backends/imgui_impl_sdlrenderer2.cpp)

# for files used in building of libimgui.a inside the build folder to detect its include
include_directories(${CMAKE_SOURCE_DIR}/imgui)
include_directories(${CMAKE_SOURCE_DIR}/imgui/backends)

#for libsdl2-dev in linux to be found by imgui doing #include <SDL.h>
include_directories(/usr/include/SDL2)
#find_package(OpenGL REQUIRED) ${OPENGL_LIBRARIES} 

add_library("imgui" STATIC ${IMGUI_GLOB}) # build a libimgui.a
add_executable(${PROJECT_NAME} main.cpp)
target_link_libraries(${PROJECT_NAME} ${SDL2_LIBRARIES} ${IMGUI_LIBRARIES} )
