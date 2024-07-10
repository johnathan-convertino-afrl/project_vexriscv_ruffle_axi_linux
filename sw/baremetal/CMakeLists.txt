################################################################################
### date      2023.06.26
### author    Jay Convertino
################################################################################

cmake_minimum_required(VERSION 3.14)

## libraries
set(FILE_FUNC_SRCS
  file_func.c
  file_func.h
)

include_directories(../ ../../kill_throbber/ ../../logger/)

add_library(file_func ${FILE_FUNC_SRCS})
target_link_libraries(file_func PUBLIC ${LIB_NAME_RINGBUFFER} Threads::Threads)
target_compile_options(file_func PRIVATE -Werror -Wall -Wextra -Wconversion -Wsign-conversion)


## baremetal applications
if(BUILD_BAREMETAL_EXAMPLES)
  add_subdirectory(examples)
endif()
