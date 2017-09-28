project(STM32F103_HAL_Skeleton C ASM)
cmake_minimum_required(VERSION 3.8.2)

set(CMAKE_VERBOSE_MAKEFILE ON)
set(STM32CUBE_PATH D:/Users/rwilf/STM32Cube/Repository/STM32Cube_FW_F1_V1.6.0/)

add_definitions(-DSTM32F103xB)
add_definitions(-DUSE_HAL_DRIVER)

file(GLOB_RECURSE USER_SOURCES "Src/*.c" "startup/startup_stm32f103xb.s")
#message("* * * * * USER_SOURCES:")
#foreach(src ${USER_SOURCES})
#    message(${src})
#endforeach()

file(GLOB_RECURSE HAL_SOURCES "${STM32CUBE_PATH}Drivers/STM32F1xx_HAL_Driver/Src/*.c")
#message("* * * * * HAL_SOURCES:")
#foreach(src ${HAL_SOURCES})
#    message(${src})
#endforeach()

include_directories(Inc)
include_directories(${STM32CUBE_PATH}Drivers/STM32F1xx_HAL_Driver/Inc)
include_directories(${STM32CUBE_PATH}Drivers/STM32F1xx_HAL_Driver/Inc/Legacy)
include_directories(${STM32CUBE_PATH}Drivers/Include)
include_directories(${STM32CUBE_PATH}Drivers/CMSIS/Device/ST/STM32F1xx/Include)
include_directories(${STM32CUBE_PATH}Drivers/CMSIS/Include)

add_library(CMSIS
        Src/system_stm32f1xx.c)

add_library(HAL
        Src/stm32f1xx_hal_msp.c
        ${HAL_SOURCES})

SET(LINKER_SCRIPT ${CMAKE_SOURCE_DIR}/STM32F103C8Tx_FLASH.ld)
message("*** LINKER_SCRIPT ${LINKER_SCRIPT}")

add_executable(${PROJECT_NAME}.elf ${USER_SOURCES})
target_link_libraries(${PROJECT_NAME}.elf CMSIS HAL)
set_target_properties(${PROJECT_NAME}.elf PROPERTIES LINK_FLAGS "-T ${LINKER_SCRIPT}")

set(CMAKE_EXE_LINKER_FLAGS "${CMAKE_EXE_LINKER_FLAGS} -Wl,-Map=${PROJECT_BINARY_DIR}/${PROJECT_NAME}.map")
set(HEX_FILE ${PROJECT_BINARY_DIR}/${PROJECT_NAME}.hex)
set(BIN_FILE ${PROJECT_BINARY_DIR}/${PROJECT_NAME}.bin)
add_custom_command(TARGET ${PROJECT_NAME}.elf POST_BUILD
        COMMAND ${CMAKE_OBJCOPY} -Oihex $<TARGET_FILE:${PROJECT_NAME}.elf> ${HEX_FILE}
        COMMAND ${CMAKE_OBJCOPY} -Obinary $<TARGET_FILE:${PROJECT_NAME}.elf> ${BIN_FILE}
        COMMENT "Building ${HEX_FILE} \nBuilding ${BIN_FILE}")