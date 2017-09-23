Steps for re-configuring project:

1) Open STM32F103C8_HAL_Skeleton.ioc in STM32CubeMX
2) Make desired changes to the project.
3) Save code, and close STM32CubeMX.
4) Delete .cproject
5) Delete .mxproject
6) Delete .project
7) Delete STM32F103C8_HAL_Skeleton.xml
8) Open Inc/stm32f1xx_hal_conf.h in your favorite editor
   a) Find the "/* ########################## Module Selection ############################## */"
   b) Uncomment all the lines that "#define HAL_XXXXX_ENABLED"
   c) Save and close
9) Move Src/stm32f1xx_hal_msp.c to HAL/stm32f1xx_hal_msp.c (overwrite the old version Depending on your needs, you might want to merge instead)
10) Move Src/system_stm32f1xx.c to CMSIS/system_stm32f1xx.c (overwrite the old version, Depending on your needs, you might want to merge instead)
11) 

