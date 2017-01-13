GRUB上的裝置名稱有它的特殊語法，所以使用GRUB第一件事，就是要知道這些語法，不然你會不知道如何去找到對的裝置\(device\)/分區\(partition\)。第一個要知道的是，GRUB對裝置的描述一定要在成對的小括號『\(\)』裡面，語法如下:

```
(device[,partmap-name1part-num1[,partmap-name2part-num2[,...]]])
```
BIOS和EFI使用『fd』或是『hd』然後後面在加一個數字；AHCI, PATA (ata), crypto和USB使用driver的名稱在加一個編號；Memdisk和host則是被限制只能有一個disk，所以只會有一個driver名稱；RAID (md), ofdisk (ieee1275 和 nand), LVM (lv), LDM 和 arcdisk (arc)則是使用disk固有的名稱前面在加driver的名稱；

底下先來看一個例子:

`(fd0)`

fd代表的是軟碟\(floppy disk\)，0代表的是磁碟\(drive\)編號，GRUB的disk number是從0開始，所以這個裝置檔描述代表的是GRUB會用到整個floppy disk。底下第二個例子:

`(hd0,msdos2)`

這個例子，hd代表的是硬碟『hard disk drive』，0一樣代表是disk number，所以就是第一顆硬碟。『msdos』代表的是『[partition scheme](https://en.wikipedia.org/wiki/Disk_partitioning)』，2代表的是分區『partition』編號\(又或者是在BSD上的PC slice number\)，之前有說過disk number是從0開始，但是這邊要注意的是，partition number卻是從1開始，所以整個描述就是代表它是第一顆disk的第二個partion。

`(hd0,msdos5)`

上面這個例子代表的是第一顆disk的第一個『extended partition』延伸分區，在GRUB裡面要特別注意的是『extended partition』的編號是從5開始，不管你這顆硬碟上前面有多少個『primary partition』。

在GRUB裡面想要存取disk或是partition，你都要用相對應的語法來存取，像是底下的兩個case:

`set root=(fd0)`

`parttool (hd0,msdos3) hidden-`

為方便使用者找到相關的device，GRUB也提供了argument completion，像是底下這個case，你只要按『tab』以後，GRUB就會列出所有的disk，partition甚至是檔案名稱:

![](Imgs/Name/Name001.PNG)

另外一件事要特別注意的是，GRUB並沒有特別區分IDE和SCSI，不管磁碟的介面，都是直接從0開始計算。一般來說，通常IDE介面會比SCSI的號碼還要小，雖然說如果你在BIOS裡面交換你的IDE和SCSI的開機順序的話，並不會直接反映在剛剛的規則上就對了。

所以到這邊我們已經有disk和partition了，接下來就只剩下檔案，看一下底下的Case:

![](Imgs/Name/Name002.PNG)

描述的是第一個disk上的第一個partition上的檔案vmlinuz，argument completion也是用在檔案的部分。

