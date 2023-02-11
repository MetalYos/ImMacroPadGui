# Add GLFW3 subdirectory
set (GLFW_DIR ${CMAKE_CURRENT_LIST_DIR}/glfw)
set(BUILD_SHARED_LIBS OFF CACHE BOOL "" FORCE)
set(GLFW_BUILD_EXAMPLES ON CACHE BOOL "" FORCE)
set(GLFW_BUILD_TESTS OFF CACHE BOOL "" FORCE)
set(GLFW_BUILD_DOCS ON CACHE BOOL "" FORCE)
add_subdirectory(${GLFW_DIR})

# Add ImGui subdirectory
set(IMGUI_DIR ${CMAKE_CURRENT_LIST_DIR}/imgui)
add_library(imgui STATIC)
target_sources(imgui
    PRIVATE
    ${IMGUI_DIR}/imgui_demo.cpp
    ${IMGUI_DIR}/imgui_draw.cpp
    ${IMGUI_DIR}/imgui_tables.cpp
    ${IMGUI_DIR}/imgui_widgets.cpp
    ${IMGUI_DIR}/imgui.cpp
   
    PRIVATE
    #specific bindings
    ${IMGUI_DIR}/backends/imgui_impl_glfw.cpp
    ${IMGUI_DIR}/backends/imgui_impl_opengl3.cpp
)
target_include_directories(imgui
    PUBLIC ${IMGUI_DIR}
    PUBLIC ${IMGUI_DIR}/backends
    PUBLIC ${GLFW_DIR}/include
)
find_package(OpenGL REQUIRED)
target_link_libraries(imgui PUBLIC ${OPENGL_LIBRARIES})
target_link_libraries(imgui PUBLIC glfw ${CMAKE_DL_LIBS})
