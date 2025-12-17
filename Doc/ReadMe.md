<h2 align="center">Description files</h2>

- Prime-M35P_v24.pdf - board functional diagram;

<h2 align="center">Linux system build procedure</h2>

**Package installation**  
$ sudo apt install build-essential  
$ sudo apt install bison flex swig git  
$ sudo apt install openssl libssl-dev libelf-dev  
$ sudo apt install libudev-dev libpci-dev libiberty-dev  
$ sudo apt install libncurses5-dev gparted python3  
$ sudo apt install dkms autoconf  

**Installing cross-compiler**  
*get file https://disk.yandex.ru/d/VCLHKDqusnvv8A/gcc-linaro-7.5.0-2019.12-x86_64_arm-linux-gnueabihf.tar*  
$ tar xvf gcc-linaro-7.5.0-2019.12-x86_64_arm-linux-gnueabihf.tar  
$ sudo mv gcc-linaro-7.5.0-2019.12-x86_64_arm-linux-gnueabihf /opt/  
$ export CC=/opt/gcc-linaro-7.5.0-2019.12-x86_64_arm-linux-gnueabihf/bin/arm-linux-gnueabihf-  
*availability check*  
$ ${CC}gcc -v  

**Install Python for binman u-boot olders version**  
$ wget https://www.python.org/ftp/python/2.7.18/Python-2.7.18.tgz  
*or get https://disk.yandex.ru/d/VCLHKDqusnvv8A/Python-2.7.18.tgz*  
$ tar xzf Python-2.7.18.tgz  
$ cd Python-2.7.18  
$ sudo ./configure --enable-optimizations  
$ sudo make altinstall  
$ sudo ln -s "/usr/local/bin/python2.7" "/usr/bin/python"  
$ sudo ln -s "/usr/local/bin/python2.7" "/usr/bin/python2"  

**Creating a working directory**  
$ mkdir Prime-M  
$ cd Prime-M  
Prime-M$ mkdir uSD  

**U-BOOT**  
Prime-M$ git clone https://github.com/SymTrioS/u-boot-m.git -b v3s-current  
Prime-M$ cd u-boot-m  
Prime-M/u-boot-m$ make ARCH=arm CROSS_COMPILE=${CC} distclean  
Prime-M/u-boot-m$ make ARCH=arm CROSS_COMPILE=${CC} prime_m_defconfig  
Prime-M/u-boot-m$ make ARCH=arm CROSS_COMPILE=${CC} menuconfig  
*making necessary changes, Device Drivers->Network device support->ON->Allwinner Sun8i Ethernet MAC support ON , save-exit* 
Prime-M/u-boot-m$ make ARCH=arm CROSS_COMPILE=${CC} -j16  
Prime-M/u-boot-m$ cp u-boot-sunxi-with-spl.bin ../uSD/  
Prime-M/u-boot-m$ cd ..  

