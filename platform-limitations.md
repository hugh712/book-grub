# GRUB上平臺限制

GRUB2的設計優點為其攜帶性和移植性，所以確實是已經移植到很多的平台上。雖然官方想要把它實做成每個平台都可以運作，但是實際上卻是有些平台的支援度沒有很高，底下是一些平台上的差異:

## ARC

ARC系統沒辦法改變時間\(Firmware似乎沒有提供相關功能\)，用EMU的話也有相似的限制; 而且ARC也不支援serial port;用EMU的話也有相似的限制。

## Console

Console charset只會支援firmware相關的console，像是gfxterm都只支援Unicode，Serial被設定成支援UTF-8或是ASCII。qemu和coreboot是vga\_text，而Loongson總是使用gfxterm。

限制最多的應該是ASCII，像是CP437提供了額外pseudographics，因為GRUB2並不使用從CP437來的語言文字，所以CP437總是因為相容的關係，被取代成這些pseudographics。而Unicode當然就是支援最多的charset，但是也是要取決於firmware的支援就對了。

## Network

在BIOS上的網路也有些限制，只有在你的映像檔是通過網路讀取的才能使用網路。在sparc64上的GRUB就無法決定它是從哪個server上啟動的。

## Serial

如果平台上沒有支援的serial的話，只要firmware支援的話，你依然可以直接將firmware給導到concole上。

## USB

USB有在ATA和AT上提供支援，在ATA上支援USB disk，而在AT上則是支援USB鍵盤，而且兩個都支援USB serial。

## Chainloading

chainloading的部分因為牽涉到使用相同的協定來讀取其它的bootloader，這部分需要藉由命令『search』的option-『hints』來達成，這個選項允許使用預先預測的機制，如果是在同一個平台的話，這個預測是很準的，除非在兩次開機間你有移動你disk的介面; 但是在不同平台上這個預測機制會經過『訓練』，所以有可能會失敗，但是失敗的話只是降低效能，不代表結果失敗。

## BadRAM

BadRAM的部分，因為協定的限制，所以mips-loongson\(Linux 協定\)和mips-qemu\_mips只能使用記憶體上的第一個『hole』。

## Limitation Table

底下列出官方所發布的限制:


|      |BIOS  |Coreboot|Multiboot|Qemu|
| :--- | :--- |:---    |:---     |:---|  
| video|yes   |yes     |yes      |yes |  
|console charset|    CP437|    CP437|    CP437|    CP437|  
|network|    yes \(\*\)|    no|    no|    no|  
|ATA/AHCI|    yes|    yes|    yes|    yes|  
|AT keyboard|    yes|    yes|    yes|    yes|  
|USB|    yes|    yes|    yes|    yes|  
|chainloader|    local|    yes|    yes|    no|  
|cpuid|    partial|    partial|    partial|    partial|  
|hints|    guess|    guess|    guess|    guess|  
|PCI|    yes|    yes|    yes|    yes|  
|badram|    yes|    yes|    yes|    yes|  
|compression|    always|    pointless|    no|    no|  
|exit    |yes    |no    |no    |no|
<br>
<br>

|	|ia32 EFI|	amd64 EFI|	ia32 IEEE1275|	Itanium|
| :--- | :--- |:---    |:---     |:---|  
|video|	yes|	yes|	no|	no|
|console charset|Unicode|Unicode|ASCII|Unicode|
|network|	yes|	yes|	yes|	yes|
|ATA/AHCI|	yes|	yes|	yes|	no|
|AT keyboard|	yes|	yes|	yes|	no|
|USB|	yes|	yes|	yes|	no|
|chainloader|	local|	local|	no|	local|
|cpuid|	partial|partial|partial|no|
|hints|	guess|	guess|	good|	guess|
|PCI|	yes|	yes|	yes|	no|
|badram|	yes|	yes|	no|	yes|
|compression|	no|	no|	no|	no|
|exit|	yes|	yes|	yes|	yes|
<br>
<br>

||Loongson|sparc64|Powerpc|ARC|
| :--- | :--- |:---    |:---     |:---|  
|video|	yes|	no|	yes|	no|
|console charset|	N/A|	ASCII|	ASCII|	ASCII|
|network|no|yes (*)|yes|no|
|ATA/AHCI|	yes|	no|	no|	no|
|AT keyboard|	yes|	no|	no|	no|
|USB|	yes|	no|	no|	no|
|chainloader|	yes|	no|	no|	no|
|cpuid|	no|	no|	no|	no|
|hints|	good|	good|	good|	no|
|PCI|	yes|	no|	no|	no|
|badram|yes (*)| no|	no|	no|
|compression|	configurable|	no|	no|	configurable|
|exit|	no|	yes|	yes|	yes|
<br>
<br>

||MIPS qemu|	emu|||
| :--- | :--- |:---    |:---     |:---|  
|video|	no|	yes|||
|console charset|	CP437|	ASCII|||
|network|no|	yes|||
|ATA/AHCI|yes|	no|||
|AT keyboard	|yes|	no|||
|USB	        |N/A|   yes|||
|chainloader	|yes|	 no|||
|cpuid|	no|	no|||
|hints|	guess|	no|||
|PCI|	no|	no|||
|badram	|yes (*)	|no|||
|compression|	configurable|	no|||
|exit|	no|	yes|||

