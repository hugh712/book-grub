#安裝GRUB
如果要安裝GRUB當成你的bootloader，第一件事就是要在你的UNIX-like系統裡面安裝GRUB系統和套件，可以用source tarball和你的distro上面的package去安裝。下一步，接下來你就需要用套件『grub-install』安裝你的bootloader到相對應的磁碟上去。

在GRUB裡會用到boot images，通常都會放在『/usr/lib/grub/&lt;cpu>-&lt;platform>』(假設是在BIOS系統的機器，路徑就會是/usr/lib/grub/i386-pc)，所以接下來有兩個路徑就要記清楚:

- image directory<br>
就是剛剛說的，GRUB images預設安裝的資料夾。
- boot directory<br>
bootloader存放的資料夾，通常是『/boot』。
    
    