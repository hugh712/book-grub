# GRUB上平臺限制

GRUB2的設計優點為其攜帶性和移植性，所以確實是已經移植到很多的平台上。雖然官方想要把它實做成每個平台都可以運作，但是實際上卻是有些平台的支援度沒有很高，底下是一些平台上的差異:

## ARC

- ARC系統沒辦法改變時間\(Firmware似乎沒有提供相關功能\)，用EMU的話也有相似的限制; 
- 而且ARC也不支援serial port;用EMU的話也有相似的限制。

## Console

Console charset只會支援firmware相關的console，像是gfxterm都只支援Unicode，Serial被設定成支援UTF-8或是ASCII，qemu和coreboot是vga\_text，而Loongson總是使用gfxterm。

限制最多的應該是ASCII，像是CP437提供了額外pseudographics，因為GRUB2並不使用從CP437來的語言文字，所以CP437總是因為相容的關係，被取代成這些pseudographics。而Unicode當然就是支援最多的charset，但是也是要取決於firmware的支援就對了。

## Network

在BIOS上的網路也有些限制，只有在你的image是通過網路讀取的才能使用網路。在sparc64上的GRUB就無法決定它是從哪個server上啟動的。

## Serial

如果平台上沒有支援的serial的話，只要firmware支援的話，你依然可以直接將firmware給導到console上。

## USB

USB有在ATA和AT上提供支援，在ATA上支援USB disk，而在AT上則是支援USB鍵盤，而且兩個都支援USB serial。

## Chainloading

chainloading的部分因為牽涉到使用相同的協定來讀取其它的bootloader，這部分需要藉由命令『search』的option -『hints』來達成，這個選項允許使用預先預測的機制，如果是在同一個平台的話，這個預測是很準的，除非在兩次開機間你有移動你disk的介面，才有可能會失敗; 但是在不同平台上這個預測機制會經過『訓練』，所以有可能會失敗，但是失敗的話只是降低效能，不代表結果失敗。

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
有些平臺有實做一些平台依賴的功能，列出如底下：

## 資訊萃取
- mipsel-loongson: lsspd
- mips-arc: lsdev
- efi: lsefisystab, lssal, lsefimmap
- i386-pc: lsapm
- acpi-enabled (i386-pc, i386-coreboot, i386-multiboot, *-efi): lsacpi

## 解決一些平台相依的問題
- i386-efi/x86_64-efi: loadbios, fixvideo
- acpi-enabled (i386-pc, i386-coreboot, i386-multiboot, *-efi): acpi (覆蓋 ACPI tables)
- i386-pc: drivemap
- i386-pc: sendkey

## 其他
- x86: iorw (直接存取 I/O ports)
- cmos (x86-*, ieee1275, mips-qemu_mips, mips-loongson): cmostest (在有些筆電上用來檢查特殊的電源鍵)
- i386-pc: play


# X86所支援的平臺
官方有整理一個x86架構支援的表格，『Yes』的意思就是kernel可以在這個平台上運作，『crashes』代表在之前的kernel會有問題，它們會跟相關的kernel工程師一起解決這些問題，『no』表示GRUB裡面沒有支援，『headless』表示kernel還是可以運作，但是少了console的driver，但是你還是可以藉由serial還是網路來操作，至於其他的不在上敘的原因則個別在底下註解。

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
<br><br>

||Multiboot|	Qemu|
| :--- | :--- |:---|
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
<br><br>


||ia32 EFI|	amd64 EFI|
| :--- | :--- |:---|
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
<br><br>


||ia32 IEEE1275|
| :--- | :--- |
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

1. 需要BIOS。
2. 因為記憶體位置0x0-0x1000不可存取。
3. EFI only。
4. 32-bit和64-bit EFI 的結構不一樣，而且運作在不同的CPU模式上，所以不可能在64-bit平台上chainload到32-bit的bootloader上，相對也無法在632-bit的平台chainload到64-bit的bootloader上。
5. 有些modules也許必須被關閉。
6. 需要ACPI的支援。
PowerPC, IA64 and Sparc64的ports只有支援Linux，而MIPS的ports支援Linux和multiboot2。

