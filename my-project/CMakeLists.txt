# General
if(NOT DEFINED CMAKE_MINIMUM_REQUIRED_VERSION)
  cmake_minimum_required(VERSION 3.12)
endif()
project(my-project VERSION 1.0.0)

# Source files (relative to the project's "src" folder)
set(
    SOURCES
    main.cpp
)

# Header files (relative to the project's "include" folder)
set(
    HEADERS
)

# Include directories
set(
    INCLUDES
    ${CURRENT_SOURCE_DIR}/include
)

# Compiler definitions
set(
    DEFINES

)

# Compiler options
set(
    OPTIONS

)
    
# Project setup
list(TRANSFORM SOURCES PREPEND "src/")
list(TRANSFORM HEADERS PREPEND "include/")
add_executable(${PROJECT_NAME})
target_sources(${PROJECT_NAME} PRIVATE ${SOURCES} ${HEADERS})
target_include_directories(${PROJECT_NAME} PRIVATE ${INCLUDES})
target_compile_definitions(${PROJECT_NAME} PRIVATE ${DEFINES})
target_compile_options(${PROJECT_NAME} PRIVATE ${OPTIONS})
set_target_properties( ${PROJECT_NAME} PROPERTIES RUNTIME_OUTPUT_DIRECTORY "bin")