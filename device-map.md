#Device Map
因為早期的歷史因素，所以從BIOS轉移給GRUB時，在BIOS driver和OS device之間的map並不能保證每一次都成功\(舉個例子來說，如果你在BIOS裡面改變你的IDE和SCSI的開機順序的話，GRUB會拿到錯的順序\)，而GRUB又需要在組態檔裡面使用從BIOS drive numbers所擷取出來的裝置名稱，所以就需要用到這個裝置名稱來確保對映成功。

因為device map在GRUB2上並不是預設，所以如果要建立出相關的device map需要用到底下的指令：

`sudo grub-mkdevicemap`

這個指令會將device.map給安裝到/boot/grub/裡面，所以如果在開機時這個檔案存在的話，GRUB的相關程式就會將它從BIOS讀取到OS device，這個檔案的組成如下:

```
(device) file
```

看一下剛剛我產生的device.map，內容是指到另一個路徑的檔案，而且這個檔案又是一個連結檔，又指到『/dev/sda』這個裝置。


```
root@hugh-VirtualBox:/boot/grub# cat device.map
(hd0)   /dev/disk/by-id/ata-VBOX_HARDDISK_VB3b4a075c-2d880932

root@hugh-VirtualBox:/boot/grub# ls -la /dev/disk/by-id/ata-VBOX_HARDDISK_VB3b4a075c-2d880932
lrwxrwxrwx 1 root root 9  一  14 13:53 /dev/disk/by-id/ata-VBOX_HARDDISK_VB3b4a075c-2d880932 -> ../../sda
```

但是不幸的是，OS的裝置名稱也常常不穩定，Linux kernel也是常常在開機途中修改到這部份，『prefix』也是會根據不同的driver subsystem的使用狀況而改變，所以就是在某些系統上的device.map需要很常的去修改。

GRUB為了避免以上提到的所有問題，所以在產生grub.cfg時都採用UUID或是file system label的作法，聽起來好像這個device.map差不多快被淘汰掉了，但是其實有些狀況還是需要它，像是如果你的開機環境跟你OS的環境不一樣時(eg. 使用虛擬機裡面使用LVM或partition...)。





