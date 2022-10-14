# ese519_lab2
# Setup Guide-Xuanang Chen
E-mail: xuanangc@seas.upenn.edu

Tested on:  
THUNDEROBOT 911Plus 11 (15.6-inch 2022)  
-Intel(R) Core(TM) i7-10870H CPU @ 2.20GHz   2.21 GHz
-Windows 11 21H2 22000.1098  
-64-bit operating system, x64-based processor  
## Step1: Install Softwares
#### 1.[Installing Arm GNU Toolchain](https://developer.arm.com/downloads/-/arm-gnu-toolchain-downloads)  
First, you need to download a install file ending with "-arm-none-eabi.exe".I chose version 11.2 as below:  
![alt](https://github.com/AngLi-00/ese5190-lab2/blob/4d2396c628fd15491f2d9b771bc2876b1c7374ae/1-arm.png)  
Note that you should tick the box to register the path to the Arm compiler as an environment variable in the Windows shell!  
![alt](https://github.com/AngLi-00/ese5190-lab2/blob/4d2396c628fd15491f2d9b771bc2876b1c7374ae/1-arm2.png)  
  
#### 2.[Installing CMake](https://cmake.org/download/)  
I choosed Windows x64 Installer as below:
![alt](https://github.com/AngLi-00/ese5190-lab2/blob/main/2-cmake.png)
Note that you should also add CMake to the system PATH for all users!
![alt](https://github.com/AngLi-00/ese5190-lab2/blob/main/2-cmake2.png)  

#### 3.[Installing Visual Studio 2022](https://visualstudio.microsoft.com/downloads/#build-tools-for-visual-studio-2022)  
The only thing you need to note during this part is installing the Build Tools for Visual Studio 2022.  
![alt](https://github.com/AngLi-00/ese5190-lab2/blob/main/3-VS2022.png)  

#### 4.[Installing Python 3.10](https://www.python.org/downloads/windows/)   
I choosed 3.10.7 for windows(64bit) version as below:  
![alt](https://github.com/AngLi-00/ese5190-lab2/blob/main/4-Python.png)  
During this part, you should ensure that it’s installed 'for all users' and add Python 3.10 to the system PATH. Besides you should disable the MAX_PATH length limit when prompted at the end of the installation.  
![alt](https://github.com/AngLi-00/ese5190-lab2/blob/main/4-Python2.png)  
#### 5.[Installing Git](https://git-scm.com/download/win)  
I choosed the latest installer for windows(64bit) version as below:  
![alt](https://github.com/AngLi-00/ese5190-lab2/blob/main/5-Git.png)  
Note that you should change the default editor away from vim during installing. Leave all other settings as default or recommanded.  
![alt](https://github.com/AngLi-00/ese5190-lab2/blob/main/5-Git2.png)  


## Step2: Getting the SDK and examples

    C:\Users\Xuanang Chen\pico\Downloads> git clone -b master https://github.com/raspberrypi/pico-sdk.git 
    C:\Users\Xuanang Chen\pico\Downloads> cd pico-sdk
    C:\Users\Xuanang Chen\pico\Downloads\pico-sdk> git submodule update --init 
    C:\Users\Xuanang Chen\pico\Downloads\pico-sdk> cd ..
    C:\Users\Xuanang Chen\pico\Downloads> git clone -b master https://github.com/raspberrypi/pico-examples.git


## Step3: Building "Hello World" from Visual Studio Code  
Download and install Visual Studio Code for Windows. After installation open the Developer Command Prompt for VS2022 and type:
    C:> code
This command will open Visual Studio Code with all the correct environment variables set.  
Then you need to install the CMake Tools extension. Type Ctrl + Shift + X and search for "CMake Tools" and click the install button. After installation you have to change several settings. Select "Settings"->"Extension"->"CMake Tools"->"Cmake: Configure Environment", click on "Add Item" and set the `PICO_SDK_PATH` to be `..\..\pico-sdk`  
Then find "Cmake: Generator" and enter `NMake Makefiles` into the box.  

Now you need to close the Settings page, go to the File menu and click on "Open Folder" and navigate to pico-examples repo and click "Select Folder". Then select "GCC for arm-none-eabi" in the upper sidebar.   
![alt](https://github.com/AngLi-00/ese5190-lab2/blob/main/6-vscode.png)   
After that, click on the "Build" buttonin the blue bottom bar of the window. This will take a long time to create the build directory and run CMake and build the examples project.
![alt](https://github.com/AngLi-00/ese5190-lab2/blob/main/6-vscode2.png)   

## Step4: Flashing and Running "Hello World"
Correctly Connect your RP2040:  When you connect RP2040 Raspberry Pi Pico to the computer via the Micro-USB, you need to hold down the BOOTSEL button to force it into USB Mass Storage Mode until the board appear as a external drive. You can find UF2 binary in the hello_world/serial and hello_world/usb directories inside the newly created build directory, then drag-and-drop the UF2 binary you want onto the external drive. The Raspberry Pi Pico will reboot, and unmount itself as an external drive, and start running the flashed code.  

Then we need a *SERIAL CONSOLE* to see the output. For me PUTTY is a good software. In lab1 we have a guide for serial console: <https://learn.adafruit.com/welcome-to-circuitpython/advanced-serial-console-on-windows>.This might help you.  

Open the software PuTTy ，choose "Serial" as connection type, enter the serial port you found that your board is using **(Check in Device Manager! The COM number is different from lab1!)**, and modify the speed to 115200.   
![alt](https://github.com/AngLi-00/ese5190-lab2/blob/main/7-PUTTY.png)  
Click "Open" botton, then you can see the output "hello world".  
![alt](https://github.com/AngLi-00/ese5190-lab2/blob/main/7-PUTTY2.png)  
