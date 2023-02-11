cmake_minimum_required(VERSION 3.10) 

# Define the project 
project(ImMacroPadGui)

add_subdirectory("libs")

add_executable(ImMacroPadGui)
target_sources(ImMacroPadGui PUBLIC src/main.cpp)
target_link_libraries(ImMacroPadGui imgui)

