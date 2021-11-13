cmake_minimum_required(VERSION 3.1)
set(project_name "tray_icon_sdk")

if(TARGET ${project_name})
    return()
endif()

project(${project_name} C CXX)

if(NOT (WIN32 OR WIN64))
  message(FATAL_ERROR "This SDK is for Windows only.")
endif()

file(GLOB_RECURSE src
  ${CMAKE_CURRENT_LIST_DIR}/impl/*.h
  ${CMAKE_CURRENT_LIST_DIR}/impl/*.c
  ${CMAKE_CURRENT_LIST_DIR}/impl/*.cc
  ${CMAKE_CURRENT_LIST_DIR}/impl/*.cpp
)

add_library(${project_name} STATIC ${src})

target_include_directories(${project_name}
	PUBLIC "${CMAKE_CURRENT_LIST_DIR}/include")

add_library(code_project::tray_icon_sdk ALIAS ${project_name})