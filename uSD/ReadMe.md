
## Preparing a uSD card:  

Prime-M35P/uSD$ gparted  
*Create two partitions: part1=~32M,fat16; part2=ext4*  
*Remember the letter designation of the Flash device, below it is designated as x: sdx1,sdx2*  

*Write u-boot:*  
Prime-M35P/uSD$ sudo dd if=u-boot-sunxi-with-spl.bin of=/dev/sdx bs=1024 seek=8  
*The finished loader file compiled for display resolution 1024x600 is located in directory DOC: u-boot-sunxi-with-spl.bin*  

*Write Linux Kernel:*  
Prime-M35P/uSD$ sudo mount /dev/sdx1 /mnt  
Prime-M35P/uSD$ sudo cp zImage /mnt  
Prime-M35P/uSD$ sudo cp boot.scr /mnt  
Prime-M35P/uSD$ sudo cp sun8i-v3s-prime-m.dtb /mnt  
Prime-M35P$/uSD sync  
Prime-M35P/uSD$ sudo umount /dev/sdx1  

*Get https://disk.yandex.ru/d/VCLHKDqusnvv8A/debian12.rootfs-m.tar rootFS in uSD folder or use another build*  

*Write FS:*  
Prime-M35P/uSD$ sudo mount /dev/sdx2 /mnt  
Prime-M35P/uSD$ sudo tar -C /mnt/ -xf debian12.rootfs-m.tar  
Prime-M35P/uSD$ sync  

*To set up the network, copy the interfaces file, having previously edited it.*  
Prime-M35P/uSD$ sudo cp interfaces /mnt/etc/network/

*Linux drivers library out.zip unzip in uSD folder*  

Prime-M35P/uSD$ sudo cp -r out/lib /mnt/usr/  
Prime-M35P/uSD$ sync  
Prime-M35P/uSD$ sudo umount /dev/sdx2  
