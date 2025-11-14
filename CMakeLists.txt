cmake_minimum_required(VERSION 3.10)

project(MyLibrary_CPP VERSION 1.0.0)

set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_POSITION_INDEPENDENT_CODE ON)

# Detect all .cpp files in src/
file(GLOB SRC_FILES "src/*.cpp")

# ---- Shared Library ----
add_library(MyLibrary_CPP SHARED ${SRC_FILES})

target_include_directories(MyLibrary_CPP
    PUBLIC ${CMAKE_CURRENT_SOURCE_DIR}/src
)

# ---- Static Library ----
add_library(MyLibrary_CPP_static STATIC ${SRC_FILES})

target_include_directories(MyLibrary_CPP_static
    PUBLIC ${CMAKE_CURRENT_SOURCE_DIR}/src
)

# Output names (no "lib" prefix on Windows)
set_target_properties(MyLibrary_CPP PROPERTIES OUTPUT_NAME "MyLibrary_CPP")
set_target_properties(MyLibrary_CPP_static PROPERTIES OUTPUT_NAME "MyLibrary_CPP")

# Install rules (optional)
install(TARGETS MyLibrary_CPP MyLibrary_CPP_static
        LIBRARY DESTINATION lib
        ARCHIVE DESTINATION lib
        RUNTIME DESTINATION bin)

install(DIRECTORY src/ DESTINATION include FILES_MATCHING PATTERN "*.h")
