# How to create a cross-compiler toolchain for arm devices
### Introduction

### Initial setup 
We'll use crosstool-ng to create a cross-compiler toolchain. Let's download it from git:
```
sudo apt-get update
sudo apt-get install build-essential git bison flex gawk texinfo libtool automake
git clone https://github.com/crosstool-ng/crosstool-ng.git
```
### Installation
Install crosstool-ng following these steps:
 ```
 cd crosstool-ng
 ./bootstrap
./configure --prefix=/usr/local
make
sudo make install
 ```
 >**Note**: During the installation it could happens to install some other libraries, therefore be careful on the log shown in the terminal.
 
### Configuration
Crosstool-ng has a terminal GUI that helps users to easily set-up cross-compiler toolchains. Let's open the menu:
```
cd crosstool-ng
ct-ng menuconfig
```
Below a screenshot of the menu:

You'll see a lot of options after the menu is opened.

