# Micrium_STM32F446RE
Porting Micrium OS on STM32 Nucleo Board F446RE.

The sourse code for micrium OS was obtained from the public repository
of Weston Embeded Solution, the official guardian of the Code.

A little about Micrium (uC/OS), it is a RTOS with a premptive realt time kernel,
with countless applications and stack support such as TCP, IP, DHCP, CAN, Client,
Server, FTP, HTTP...

The preemptive kernel allows higher priorities task to stop the execution of lower
priority stack, and gain control of the CPU until it is required;
In embedded system it becomes necessary to run safety and time critical operations
to allow the correct response to any errors or external signals.

## GOAL
Running a simple Blinking task in MicriumOS, using the Nucleo board.

## Setup
To be able to setup the environment, we required some development tools.
We needed the configuration data and parameters for our specific board along with an
environment to build and flash our code onto the board. 
For this we made use of
####   PlatformIO
PlatformIO is a cross-platform IDE (Integrated Development Environment)
for microcontroller-based embedded systems and embedded development.
PlatformIO IDE can be installed as an extension of Visual Studio Code 
dierectly or downloaded from this page [PLATFORM_IO](https://platformio.org/).
This allowed us to easily test debug and program our board.

####    Visual Studio Code
This was the main IDE where our software was built custom specific for
our CPU, an ARM Cortex-M4. Here is where we integrated Micrium OS in 
our project, with all the correct directory and dependencies.
Starting from the startup file to assign the reset handler to uC/OS3
after the initialization, to the main where the os was started and
a task was created to blink a LED with a delay function.

####    STM32CubeF4
STM32CubeMX is a graphical software, Graphical User Interface (GUI), 
offered by ST to help with the configuration and initialization of 
C-code for the STM32 microcontrollers and microprocessors, and can 
be easily downloaded here [STM32Cubef4](https://www.st.com/en/embedded-software/stm32cubef4.html).

## Environment
Easy to setup and generate the appropriate files
from the STM32CubeIDE by selecting the right board, in our case 
STM32-F446RE.
### The pinout configuration IOC file:
  Configure pin PA5 as GPIO output and rename to LD2
  PA5  ->  LED2;
  Add USART2 from connectivity and configure the following pins
  as USART2_TX and USART2_RX
  PA2  ->  USART2_TX 
  PA3  ->  USART2_RX
  plus make sure that in System Core under Debug JTAG
  STLINK is selected.
### Clock Configuration:
  16 MHz HCLK is enough for us giving both SYSCLK a 16MHz
  as well as to the Cortex System Timer.
  using the HSI RC on the board we can go up to 180 MHz frequencies.
### Project Manager:
  Give the name and select the STM32Cube toolchain which will
  be read by platformIO later.
### Code Generator:
  Select Copy only necessary files as well as genrate peripheral 
  initialization as pair of .c/.h files.
### In the advanced section:
  you can see which peripherals will be created and
  initializade from the HAL driver file.

Now we generate the code and shift our focus on the PLATFORMIO
and the OS configuration, as we have generated all necessary files to run the board.
Here you can also test, by adding a toggle function in the while loop of main.c, to test the boards
LED before moving on.
HAL_GPIO_TogglePin(LD2_GPIO_Port, LD2_Pin);  // Should work fine than press reset button to see if is toggled again & try debuggig
  
  

and than configure a SYSCLK, like 16MHz.
Thanks to the GUI you can easily configure and add the 
right peripherals or GPIO with their configuration. 
For the pourpose of demonstarting we also added a USART
periphal to display how easy it is to integrate and than 
use.
This first step allowed us to generate the .ioc file 
as well as the HAL module driver and some other basic
board file as part of the BSP (board support package)
2nd Step is to create a project with platformIO selecting
the appropriate board. This project is where we will work,
after integrating all the BSP files and CSMIS files in 
the project directory.

## RTOS
Next steps concerned the porting of Micrium

## Start file

## Main 

## Running the Task

