# Micrium_STM32F446RE
Porting Micrium OS on STM32 Nucleo Board F446RE.

The sourse code for micrium OS was obtained from the public repository
of Weston Embeded Solution, the official guardian of the Code.

A little about Micrium (uC/OS), it is a RTOS with a premptive realt time kernel,
with countless applications and stack support such as TCP, IP, DHCP, CAN, Client,
Server, FTP, HTTP...

The preemptive kernel aloows higher priorities task to stop the execution of lower
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
Easy to setup from the STM32CubeIDE by selecting the right board, in our case 
STM32-F446RE and than configure a SYSCLK, 16MHz in our case.
Thanks to the GUI you can easily configure and integrate the 
right peripherals or GPIO like for us. For the pourpose 
of demonstarting we also added a USART 

# CPU Specific file

# Start file

# Main 

# Running the OS

# Running the Task

