################################################################################
### date      2023.06.26
### author    Jay Convertino
################################################################################

cmake_minimum_required(VERSION 3.14)

## baremetal applications
include_directories(../dsp_node/ ../kill_throbber ../logger)

set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/apps)

add_executable(file_to_file file_to_file.c)
target_link_libraries(file_to_file PRIVATE ${LIB_NAME_RINGBUFFER} dsp_node file_func kill_throbber logger)
target_compile_options(file_to_file PRIVATE -Werror -Wall -Wextra -Wconversion -Wsign-conversion)
install(TARGETS file_to_file DESTINATION bin)
