GRUB是由許多image所組成的，一系列的bootstrap images\(對應各種方式開啟GRUB\)，一個kernel image，一系列的modules會跟kernel image綁在一起然後組成core image。在我的電腦，這些檔案都在路徑『/usr/lib/grub/i386-pc』底下。

# boot.img

在PC BIOS系統上，這個image是在GRUB上第一個執行的部分，這個image是將其寫成MBR或是partition的boot sector，因為PC boot sector是512 bytes，所以這個image的大小也剛好是512 bytes。這個image唯一的功用就是從你的disk裡面的core image，將其第一個sector讀出來，然後將控制權交給core image。因為size的限制，所以這個image不可能知道任何的檔案結構，所以grub-setup會將boot.img的第一個sector的位址給hardcode到裡面。

```
# ll boot.img; file boot.img
-rw-r--r-- 1 root root 512  一  25 08:49 boot.img
boot.img: DOS/MBR boot sector
```

# diskboot.img
當你從硬碟(hard disk)開機時，這個image會被當成core image的第一個sector，它會將剩下的core image讀入記憶體然後將控制權交給kernel，因為在這個時間點檔案系統還沒好，所以會將core image的位址用block list的格式給編碼進這個image。

```
# ll diskboot.img; file diskboot.img
-rw-r--r-- 1 root root 512  六  17  2016 diskboot.img
diskboot.img: data
```

# cdboot.img
如果你是用CD-ROM開機的話，這個image就會被當成core image的第一個sector。行為來說就跟『diskboot.img』一樣。

```
# ll cdboot.img; file cdboot.img
-rw-r--r-- 1 root root 2048  六  17  2016 cdboot.img
cdboot.img: data
```

# pxeboot.img
當你透過網路用PXE開機的話，這個image就會被當成core image的第一個sector。


# lnxboot.img

# kernel.img

# core.img

# \*.mod



