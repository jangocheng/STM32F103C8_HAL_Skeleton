project(f1_blink C ASM)
cmake_minimum_required(VERSION 3.8.2)

add_definitions(-DSTM32F103xB)

file(GLOB_RECURSE USER_SOURCES "Src/*.c")
message("* * * * * USER_SOURCES:")
foreach(src ${USER_SOURCES})
    message(${src})
endforeach()

set(STM32CUBE_PATH D:/Users/rwilf/STM32Cube/Repository/STM32Cube_FW_F1_V1.6.0/)

file(GLOB_RECURSE HAL_SOURCES "${STM32CUBE_PATH}Drivers/STM32F1xx_HAL_Driver/Src/*.c")
message("* * * * * HAL_SOURCES:")
foreach(src ${HAL_SOURCES})
    message(${src})
endforeach()

add_library(CMSIS
    CMSIS/system_stm32f1xx.c
    CMSIS/startup_stm32f103xb.s)

include_directories(Inc)
include_directories(${STM32CUBE_PATH}Drivers/STM32F1xx_HAL_Driver/Inc)
include_directories(${STM32CUBE_PATH}Drivers/STM32F1xx_HAL_Driver/Inc/Legacy)
include_directories(${STM32CUBE_PATH}Drivers/Include)
include_directories(${STM32CUBE_PATH}Drivers/CMSIS/Device/ST/STM32F1xx/Include)
include_directories(${STM32CUBE_PATH}Drivers/CMSIS/Include)

add_executable(${PROJECT_NAME}.elf ${USER_SOURCES} ${HAL_SOURCES} ${LINKER_SCRIPT})

target_link_libraries(${PROJECT_NAME}.elf CMSIS)

set(CMAKE_EXE_LINKER_FLAGS "${CMAKE_EXE_LINKER_FLAGS} -Wl,-Map=${PROJECT_SOURCE_DIR}/build/${PROJECT_NAME}.map")
set(HEX_FILE ${PROJECT_SOURCE_DIR}/build/${PROJECT_NAME}.hex)
set(BIN_FILE ${PROJECT_SOURCE_DIR}/build/${PROJECT_NAME}.bin)
add_custom_command(TARGET ${PROJECT_NAME}.elf POST_BUILD
COMMAND ${CMAKE_OBJCOPY} -Oihex $<TARGET_FILE:${PROJECT_NAME}.elf> ${HEX_FILE}
COMMAND ${CMAKE_OBJCOPY} -Obinary $<TARGET_FILE:${PROJECT_NAME}.elf> ${BIN_FILE}
COMMENT "Building ${HEX_FILE} \nBuilding ${BIN_FILE}")