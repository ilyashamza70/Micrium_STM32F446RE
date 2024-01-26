# Micrium_STM32F446RE
Porting Micrium OS on STM32 Nucleo Board F446RE.

The sourse code for micrium OS was obtained from the public repository
of Weston Embeded Solution, the official guardian of the Code.

A little about Micrium (uC/OS), it is a RTOS with a premptive realt time kernel,
with countless applications and stack support such as TCP, IP, DHCP, CAN, Client, Server, FTP, HTTP...

The preemptive kernel aloows higher priorities task to stop the execution of lower priority stack,
and gain control of the CPU until it is required;
In embedded system it becomes necessary to run safety and time critical operations to allow
the correct response to any errors or external signals.

## GOAL
Running a simple Blinking task in MicriumOS, using the Nucleo board.

## Setup
To be able to setup the environment, we required some development tools.
We needed the configuration data and parameters for our specific board along with an environment to build
and flash our code onto the board. 
For this we made use of
###   PlatformIO
            *PlatformIO is a cross-platform IDE (Integrated Development Environment) for microcontroller-based embedded 
            systems and embedded development. PlatformIO IDE can be installed on top of Visual Studio Code, which is what
            we have done for this project.*
###    STM32CubeMX
            *STM32CubeMX is a graphical software, Graphical User Interface (GUI), offered by ST to help with the 
            configuration and initialization of C-code for STM32 microcontrollers and microprocessors.*



# Environment

# CPU Specific file

# Start file

# Main 

# Running the OS

# Running the Task

