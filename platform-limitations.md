# GRUB上平臺限制
GRUB2的設計優點為其攜帶性和移植性，所以確實是已經移植到很多的平台上。雖然官方想要把它實做成每個平台都可以運作，但是實際上卻是有些平台的支援度沒有很高。

## ARC
ARC系統沒辦法改變時間(Firmware似乎沒有提供相關功能)，用EMU的話也有相似的限制; 而且ARC也不支援serial port;用EMU的話也有相似的限制。 

## Console
Console charset只會支援firmware相關的console，像是gfxterm都只支援Unicode，Serial被設定成支援UTF-8或是ASCII。qemu和coreboot是vga_text，而Loongson總是使用gfxterm。

ASCII

Network

keyboard

USB

Chainloading

BadRAM




# 平臺限制的功能


# X86所支援的平臺
