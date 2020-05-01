HOW TO RUN QEMU
===============

## 1. get compiler other tools and update

```
    git clone --depth 1 https://github.com/raspberrypi/tools ~/tools
    sudo apt update
    sudo apt install git bison flex libssl-dev
```

## 2. clone this source code:

```
    git clone --depth 1 https://github.com/sergiPopescou/linux ~/linux
```


## 3. instal QEMU for ARM
```
    sudo apt install qemu-system-arm
```
### Status after first three steps

After this step, you have your tools and linux source code in the following paths:
```
    ~/tools/: Raspberry Pi’s compiler tool set
    ~/linux/: Patched Linux kernel source code folder
```

## 4. set the environmental variables:
```
    echo PATH=\$PATH:~/tools/arm-bcm2708/gcc-linaro-arm-linux-gnueabihf-raspbian-x64/bin >> ~/.bashrc
    echo KERNEL=kernel7 >> ~/.bashrc
    echo CROSS_COMPILE=arm-linux-gnueabihf- >> ~/.bashrc
    echo ARCH=arm >> ~/.bashrc
    source ~/.bashrc
```
The last command will execure bashrc once again to set the variables


## 5. compile the patched kernel
```
    cd ~/linux
    make ARCH=arm CROSS_COMPILE=arm-linux-gnueabihf- versatile_defconfig
    make ARCH=arm CROSS_COMPILE=arm-linux-gnueabihf- zImage modules dtbs -j 6
```
Just in case variables are set once more


## 6. download and decompress qemu files

### 6.1 python tool for downloading from the google dive needed
```
    sudo apt install python-pip
    pip install gdown
```
### 6.2 download file in linux folder
```
    cd ~/linux
    gdown https://drive.google.com/uc?id=1UAf0JUE5PW8dbqoNj-uocu8Kj4WnHrga
```
### 6.3 decompress it directly in linux root folder (not in sub-folder)
```
    tar -xf qemu_files.tar.xz
```

## 7. run QEMU emulator

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
