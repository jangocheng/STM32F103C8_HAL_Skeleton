## Steps for re-configuring project:

1) Open STM32F103C8_HAL_Skeleton.ioc in STM32CubeMX
2) Make desired changes to the project
3) Save code, and close STM32CubeMX
4) Delete .cproject
5) Delete .mxproject
6) Delete .project
7) Delete STM32F103C8_HAL_Skeleton.xml
8) Open Inc/stm32f1xx_hal_conf.h in your favorite editor
   * Find the "/* ########################## Module Selection ############################## */"
   * Uncomment all the lines that "#define HAL_XXXXX_ENABLED"
   * Save and close
9) Move Src/stm32f1xx_hal_msp.c to HAL/stm32f1xx_hal_msp.c (overwrite the old version Depending on your needs, you might want to merge instead)
10) Move Src/system_stm32f1xx.c to CMSIS/system_stm32f1xx.c (overwrite the old version, Depending on your needs, you might want to merge instead)

##You are now ready to open the project in CLion
1) If you want a completely clean environment, delete the .idea folder
2) Open the project folder in CLion
3) Tell it to ignore the fact that some files are outside the project folder (It's by design)
4) From the menu, go to: File -> Settings -> Build, Execution, Deployment -> CMake
5) In "CMake options" type: -DCMAKE_TOOLCHAIN_FILE=stm32f103.cmake
6) Click OK
7) Open the CMake view (at the bottom left)
8) Click the grar and choose "Reset Cache and Reload Project
9) Build
10) (OPTIONAL) right-click on the "Inc" folder and Mark Directory As -> Project Sources and Headers (It gets rid of warning messages when you open header files)
11) In fact, I do that to all my code folders to make them blue instead of orange
