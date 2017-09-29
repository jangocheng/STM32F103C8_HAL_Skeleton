project(STM32F103_HAL_Skeleton C ASM)
cmake_minimum_required(VERSION 3.8.2)

set(CMAKE_VERBOSE_MAKEFILE ON)
set(STM32CUBE_PATH "D:/Users/rwilf/STM32Cube/")

add_definitions(-DSTM32F103xB)
add_definitions(-DUSE_HAL_DRIVER)
add_definitions(-DARM_MATH_CM3)

file(GLOB_RECURSE USER_SOURCES "Src/*.c" "startup/startup_stm32f103xb.s")
#message("* * * * * USER_SOURCES:")
#foreach(src ${USER_SOURCES})
#    message(${src})
#endforeach()

file(GLOB_RECURSE HAL_SOURCES "Drivers/STM32F1xx_HAL_Driver/Src/*.c")
#message("* * * * * HAL_SOURCES:")
#foreach(src ${HAL_SOURCES})
#    message(${src})
#endforeach()

include_directories(Inc)
include_directories(Drivers/STM32F1xx_HAL_Driver/Inc)
include_directories(Drivers/STM32F1xx_HAL_Driver/Inc/Legacy)
include_directories(Drivers/CMSIS/Device/ST/STM32F1xx/Include)
include_directories(Drivers/CMSIS/Include)

find_library(CMSIS arm_cortexM3l_math
        ${STM32CUBE_PATH}/Repository/STM32Cube_FW_F1_V1.6.0/Drivers/CMSIS/Lib/GCC
        NO_DEFAULT_PATH)
#message("* * * * CMSIS: ${CMSIS}")

add_library(HAL ${HAL_SOURCES})

SET(LINKER_SCRIPT ${CMAKE_SOURCE_DIR}/STM32F103C8Tx_FLASH.ld)
#message("*** LINKER_SCRIPT ${LINKER_SCRIPT}")

add_executable(${PROJECT_NAME}.elf ${USER_SOURCES})
target_link_libraries(${PROJECT_NAME}.elf  HAL ${CMSIS})
set_target_properties(${PROJECT_NAME}.elf PROPERTIES LINK_FLAGS "-T ${LINKER_SCRIPT}")

set(CMAKE_EXE_LINKER_FLAGS "${CMAKE_EXE_LINKER_FLAGS} -Wl,-Map=${PROJECT_BINARY_DIR}/${PROJECT_NAME}.map")
set(HEX_FILE ${PROJECT_BINARY_DIR}/${PROJECT_NAME}.hex)
set(BIN_FILE ${PROJECT_BINARY_DIR}/${PROJECT_NAME}.bin)
add_custom_command(TARGET ${PROJECT_NAME}.elf POST_BUILD
        COMMAND ${CMAKE_OBJCOPY} -Oihex $<TARGET_FILE:${PROJECT_NAME}.elf> ${HEX_FILE}
        COMMAND ${CMAKE_OBJCOPY} -Obinary $<TARGET_FILE:${PROJECT_NAME}.elf> ${BIN_FILE}
        COMMENT "Building ${HEX_FILE} \nBuilding ${BIN_FILE}")