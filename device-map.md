因為早期的歷史因素，所以從BIOS轉移給GRUB時，在BIOS driver和OS device之間的map並不能保證每一次都成功\(舉個例子來說，如果你在BIOS裡面改變你的IDE和SCSI的開機順序的話，GRUB會拿到錯的順序\)，而GRUB又需要在組態檔裡面使用從BIOS drive numbers所擷取出來的device name，所以就需要用到這個device map來確保對映成功。

因為device map在GRUB2上並不是預設，所以如果要建立出相關的device map需要用到底下的指令：

`sudo grub-mkdevicemap`

這個指令會將device.map給安裝到/boot/grub/裡面，所以如果這個檔案存在的話，GRUB的相關程式就會將它從BIOS讀取到OS device，這個檔案的組成如下:

\(device\) file

看一下剛剛我產生的device.map


```
vim /boot/grub/device.map

(hd0)   /dev/disk/by-id/ata-VBOX_HARDDISK_VB3b4a075c-2d880932

root@hugh-VirtualBox:/boot/grub# ls -la /dev/disk/by-id/ata-VBOX_HARDDISK_VB3b4a075c-2d880932
lrwxrwxrwx 1 root root 9  一  14 13:53 /dev/disk/by-id/ata-VBOX_HARDDISK_VB3b4a075c-2d880932 -> ../../sda

```






