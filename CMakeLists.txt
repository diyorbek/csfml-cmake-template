cmake_minimum_required(VERSION 3.14)
project(csfml_project)

include(FetchContent)

set(SFML_VERSION "2.6.0")

# Remove C++ stdlib flag for C compilation
if(APPLE)
    set(CMAKE_C_FLAGS "${CMAKE_C_FLAGS} -Wno-unused-command-line-argument")
endif()

# Fetch SFML
FetchContent_Declare(
    SFML
    GIT_REPOSITORY https://github.com/SFML/SFML.git
    GIT_TAG "${SFML_VERSION}"
)
FetchContent_MakeAvailable(SFML)

# Configure paths before fetching CSFML
set(SFML_ROOT "${sfml_SOURCE_DIR}")
set(SFML_DIR "${sfml_BINARY_DIR}")
set(SFML_PATH "${sfml_SOURCE_DIR}")
set(SFML_INCLUDE_DIR "${sfml_SOURCE_DIR}/include")
set(SFML_LIBRARY_DIR "${sfml_BINARY_DIR}/lib")
set(SFML_DEPENDENCIES_DIR "${sfml_SOURCE_DIR}/extlibs")

# Create SFML config file that CSFML can find. This overwrites the already existing one because the original one causes conflict.
file(WRITE "${sfml_BINARY_DIR}/SFMLConfig.cmake" 
"set(SFML_VERSION ${SFML_VERSION})
set(SFML_INCLUDE_DIR \"${SFML_INCLUDE_DIR}\")
set(SFML_LIBRARY_DIR \"${SFML_LIBRARY_DIR}\")
set(SFML_DEPENDENCIES_DIR \"${SFML_DEPENDENCIES_DIR}\")
set(SFML_FOUND TRUE)
")

# Fetch CSFML
FetchContent_Declare(
    CSFML
    GIT_REPOSITORY https://github.com/SFML/CSFML.git
    GIT_TAG "${SFML_VERSION}"
)
FetchContent_MakeAvailable(CSFML)

# Add executable with main.c in root directory
add_executable(${PROJECT_NAME} main.c)

# Link all CSFML libraries
target_link_libraries(${PROJECT_NAME} PRIVATE
    sfml-system
    sfml-window
    sfml-graphics
    sfml-audio
    sfml-network
    csfml-system
    csfml-window
    csfml-graphics
    csfml-audio
    csfml-network
)

# Include directories
target_include_directories(${PROJECT_NAME} PRIVATE
    ${csfml_SOURCE_DIR}/include
)
