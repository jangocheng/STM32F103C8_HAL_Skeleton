# Ray's STM32F103C8 Project Skeleton
## Introduction
I wanted an easy routine for starting new development projects using the STM32
microcontroller family. I found a few existing repositories, including
[this advanced project](https://github.com/ObKo/stm32-cmake). In fact, I used
their compile and linker flags. However, I wanted something more specialized
for my requirements:
* I wanted my configuration scripts to be simple to read and edit
* I wanted to modify the initialization using STM32Cube
* I wanted to open a new project in CLion and get going in less than 2 minutes      

## Prerequisite 3rd party software
* This project was set-up to run under Windows 10
* I downloaded STM32CubeMX from [here](http://www.st.com/content/st_com/en/products/embedded-software/mcus-embedded-software/stm32-embedded-software/stm32cube-embedded-software/stm32cubef1.html)
* I needed the GCC ARM toolchain from [here](https://developer.arm.com/open-source/gnu-toolchain/gnu-rm/downloads)
* For debugging, I use OpenOCD. I grabbed a prebuilt windows binary from [here](https://github.com/gnu-mcu-eclipse/openocd/releases)
* I'm using an ST-Link debugging interface so I got some drivers and utilities from [here](http://www.st.com/content/st_com/en/products/development-tools/software-development-tools/stm32-software-development-tools/stm32-programmers/stsw-link004.html)
* CLion (by [JET BRAINS](https://www.jetbrains.com/clion/?fromMenu)) If you can't afford a license,
then use the 30-day trial, or use the free EAP ([Early Access Program](https://www.jetbrains.com/clion/nextversion/)) 

## Links to helpful sites
* [STM32 Blue Pill](http://wiki.stm32duino.com/index.php?title=Blue_Pill) Information 

## Steps for configuring your new project:

1. Open STM32F103C8_HAL_Skeleton.ioc in STM32CubeMX
1. Make desired changes to the project
1. Save STM32CubeMX project
1. Generate project code (your changes should be merged with existing code)
1. Close STM32CubeMX
1. Optionally Delete These Files:
* .cproject
* .mxproject
* .project
* STM32F103C8_HAL_Skeleton.xml

## You are now ready to open the project in CLion
1. If you want a completely clean environment, delete the .idea folder
1. Open the project folder in CLion (It auto-detects the CMakeLists.txt)
1. From the menu, go to: File -> Settings -> Build, Execution, Deployment -> CMake
1. In "CMake options" type: -DCMAKE_TOOLCHAIN_FILE=stm32f103.cmake
1. Click OK
1. Set your project name in the project() command at the top of CMakeLists.txt
1. Verify/set the "*** IMPORTANT ***" setting in CMakeLists.txt
1. Set the TOOLCHAIN_PATH in stm32f103.cmake (It WILL be wrong for your environment!!!)  
1. Open the CMake view (at the bottom left)
1. Click the gear and choose "Reset Cache and Reload Project"
1. You should see some "*** IMPORTANT ***" lines in the CMake view (Are they correct?) 
1. Build
1. (OPTIONAL) right-click on the "Inc" folder and Mark Directory As -> Project Sources and Headers (This cancels warning message when you open header files)
1. (OPTIONAL) right-click on the "Src" folder and Mark Directory As -> Project Sources and Headers
1. (OPTIONAL) right-click on the "startup" folder and Mark Directory As -> Project Sources and Headers
1. (OPTIONAL) right-click on the "Drivers" folder and Mark Directory As -> Library Files
