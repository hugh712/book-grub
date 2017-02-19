# GRUB Frozen
如果只有螢幕左上角有個『GRUB』，但是沒有任何反應的話，代表GRUB2連MBR或是開機磁區的基本資訊都找不到。因此，『core.img』和『/boot/gurb』的位置GRUB2完全都抓不到。

![](Imgs/Fix/Fix004.PNG)

在這個況況底下，因為連GRUB2都不能用了，所以一定要用到其他的作業系統還是LiveCD，然後使用『chroot』到損壞的partition裡面去重新安裝GRUB2。這部份更進接的訊息請參考『[Fixing a Broken System](https://hugh712.gitbooks.io/grub/content/fixing-a-broken-system.html)』
	



