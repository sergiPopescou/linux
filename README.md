HOW TO BUILD FOR QEMU:
=====================
## 1. set the variables
set to the path to of the linux source fot two more environ variables in ~/.bashrc
if this source is cloned in `~/linux-src` then it looks like this in bashrc

    export INSTALL_MOD_PATH=~/linux-src
    export INSTALL_DTBS_PATH=~/linux-src

## 2. compile the patched kernel
```
    cd ~/linux-src
    make ARCH=arm CROSS_COMPILE=arm-linux-gnueabihf- versatile_defconfig
    make ARCH=arm CROSS_COMPILE=arm-linux-gnueabihf- zImage modules dtbs -j 6
```
Just in case variables are set once more


## 3. download and decompress qemu files

### 3.1 python tool for downloading from the google dive needed
```
    sudo apt install python-pip
    pip install gdown
```
### 3.2 download file in linux folder
```
    cd ~/linux-src
    gdown https://drive.google.com/uc?id=1UAf0JUE5PW8dbqoNj-uocu8Kj4WnHrga
```
### 3.3 decompress it directly in linux-src root folder (not in sub-folder)
```
    tar -xf qemu_files.tar.xz
```

## 4. run QEMU emulator

With all the previous steps, we should get the kernel image, the device tree blob file and the disk image in the paths shown below:
```
    ~/linux/arch/arm/boot/zImage
    ~/linux/vmlinux
    ~/linux/arch/arm/boot/dts/versatile-pb.dtb
    ~/linux/2020-04-30-raspbian-buster-lite.img
    ~/linux/run_qemu.sh
```

run `./run_qemu.sh` in `~/linux` folder




Linux kernel
============

There are several guides for kernel developers and users. These guides can
be rendered in a number of formats, like HTML and PDF. Please read
Documentation/admin-guide/README.rst first.

In order to build the documentation, use ``make htmldocs`` or
``make pdfdocs``.  The formatted documentation can also be read online at:

    https://www.kernel.org/doc/html/latest/

There are various text files in the Documentation/ subdirectory,
several of them using the Restructured Text markup notation.
See Documentation/00-INDEX for a list of what is contained in each file.

Please read the Documentation/process/changes.rst file, as it contains the
requirements for building and running the kernel, and information about
the problems which may result by upgrading your kernel.
