## Steps for re-configuring project:

1) Open STM32F103C8_HAL_Skeleton.ioc in STM32CubeMX
2) Make desired changes to the project
3) Save STM32CubeMX project
4) Generate project code (your changes should be merged with existing code)
5) Close STM32CubeMX
4) Optionally Delete These Files:
* .cproject
* .mxproject
* .project
* STM32F103C8_HAL_Skeleton.xml

## You are now ready to open the project in CLion
1) If you want a completely clean environment, delete the .idea folder
2) Open the project folder in CLion
4) From the menu, go to: File -> Settings -> Build, Execution, Deployment -> CMake
5) In "CMake options" type: -DCMAKE_TOOLCHAIN_FILE=stm32f103.cmake
6) Click OK
7) Open the CMake view (at the bottom left)
8) Click the gear and choose "Reset Cache and Reload Project
9) Build
10) (OPTIONAL) right-click on the "Inc" folder and Mark Directory As -> Project Sources and Headers (This cancels warning message when you open header files)
10) (OPTIONAL) right-click on the "Src" folder and Mark Directory As -> Project Sources and Headers
10) (OPTIONAL) right-click on the "startup" folder and Mark Directory As -> Project Sources and Headers
10) (OPTIONAL) right-click on the "Drivers" folder and Mark Directory As -> Library Files
