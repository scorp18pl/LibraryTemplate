cmake_minimum_required(VERSION 3.15)
set(CMAKE_CXX_STANDARD 20)

project(LibraryName VERSION 0.3.0 DESCRIPTION "a general purpose c++ library")
string(TOLOWER ${PROJECT_NAME} PROJECT_EXECUTABLE_NAME)

include(GNUInstallDirs)

option(BUILD_TESTS "Build tests" OFF)

if (BUILD_TESTS)
    include(FetchContent)
    FetchContent_Declare(
            googletest
            GIT_REPOSITORY https://github.com/google/googletest.git
            GIT_TAG release-1.11.0
    )
    FetchContent_MakeAvailable(googletest)
endif ()

include(${CMAKE_CURRENT_SOURCE_DIR}/include_files.cmake)
include(${CMAKE_CURRENT_SOURCE_DIR}/source_files.cmake)

add_library(${PROJECT_EXECUTABLE_NAME} STATIC ${SOURCE_FILES} ${INCLUDE_FILES})

target_include_directories(${PROJECT_EXECUTABLE_NAME}
        PUBLIC ${CMAKE_CURRENT_SOURCE_DIR}/Include
        PRIVATE ${CMAKE_CURRENT_SOURCE_DIR}/Source ${CMAKE_CURRENT_SOURCE_DIR}/3rdParty/Include
        )

if (CMAKE_BUILD_TYPE STREQUAL "Debug")
    if (MSVC)
        target_compile_options(${PROJECT_EXECUTABLE_NAME} PRIVATE /W4 /WX)
    else ()
        target_compile_options(${PROJECT_EXECUTABLE_NAME} PRIVATE -Wall -Wextra -Werror)
    endif ()
endif ()

target_link_libraries(${PROJECT_EXECUTABLE_NAME} PRIVATE)

set_target_properties(${PROJECT_EXECUTABLE_NAME} PROPERTIES VERSION ${PROJECT_VERSION})

configure_file(${CMAKE_CURRENT_SOURCE_DIR}/Tools/${PROJECT_EXECUTABLE_NAME}.pc.in
        ${CMAKE_CURRENT_SOURCE_DIR}/Tools/${PROJECT_EXECUTABLE_NAME}.pc @ONLY
        )

install(DIRECTORY Include DESTINATION ${CMAKE_INSTALL_INCLUDEDIR})

install(TARGETS ${PROJECT_EXECUTABLE_NAME}
        LIBRARY DESTINATION ${CMAKE_INSTALL_LIBDIR}
        )

install(FILES ${CMAKE_BINARY_DIR}/Tools/${PROJECT_EXECUTABLE_NAME}.pc
        DESTINATION ${CMAKE_INSTALL_DATAROOTDIR}/pkgconfig)

if (BUILD_TESTS)
    add_subdirectory(Tests)
endif ()
