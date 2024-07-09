################################################################################
### date      2024.07.09
### author    Jay Convertino
################################################################################

cmake_minimum_required(VERSION 3.14)

project(sw)

if(NOT DEFINED BUILD_BAREMETAL_EXAMPLES)
  set(BUILD_BAREMETAL_EXAMPLES OFF)
endif()

if(NOT DEFINED BUILD_LINUX)
  set(BUILD_LINUX OFF)
endif()

set(BAREMETAL_CONFIG ${CMAKE_CURRENT_SOURCE_DIR}/riscv-gnu-toolchain/configure --prefix=${CMAKE_CURRENT_SOURCE_DIR}/bin/riscv --with-arch=rv32imazicsr --with-abi=ilp32)

include(ExternalProject)

#ExternalProject_Add(riscv-gnu-toolchain
  #SOURCE_DIR ${CMAKE_CURRENT_SOURCE_DIR}/riscv-gnu-toolchain
  #DOWNLOAD_COMMAND git submodule update --init --recursive ${CMAKE_CURRENT_SOURCE_DIR}/riscv-gnu-toolchain
  #CONFIGURE_COMMAND ${BAREMETAL_CONFIG}
  #BUILD_COMMAND ${MAKE}
  #BUILD_IN_SOURCE 1)

ExternalProject_Add(riscv-openocd
  SOURCE_DIR ${CMAKE_CURRENT_SOURCE_DIR}/riscv-openocd
  CONFIGURE_COMMAND ${CMAKE_CURRENT_SOURCE_DIR}/riscv-openocd/bootstrap
    COMMAND ${CMAKE_CURRENT_SOURCE_DIR}/riscv-openocd/configure --prefix=${CMAKE_CURRENT_SOURCE_DIR}/bin/openocd --enable-ftdi --enable-dummy --enable-jtag_vpi
  BUILD_COMMAND ${MAKE}
  BUILD_IN_SOURCE 1)

if(BUILD_BAREMETAL_EXAMPLES)
  add_subdirectory(baremetal)
endif()

if(BUILD_LINUX)
  add_subdirectory(linux)
endif()
