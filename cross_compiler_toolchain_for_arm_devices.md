# How to create a cross-compiler toolchain for arm devices
## Introduction
in this tutorial we'll use Crosstool-NG, a versatile (cross) toolchain generator. It supports many architectures and components and has a simple yet powerful menuconfig-style interface to help users to set-up a custom toolchain.

## Initial setup 
To begin, we need to download Crosstool-NG from Git. Open a terminal and run the following commands:
```
sudo apt-get update
sudo apt-get install build-essential git bison flex gawk texinfo libtool automake
git clone https://github.com/crosstool-ng/crosstool-ng.git
```
## Installation
Install crosstool-ng following these steps:
 ```
 cd crosstool-ng
 ./bootstrap
./configure --prefix=/usr/local
make
sudo make install
 ```
 >**Note**: During the installation, you may need to install some additional libraries not mentioned above. Please be attentive to the log shown in the terminal for any error messages.
 
## Configuration
Crosstool-NG provides a terminal GUI to help users set up cross-compiler toolchains effortlessly. Let's open the menu:
```
cd crosstool-ng
ct-ng menuconfig
```
Below a screenshot of the menu:

<img width="716" alt="Screenshot 2023-07-28 at 12 38 59" src="https://github.com/Flaviocondemi/crosscompiler-toolchain-guide/assets/45661520/b99ce80b-f8af-433d-81a9-eb31b066545f">

If you want to create a toolchain for arm devices you have to check the right options.
Let's follow this path: **target options -> Target Architecture -> arm**
There are a few other options you can check like compiler, linker, gcc versions and so on.. but currently we don't need them. Now let's download the configuration file doing a step back to main menu clicking "exit" button. After you come back to the bash terminal interface, type the following command:
```
ct-ng build
```
This will create the toolchain in the following folder: **~/x-tools/**
> **Note**: You can choose a custom path during the configuration selecting **Paths and misc options** on the main menu.
Congratualtions, now you have created you first custom cross compiler toolchain!

## Testing
If you don't have an arm device and you want to test your compiled .c file int your host maching, you can use qemu.
Create a simple C program file:
```
cd ~/Desktop
nano main.c
```

```
#include <stdio.h>
int main(){
 printf("Hello World!\n");
 return 0;
}
```
Save and compile the C file with the arm cross-compiler created before:
```
cd ~/x-tools/<name-of-the-crosscompiler>/bin
./<name-of-the-crosscompiler>-gcc -o ~/Desktop/main.o ~/Desktop/main.c
```
The command below will generate the compiled file. Now,install and test the C program on qemu:

```
sudo apt-get install qemu-user
qemu-arm ~/Desktop/main.o
```
If everything went smoothly, you'll see "Hello World!" displayed in the terminal.
That's it! You have successfully created a cross-compiler toolchain for ARM devices and tested it using QEMU.



