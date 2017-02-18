#安裝GRUB
想要在UNIX-like的機器上安裝GRUB，這部分就必須要用superuser來呼叫『grub-install』，這個程式使用方式很簡單，只要一個參數，就是你想要把grub安裝到哪裡，也就是一個裝置檔\(eg. /dev/sda\)。像是底下這個case，Linux會將GRUB安裝到第一個IDE disk的MBR上面:

`# grub-install /dev/hda`



```
root@hugh-VirtualBox:/home/hugh\# lsblk
NAME   MAJ:MIN RM  SIZE RO TYPE MOUNTPOINT
sda      8:0    0   16G  0 disk 
├─sda1   8:1    0   14G  0 part /
├─sda2   8:2    0    1K  0 part 
└─sda5   8:5    0    2G  0 part \[SWAP\]
sdb      8:16   0  512M  0 disk 
sr0     11:0    1 1024M  0 rom
```

`root@hugh-VirtualBox:/home/hugh# fdisk /dev/sdb ` 




```
root@hugh-VirtualBox:/home/hugh# mkfs.ext4 /dev/sdb1
```




```
root@hugh-VirtualBox:/home/hugh# parted /dev/sdb1 -l
Model: ATA VBOX HARDDISK (scsi)
Disk /dev/sdb: 537MB
Sector size (logical/physical): 512B/512B
Partition Table: msdos
Disk Flags: 

Number  Start   End    Size   Type     File system  Flags
 1      1049kB  211MB  210MB  primary  ext4


```



```
root@hugh-VirtualBox:/home/hugh# mount /dev/sdb1 /mnt
root@hugh-VirtualBox:/home/hugh# mkdir /mnt/boot
root@hugh-VirtualBox:/home/hugh# grub-install /dev/sdb --boot-directory=/mnt/boot
Installing for i386-pc platform.
Installation finished. No error reported.

root@hugh-VirtualBox:/home/hugh# ls /mnt/boot/grub/
fonts  grubenv  i386-pc  locale

root@hugh-VirtualBox:/home/hugh# umount /mnt

```

其實grub-install只是一個shell script，真正建制GRUB的任務是透過『grub-mkimage』和『grub-setup』，當然你也可以直接用這兩個指令來建制你的GRUB，但是除非你真的很熟悉GRUB的運作，最好不要這樣作，因為在一台正在運作的OS上操作這些步驟是很危險的。










