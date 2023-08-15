# LibraryName

<h1 align="center">
  <img src="Media/library_logo.png" alt="LibraryName">
</h1>

Library description.

## Features

## Installation prerequisites
The LibraryName library depends on these ...:

You can install them with the following bash commands:
```Bash
# commands
```
## Library installation
1. Clone the repository.
    ```bash
    git clone https://github.com/scorp18pl/LibraryName.git
    cd LibraryName
    ```
2. Create and proceed to the build directory.
    ```bash
    mkdir build && cd build
    ```
3. Install the library.
    ```bash
    cmake .. -DCMAKE_BUILD_TYPE=Release
    sudo make install
    ```

## Using the library (CMake)
In your project's CMakeLists.txt file:
1. Find the library.
    ```CMake
    find_library(LibraryName LibraryName)
    ```
2. Link the found library with your target.
    ```CMake
    target_link_libraries(<target_name> ${LibraryName})
    ```
