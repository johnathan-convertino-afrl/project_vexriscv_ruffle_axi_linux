################################################################################
### date      2023.06.26
### author    Jay Convertino
################################################################################

cmake_minimum_required(VERSION 3.14)

## libraries
set(XILINX_BSP_COMMON_PATH embeddedsw/lib/bsp/standalone/src/common/)
set(XILINX_BSP_COMMON_SRCS
  print.c
  sleep.h
  xbasic_types.h
  xdebug.h
  xenv.h
  xenv_standalone.h
  xil_assert.c
  xil_assert.h
  xil_cache_vxworks.h
  xil_hal.h
  xil_io.h
  xil_macroback.h
  xil_mem.c
  xil_mem.h
  xil_printf.c
  xil_printf.h
  xil_sleepcommon.c
  xil_testcache.c
  xil_testcache.h
  xil_testio.c
  xil_testio.h
  xil_testmem.c
  xil_testmem.h
  xil_types.h
  xil_util.c
  xil_util.h
  xplatform_info.c
  xplatform_info.h
  xstatus.h
)

set(XILINX_DRIVER_PATH embeddedsw/XilinxProcessorIPLib/drivers/)
set(XILINX_GPIO_PATH gpio/src/)
set(XILINX_GPIO_SRCS
  xgpio.c
  xgpio_extra.c
  xgpio_g.c
  xgpio.h
  xgpio_i.h
  xgpio_intr.c
  xgpio_l.h
  xgpio_selftest.c
  xgpio_sinit.c
)

include_directories(riscv-gnu-baremetal-addons/)

list(TRANSFORM XILINX_BSP_COMMON_SRCS PREPEND ${XILINX_BSP_COMMON_PATH})

list(TRANSFORM XILINX_GPIO_SRCS PREPEND ${XILINX_DRIVER_PATH}${XILINX_GPIO_PATH})

add_library(xilinx_bsp ${XILINX_BSP_COMMON_SRCS})
target_compile_options(xilinx_bsp PRIVATE -Werror -Wall -Wextra)

add_library(xilinx_gpio ${XILINX_GPIO_SRCS})
target_link_libraries(xilinx_gpio PUBLIC xilinx_bsp)
target_compile_options(xilinx_gpio PRIVATE -Werror -Wall -Wextra)


## baremetal applications
if(BUILD_BAREMETAL_EXAMPLES)
  add_subdirectory(examples)
endif()
