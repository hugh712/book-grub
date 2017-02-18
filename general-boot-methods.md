#GRUB的兩種啟動方式

GRUB有兩種不同的啟動方式，第一種是直接讀取作業系統，第二種是『chain-load』其他的bootloader，而這個bootloader會在讀取其他的作業系統。

實質上來說，第一種比較方便，因為你就不需要安裝並且維護其他的bootloader，而且GRUB會自動的在這個磁碟或是partition上辨識並讀取你的作業系統。但是第二種方式也是有需要存在，因為GRUB並不完全支援現存的所有作業系統。

## 直接啟動作業系統
Multiboot是GRUB本來就有支援的格式，而且Linux, FreeBSD, NetBSD 和OpenBSD也都支援，除了上敘以外，如果你想要啟動其他的作業系統，你就需要用到chain-load。

在kernel和root filesystem都載入的狀況之下，要直接啟動作業系統的話，只要一個指令-『boot』就好了，這部份只要先知道這個就好，後面會有完整的case。而如果是要啟動DOS或是Windows的話，需要有特殊的作法，這邊就不探討，有需要的可以直接看官方手冊。

## 使用Chain-loading
如果作業系統沒有支援Multiboot而且在GRUB裡面也沒有支援這個作業系統的話，那就必須要用chain-loaded的方式，這個方式主要是讀取另一個boot loader並且在real mode底下跳到那個位址上去，但是Chain-loading的方式只有在PC BIOS和EFI平台上支援，這邊要特別注意一下。

這部份的話就需要用到命令『chainloader』，使用這個之前通常需要先設定你的GRUB modules和設定你的root device，所以將以上的資訊全部都湊齊之後，會有如下的格式，主要是描述在windows系統底下的第一顆磁碟的第一個partition：

```
menuentry "Windows" {
	insmod chain
	insmod ntfs
	set root=(hd0,1)
	chainloader +1
}
```




