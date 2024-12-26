# CSFML CMake Template

This is a template project for setting up a CSFML (C Binding for SFML) project using CMake. The dependencies are loaded via `FetchContent`.

## Prerequisites

- CMake 3.14 or higher
- A C compiler (e.g., GCC, Clang)

## Getting Started

1. **Clone the repository:**

```sh
git clone https://github.com/diyorbek/csfml-cmake-template.git
cd csfml-cmake-template
```

2. **Create a build directory:**

```sh
mkdir build
cd build
```

3. **Generate the build files using CMake:**

```sh
cmake ..
```

4. **Build the project:**

```sh
cmake --build .
```

5. **Run the executable:**

```sh
# default name is csfml_project
./csfml_project
```

## Acknowledgments

- [SFML](https://www.sfml-dev.org/) - Simple and Fast Multimedia Library
- [CSFML](https://www.sfml-dev.org/download/csfml/) - C Binding for SFML
