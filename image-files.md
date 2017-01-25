GRUB是由許多image所組成的，一系列的bootstrap images\(對應各種方式開啟GRUB\)，一個kernel image，一系列的modules會跟kernel image綁在一起然後組成core image。在我的電腦，這些檔案都在路徑『/usr/lib/grub/i386-pc』底下。

# boot.img

在PC BIOS系統上，這個image是在GRUB上第一個執行的部分，這個image是將其寫成MBR或是partition的boot sector，因為PC boot sector是512 bytes，所以這個image的大小也剛好是512 bytes。這個image唯一的功用就是從你的disk裡面的core image，將其第一個sector讀出來，然後將控制權交給core image。因為size的限制，所以這個image不可能知道任何的檔案結構，所以grub-setup會將boot.img的第一個sector的位址給hardcode到裡面。

```
# ll boot.img; file boot.img
-rw-r--r-- 1 root root 512  一  25 08:49 boot.img
boot.img: DOS/MBR boot sector
```

# diskboot.img





```
# ll diskboot.img; file diskboot.img
-rw-r--r-- 1 root root 512  六  17  2016 diskboot.img
diskboot.img: data
```





# cdboot.img

# pxeboot.img

# lnxboot.img

# kernel.img

# core.img

# \*.mod



