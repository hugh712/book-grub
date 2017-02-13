# 自制開機menu組態

GRUB的multi-boot環境取決於os-prober，也就是在『grub-install』執行以後，GRUB會探測你目前有多少種的kernel和其他作業系統然後幫你輸出到『grub.cfg』裡。

除了Linux和Hurd以外，GRUB2也支援像是FreeBSD，NetBSD和OpenBSD等等的作業系統，並且只要你的作業系統是用multiboot規格去編譯的話，也都可以用GRUB2來開機。

這個章節來介紹一下，怎麼自製的簡單『grub.cfg』組態:

## Linux  
根據章節『Making a GRUB bootable CD-ROM』的步驟，先建立相關資料夾，安裝grub，然後在掛載起來的路徑『/mnt/boot/grub/』底下建立一個『grub.cfg』，內容如下：
```
menuentry "my Ubuntu 16.04" {
        set root=(hd0,msdos1)
        linux /vmlinuz root=UUID=8c9eb01d-b58b-4e19-acdb-e1028004a637
        initrd /initrd.img
}
```
然後在將grub給安裝到目錄下，然後將以上的所有內容給建立救援映像檔：<br>

```
grub-mkrescue -o grub.iso iso
```
接下來將這個映像檔給掛載起來以後重開機，直接看到以下畫面:
![](Imgs/Config/config004.png)
按『e』看一下裡面的內容如下:
![](Imgs/Config/config005.png)
然後直接按『F10』應該就沒問題可以直接開機了。


## FreeBSD
GRUB2可以使用命令『kfreebsd』來啟動FreeBSD kernel，流程的話如下:


1.設定FreeBSD kernel所在的partition
```
set root=(/dev/ad4,msdos1)
```
2.讀取kernel 
```
kfreebsd /boot/kernel/kernel
```
3.讀取 kernel boot information 
```
kfreebsd_loadenv /boot/device.hints
```
4.設定 root裝置的路徑
```
set kFreeBSD.vfs.root.mountfrom=ufs:/dev/ad4s1a
```
5.設定file-system的options
```
vfs.root.mountfrom.options=rw
```
6.最後，以剛剛的kernel和root file-system啟動
```
boot
```

如果想要使用自制的『grub.cfg』的話，可以拿下面這個例子來加在你的『/etc/grub.d/40_custom』裡面在加以修改:
```
menuentry "FreeBSD 8.0 direct" {
        insmod ufs2
        set root='(/dev/ad4,msdos1)'
        search --no-floppy --fs-uuid --set 4c0029f407b3cd1d
        kfreebsd /boot/kernel/kernel
        kfreebsd_loadenv /boot/device.hints
        kfreebsd_module /boot/splash.bmp type=splash_image_data
        set kFreeBSD.vfs.root.mountfrom=ufs:ad4s1a
}
```
不確定你的UUID的話，可以用以下指令:
```
ls (hd0,1)
```
如果你想要傳遞參數給FreeBSD bootloader的option的話(/boot/loader.conf)，可以直接使用『set』命令，如下面例子:

```
# 強制叫kernel等USB出現
set kFreeBSD.kern.cam.boot_delay="10000"
```

## NetBSD
GRUB2可以使用命令『knetbsd 』來啟動NetBSD kernel，流程的話如下:

1.設定NetBSD kernel所在的partition，如果你的NetBSD是安裝在第一個disk的第一個partition的話
```
set root=(hd0,msdos1)
```
2.讀取kernel並且指定root裝置的路徑
```
knetbsd /netbsd --root=wd0a
```
3.啟動kernel
```
boot
```

一樣，如果想要使用自制的『grub.cfg』的話，可以拿下面這個例子來加在你的『/etc/grub.d/40_custom』裡面在加以修改:
```
menuentry "NetBSD on sda1" {
        insmod ufs2
        set root=(hd0,msdos1)
        knetbsd /netbsd --root=wd0a
}
```

## Generic Multi-Boot
想要啟動一個multi-boot相容的kernel，你在讀取kernel時，必須要用命令『multiboot』來讀取，有個例子可以讓你練習一下，先下載『[Grub Invaders](http://www.erikyyy.de/invaders)』，然後解壓縮放到路徑『/boot』。接下來執行下面兩個步驟，沒意外的話你就會看到『invaders』已經被啟動了。

1.讀取Grub invaders
```
multiboot /boot/invaders/invaders
```
2.啟動
```
boot
```
## Chain Loading
如果想要使用FreeBSD，NetBSD或是Windows的boot程式的話，就要使用chain load來指定特定的partition。通常一般的entry會像這樣:
```
menuentry "FreeBSD"{
    set root=(hd0,msdos1)
    chainloader +1
}
```
而如果你有兩個版本以上的Ubnutu或是多種的作業系統安裝的話，最好就不要使用chainload，而是要在『/etc/grub.d/40_custom』加入像底下這樣子的entry:
```
menuentry "Yet another distro/installation/encrypted Ubuntu installation/..." { 
               set root=(hd0,msdosX) 
               configfile /boot/grub/grub.cfg 
}
```
上面這個例子，如果你的目標作業系統的『/boot』是在『/dev/sda5』的話，那那個X就會是5，並且使用『configfile』來切換會比使用『multiboot』來的好，因為在Ubuntu 12.04時，multiboot通常會指到『/boot/grub/core.img』，但是在14.04以後『core.img』的位置換到了『/boot/grub/i386-pc/core.img』，所以如果使用multiboot時，系統會有可能混亂。

在修改好你的客製化menu以後，接下來下一步就是在檔案『/etc/default/grub』裡面將『os_prober』關掉，並且更新組態:

```
GRUB_DISABLE_OS_PROBER=true
```
最後記得『update-grub』。