# 平臺限制的功能

# X86所支援的平臺


|	|BIOS|	Coreboot|
| :--- | :--- |:---|
|BIOS| chainloading|	yes|	no (1)|
|NTLDR|	yes|	no (1)|
|Plan9|	yes|	no (1)|
|Freedos|	yes|	no (1)|
|FreeBSD| bootloader	yes|	crashes (1)|
|32-bit| kFreeBSD	yes|	crashes (2,6)|
|64-bit| kFreeBSD	yes|	crashes (2,6)|
|32-bit| kNetBSD	yes|	crashes (1)|
|64-bit| kNetBSD	yes|	crashes (2)|
|32-bit| kOpenBSD	yes|	yes|
|64-bit| kOpenBSD	yes|	yes|
|Multiboot|	yes|	yes|
|Multiboot2|	yes|	yes|
|32-bit Linux (legacy protocol)|	yes|	no (1)|
|64-bit Linux (legacy protocol)	|yes|	no (1)|
|32-bit Linux (modern protocol)	|yes|	yes|
|64-bit Linux (modern protocol)	|yes|	yes|
|32-bit XNU|	yes|	?|
|64-bit XNU|	yes|	?|
|32-bit EFI chainloader|	no (3)|	no (3)|
|64-bit EFI chainloader|	no (3)| no (3)|
|Appleloader|	no (3)|	no (3)|
||Multiboot|	Qemu|
|BIOS chainloading|	no (1)|	no (1)|
|NTLDR|	no (1)|	no (1)|
|Plan9|	no (1)|	no (1)|
|FreeDOS|	no (1)|	no (1)|
|FreeBSD bootloader|	crashes (1)|	crashes (1)|
|32-bit kFreeBSD|	crashes (6)|	crashes (6)|
|64-bit kFreeBSD|	crashes (6)|	crashes (6)|
|32-bit kNetBSD|	crashes (1)|	crashes (1)|
|64-bit kNetBSD|	yes|	yes|
|32-bit kOpenBSD|	yes|	yes|
|64-bit kOpenBSD|	yes|	yes|
|Multiboot|	yes|	yes|
|Multiboot2|	yes|	yes|
|32-bit Linux (legacy protocol)|no (1)|no (1)
|64-bit Linux (legacy protocol)	|no (1)|no (1)|
|32-bit Linux (modern protocol)	|yes|yes|
|64-bit Linux (modern protocol)	|yes|	yes|
|32-bit XNU|	?|	?|
|64-bit XNU|	?|	?|
|32-bit EFI chainloader|	no (3)|	no (3)|
|64-bit EFI chainloader|	no (3)| no (3)|
|Appleloader|	no (3)|	no (3)|
||ia32 EFI|	amd64 EFI|
|BIOS chainloading|	no (1)|	no (1)|
|NTLDR|	no (1)|	no (1)|
|Plan9|	no (1)|	no (1)|
|FreeDOS|	no (1)|	no (1)|
|FreeBSD bootloader|	crashes (1)|	crashes (1)|
|32-bit kFreeBSD|	headless|	headless|
|64-bit kFreeBSD|	headless|	headless|
|32-bit kNetBSD|	crashes (1)|	crashes (1)|
|64-bit kNetBSD|	yes|	yes|
|32-bit kOpenBSD|	headless|	headless|
|64-bit kOpenBSD|	headless|	headless|
|Multiboot|	yes|	yes|
|Multiboot2|	yes|	yes|
|32-bit Linux (legacy protocol)|	no (1)|	no (1)|
|64-bit Linux (legacy protocol)	|no (1)|no (1)|
|32-bit Linux (modern protocol)	|yes|	yes|
|64-bit Linux (modern protocol)	|yes|	yes|
|32-bit XNU|	yes|	yes|
|64-bit XNU|	yes (5)|	yes|
|32-bit EFI chainloader|	yes|	no (4)|
|64-bit EFI chainloader|	no (4)|	yes|
|Appleloader|	yes|	yes|
||ia32 IEEE1275|
|BIOS chainloading|	no (1)|
|NTLDR|	no (1)|
|Plan9|	no (1)|
|FreeDOS|	no (1)|
|FreeBSD bootloader|	crashes (1)|
|32-bit kFreeBSD|	crashes (6)|
|64-bit kFreeBSD|	crashes (6)|
|32-bit kNetBSD|	crashes (1)|
|64-bit kNetBSD|	?|
|32-bit kOpenBSD|	?|
|64-bit kOpenBSD|	?|
|Multiboot|	?|
|Multiboot2|	?|
|32-bit Linux (legacy protocol)|	no (1)|
|64-bit Linux (legacy protocol)	|no (1)|
|32-bit Linux (modern protocol)	|?|
|64-bit Linux (modern protocol)	|?|
|32-bit XNU|	?|
|64-bit XNU|	?|
|32-bit EFI chainloader|	no (3)|
|64-bit EFI chainloader	|no (3)|
|Appleloader|	no (3)|


