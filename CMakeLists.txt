cmake_minimum_required(VERSION 3.20)
if(POLICY CMP0135)
  cmake_policy(SET CMP0135 NEW)
endif()
project(PharmaStock VERSION 1.0 LANGUAGES C CXX)
set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_CXX_EXTENSIONS OFF)
add_library(pharma_core src/Model.cpp)
target_include_directories(pharma_core PUBLIC src)

include(CTest)
if(BUILD_TESTING)
  add_executable(pharma_tests tests/core.cpp)
  target_link_libraries(pharma_tests PRIVATE pharma_core)
  add_test(NAME business_rules COMMAND pharma_tests)
endif()

option(PHARMA_GUI "Build the desktop application" ON)
if(PHARMA_GUI)
  include(FetchContent)
  find_package(OpenGL REQUIRED)
  set(GLFW_BUILD_EXAMPLES OFF CACHE BOOL "" FORCE)
  set(GLFW_BUILD_TESTS OFF CACHE BOOL "" FORCE)
  set(GLFW_BUILD_DOCS OFF CACHE BOOL "" FORCE)
  set(GLFW_INSTALL OFF CACHE BOOL "" FORCE)
  FetchContent_Declare(glfw URL "${CMAKE_CURRENT_SOURCE_DIR}/third_party/glfw-3.4.zip"
    URL_HASH SHA256=8fa1a8dbf379e2070c4bb3e21e89fea57f4341c4c5f1ff704e10cc35b6b2eea6)
  FetchContent_Declare(imgui URL "${CMAKE_CURRENT_SOURCE_DIR}/third_party/imgui-1.91.9b.zip"
    URL_HASH SHA256=df99df1d48c3e1e643a9b29411f28366f59e6c01ada360dfa85eab0800345e79)
  FetchContent_MakeAvailable(glfw imgui)
  add_library(dear_imgui STATIC
    ${imgui_SOURCE_DIR}/imgui.cpp
    ${imgui_SOURCE_DIR}/imgui_draw.cpp
    ${imgui_SOURCE_DIR}/imgui_tables.cpp
    ${imgui_SOURCE_DIR}/imgui_widgets.cpp
    ${imgui_SOURCE_DIR}/backends/imgui_impl_glfw.cpp
    ${imgui_SOURCE_DIR}/backends/imgui_impl_opengl3.cpp)
  target_include_directories(dear_imgui PUBLIC ${imgui_SOURCE_DIR} ${imgui_SOURCE_DIR}/backends)
  target_link_libraries(dear_imgui PUBLIC glfw OpenGL::GL)
  add_executable(PharmaStock MACOSX_BUNDLE src/main.cpp src/GUI.cpp)
  set_target_properties(PharmaStock PROPERTIES
    MACOSX_BUNDLE_GUI_IDENTIFIER edu.cs2003.pharmastock
    MACOSX_BUNDLE_BUNDLE_NAME PharmaStock
    MACOSX_BUNDLE_SHORT_VERSION_STRING 1.0
    MACOSX_BUNDLE_BUNDLE_VERSION 1)
  target_compile_definitions(PharmaStock PRIVATE GL_SILENCE_DEPRECATION)
  target_link_libraries(PharmaStock PRIVATE pharma_core dear_imgui)
endif()
