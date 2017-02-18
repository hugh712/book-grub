#建立可啟動的CD-ROM GRUB image
GRUB也可以直接由CD-ROM或是USB上驅動，這部分需要一份image叫做 -『cdboot.img』，然後還有另一個image -『core.img』。core.img的使用至少應該有『iso9660』和『biosdisk』模組，而你的CD-ROM通常也需要包含組態檔-『grub.cfg』和其他的模組，總之就像如下公式:

`GRUB CD-ROM = cdboot.img + core.img + [grub.cfg] + [modules]`

底下說明一下如果要建立一個簡單的GRUB rescue CD要怎麼做，這部份需要用到一個程式叫做-『grub-mkrescue』，使用這個程式需要先安裝『xorriso』套件:

```
root@hugh-VirtualBox:/home/hugh# apt-get install xorriso
```

xorriso是一個可以從POSIX相容的檔案系統裡將檔案給製作成『Rock Ridge enhanced ISO 9660』格式的檔案系統映像檔程式。grub-mkrescue裡面主要會用到xorriso和mkisofs，這邊只要先知道有用到這兩支就好了，細節就先不探討。

1.首先，要先建立一個最上層的資料夾:
```
root@hugh-VirtualBox:/home/hugh# mkdir iso
```

2.然後為GRUB建立資料夾
```
root@hugh-VirtualBox:/home/hugh# mkdir -p iso/boot/grub
```

3.有需要的話，可以將相關的組態還是moudles給複製到grub資料夾裡:

```
root@hugh-VirtualBox:/home/hugh# cp /boot/grub/grub.cfg iso/boot/grub/
```

4.所以假設現在grub資料夾裡面已經有所有的資料了，就可以來建立映像檔了，只要一行簡單的指令\(底下也列出相關結果\):

```
root@hugh-VirtualBox:/home/hugh# grub-mkrescue -o grub.iso iso
xorriso 1.4.2 : RockRidge filesystem manipulator, libburnia project.

Drive current: -outdev 'stdio:grub.iso'
Media current: stdio file, overwriteable
Media status : is blank
Media summary: 0 sessions, 0 data blocks, 0 data, 9512m free
Added to ISO image: directory '/'='/tmp/grub.HVxC3C'
xorriso : UPDATE : 281 files added in 1 seconds
Added to ISO image: directory '/'='/home/hugh/iso'
xorriso : UPDATE : 284 files added in 1 seconds
xorriso : NOTE : Copying to System Area: 512 bytes from file '/usr/lib/grub/i386-pc/boot_hybrid.img'
ISO image produced: 2540 sectors
Written to medium : 2540 sectors at LBA 0
Writing to 'stdio:grub.iso' completed successfully.
```

5.檢查檔案格式<br>
```
root@hugh-VirtualBox:/home/hugh# file grub.iso
grub.iso: DOS/MBR boot sector; GRand Unified Bootloader, stage1 version 0x79, boot drive 0xbb, stage2 address 0x8e70, 1st sector stage2 0xb8db31c3, stage2 segment 0x201 ISO 9660 CD-ROM filesystem data (DOS/MBR boot sector) 'ISOIMAGE' (bootable)
```

如上面所看到的，產生了一個『grub.iso』，接下來你就可以把這個image給燒入CD-ROM或是USB裡面以後，放入相關媒體重新開機後，你的機器一開始應該就會讀到了。

