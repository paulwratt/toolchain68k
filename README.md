# toolchain68k
Build a toolchain for 68k cross developement using recent compilers and libraries.
The build script is also supporting the avr target.

The script can be used on Windows 10 with MSYS2, on Debian 8, and on Fedora 25.


# Prepare Build Environment for Windows and MSYS
all commands are to be typed into the msys shell
## Installation of  MSYS2 Base System and needed packages
  * download the MSYS2 Installer from the [MSYS Home Page](http://www.msys2.org/), use the 64 Bit Version
  * execute installer and chose the installation path as follows
    * best on a SSD
    * will need approx 4 GB space
    * exclude it from the virus scanner
    * exclude it form the windows index service
    * short path without spaces
    * not on a FAT Filesystem
    * i use *C:\Tools\msys64*
  * update the base system as described on the [MSYS Home Page](http://www.msys2.org/)
    * ```pacman -Syu```
    * ok the questions, close window when ready
    * open MSYS Shell again(start menu, use 64bit version)
    * ```pacman -Su```

Now clone the git repository.
```
git clone https://github.com/haarer/toolchain68k.git
```
Install the required packages for msys
```
sh install_req_pkg_msys.sh
```

# Prepare Build Environment for Debian 8
First install git.
```
sudo apt-get install git
```
Now clone the git repository.
```
git clone https://github.com/haarer/toolchain68k.git
```
Install the required packages for msys.
```
cd toolchain68k
bash install_req_pkg_debian.sh
```

# Prepare Build Environment for Fedora 25
First install git.
```
sudo yum install git
```
Now clone the git repository.
```
git clone https://github.com/haarer/toolchain68k.git
```
Install the required packages for fedora.
```
sh install_req_pkg_fedora.sh
```

# Building and Installing of the Toolchain    
Set the wanted target architecture in the build script by commenting out the unwanted arch.
```
#TARGETARCHITECTURE=avr
TARGETARCHITECTURE=m68k-elf
```
Note that the toolchain is currently installed to /opt/m68k - i'll change that to something like /opt/crosstoolchain later.
Start the build script.
```
bash   buildtoolchain.sh
```
On linux, authorize sudo (this needed for installation).

# Testing the Toolchain
Add the path to the binaries
```
export PATH=$PATH:/opt/m68k/bin
```

### compile one of the 68k toolchain examples
see the linker scripts called for the make file.
One example uses toolchain provided startup files and linkerscript (m68k-example2), the other one uses custom linker scripts and own startup files (m68k-example)

```
cd examples/m68k-example
make 
```

### compile the avr toolchain examples
This example assumes an arduino mega connected to usb (com3, see makefile) and is a simple led blink example.
```
cd examples/avr-example
make 
make flash
```
