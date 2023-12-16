cmake_minimum_required(VERSION 3.15.3)
set(CMAKE_MESSAGE_LOG_LEVEL debug)
set(PROJECT mpctss)

project(${PROJECT})

set(EXECUTABLE ${PROJECT_NAME})
set(CMAKE_C_STANDARD 11)
set(CMAKE_C_STANDARD_REQUIRED ON)
set(CMAKE_C_EXTENSIONS OFF)

set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -Wall")
set(CMAKE_BUILD_TYPE Debug)

file(GLOB_RECURSE SOURCES "vendor/*.*" "src/*.*")

add_executable(${EXECUTABLE} ${SOURCES} ${INCLUDES})
add_compile_definitions(USE_BIP32_CACHE=0 USE_BIP39_CACHE=0 USE_MONERO=1)

target_include_directories(${EXECUTABLE} PRIVATE
        src/
        vendor/crypto
        )

target_compile_options(${EXECUTABLE} PRIVATE
        -Wall -g
        -D_POSIX_C_SOURCE=200809L
        -DUSE_BN_PRINT=1
        -DUSE_INSECURE_PRNG=1

        $<$<CONFIG:Debug>:-g3>
        )

target_link_libraries(${CMAKE_PROJECT_NAME} ws2_32)        