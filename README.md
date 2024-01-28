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
#### The pinout configuration IOC file:
  Configure pin PA5 as GPIO output and rename to LD2.
  
  PA5  ->  LED2;
  
  Add USART2 from connectivity and configure the following pins.
  
  as USART2_TX and USART2_RX.
  
  PA2  ->  USART2_TX;
  
  PA3  ->  USART2_RX;
  
  plus make sure that in System Core under Debug JTAG ST-LINK is selected.
#### Clock Configuration:
  16 MHz HCLK is enough for us giving both SYSCLK a 16MHz
  as well as to the Cortex System Timer.
  using the HSI RC on the board we can go up to 180 MHz frequencies.
#### Project Manager:
  Give the name and select the STM32Cube toolchain which will
  be read by platformIO later.
##### Code Generator:
  Select Copy only necessary files as well as genrate peripheral 
  initialization as pair of .c/.h files.
##### In the advanced section:
  you can see which peripherals will be created and
  initializade from the HAL driver file.

Now we generate the code and shift our focus on the PLATFORMIO
and the OS configuration, as we have generated all necessary files to run the board.

Here you can also test, by adding a toggle function in the while loop of main.c, to test the boards
LED before moving on.

HAL_GPIO_TogglePin(LD2_GPIO_Port, LD2_Pin);  // Should work fine than
press reset button to see if is toggled again & try debuggig

## RTOS
First thing open project folder on Visual Code and than use PLATFORMIO
to create a project, select again our Board, this will generate .pio\build files
that will alllow us to build and run our project on our target.
To do so first we need to add the project configurations in stm32pio.ini such as 
location of cubeMX files and ioc_file as well as Inc files and Src files.
The directories are easy to locate as we created the project in the exsisting folder.
For more check stm32pio.ini and platformio.ini files.
Now that our directory and dependencies are satisfied we need to add uC/OS in the LIB folder of our project.
Our Working Tree looks like:

![image](https://github.com/ilyashamza70/Micrium_STM32F446RE/assets/70276386/eb606d82-61c5-4c91-860a-80c6f3142625)

Where Lib contains all the micrium files achieved from the uC/OS3 repository.
This includes cfg, uC-CPU, uC-LIB, uC-OS3.
For more specification refer to the official Micrium porting Documentation [here](https://micrium.atlassian.net/wiki/spaces/osiiidoc/pages/132507/Porting+uC-OS-III).

## Main 

In the main after the initialization of the HAL module and the SystemClock, alongside GPIO
and USART2 we start the initialization process for the micrium OS.
Check main.c file for reference and uC documentation on functions for starting the OS
as well as creating a task, configure it's TCB...
In our main we initialize the OS_ERR and we initialize the OS with OS_Initi(&os_err),
Before running it we check for any errors and create our task before starting OS.
You can see the TCB structure for creating a LED Toggle task with a delay using the
HAL time delay functions.
Then we create a task with Name,function name, priority, task stack size, limit for stack...

Again we check for errors before starting the OS Scheduler with OSStart(&os_err)
from where our application should never exit, keep executing the task it is required.
Behaviour achieved by assignin the OS start to the reset handler in the startup file,
we can also check this by pressing the rest button on the board from the LED behaviour.

official micrium manual [document](https://www.analog.com/media/en/dsp-documentation/software-manuals/Micrium-uCOS-III-UsersManual.pdf)
## Running the Task

Running the task is pretty straight forward as after the operating system has been started it keeps calling
all it's TASK, which for us is LEDTASK.

Here we simply initialize the OS_err and than in an endlees loop we Toggle the LD2 pin 
add a small delay, various times can be checked,300 ms, 600ms, 900ms with OSTimeDlyHMSM(0, 0, 0, 300, OS_OPT_TIME_HMSM_NON_STRICT, &os_err);
than we turn off the LED.
Lastly we check for OS_err again in case any problems occurs.
This lays the ground for runnig Micrium OS on STM32F446RE and can be further
customized and also can be used as a starting point.
