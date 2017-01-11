想要在UNIX-like的機器上安裝GRUB，這部分就必須要用superuser來呼叫『grub-install』，這個程式使用方式很簡單，只要一個參數，就是你想要把grub安裝到哪裡，也就是一個裝置檔\(eg. /dev/sda\)。像是底下這個case，Linux會將GRUB安裝到第一個IDE disk的MBR上面:

`# grub-install /dev/hda`

`root@hugh-VirtualBox:/home/hugh\# lsblk

NAME   MAJ:MIN RM  SIZE RO TYPE MOUNTPOINT

sda      8:0    0   16G  0 disk 

├─sda1   8:1    0   14G  0 part /

├─sda2   8:2    0    1K  0 part 

└─sda5   8:5    0    2G  0 part \[SWAP\]

sdb      8:16   0  512M  0 disk 

sr0     11:0    1 1024M  0 rom  
`




