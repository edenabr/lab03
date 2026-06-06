cmake_minimum_required(VERSION 3.10)

project(lab03)

set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

add_library(formatter STATIC
    ${CMAKE_CURRENT_SOURCE_DIR}/formatter_lib/formatter.cpp
)

target_include_directories(formatter PUBLIC
    ${CMAKE_CURRENT_SOURCE_DIR}/formatter_lib
)

add_library(formatter_ex STATIC
    ${CMAKE_CURRENT_SOURCE_DIR}/formatter_ex_lib/formatter_ex.cpp
)

target_include_directories(formatter_ex PUBLIC
    ${CMAKE_CURRENT_SOURCE_DIR}/formatter_ex_lib
)

target_link_libraries(formatter_ex formatter)

add_library(solver STATIC
    ${CMAKE_CURRENT_SOURCE_DIR}/solver_lib/solver.cpp
)

target_include_directories(solver PUBLIC
    ${CMAKE_CURRENT_SOURCE_DIR}/solver_lib
)

add_executable(hello_world
    ${CMAKE_CURRENT_SOURCE_DIR}/hello_world_application/hello_world.cpp
)

target_link_libraries(hello_world formatter_ex)

add_executable(equation
    ${CMAKE_CURRENT_SOURCE_DIR}/solver_application/equation.cpp
)

target_link_libraries(equation solver formatter_ex)

install(TARGETS formatter formatter_ex solver hello_world equation
    RUNTIME DESTINATION bin
    ARCHIVE DESTINATION lib
    LIBRARY DESTINATION lib
)

install(DIRECTORY formatter_lib/
    DESTINATION include
    FILES_MATCHING PATTERN "*.h"
)

install(DIRECTORY formatter_ex_lib/
    DESTINATION include
    FILES_MATCHING PATTERN "*.h"
)

install(DIRECTORY solver_lib/
    DESTINATION include
    FILES_MATCHING PATTERN "*.h"
)
