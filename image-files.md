GRUB是由許多image所組成的，一系列的bootstrap images\(對應各種方式開啟GRUB\)，一個kernel image，一系列的modules會跟kernel image綁在一起然後組成core image。在我的電腦，這些檔案都在路徑『/usr/lib/grub/i386-pc』底下。

# boot.img

在PC BIOS系統上，這個image是在GRUB上第一個執行的部分，這個image是將其寫成MBR或是partition的boot sector，因為PC boot sector是512 bytes，所以這個image的大小也剛好是512 bytes。這個image唯一的功用就是從你的disk裡面的core image，將其第一個sector讀出來，然後將控制權交給core image。

# diskboot.img

# cdboot.img

# pxeboot.img

# lnxboot.img

# kernel.img

# core.img

# \*.mod



