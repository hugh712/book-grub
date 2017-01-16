除了直接讀取作業系統和chain-loader的方式以外，GRUB也可以從任何可存取的儲存裝置上讀取映像檔，但是首先作業系統必須要有辦法找到他的root才行。但是這個動作通常需要用到userspace的程式才行，但是因為這時候真正的root filesystem還沒辦法讀取，所以這時候就要透過GRUB來讀取特殊的映像檔，並且將它當成ramdisk傳遞給kernel。這部份的話就要取決於loader然後透過多組的命令來完成：『kfreebsd_module, knetbsd_module_elf, kopenbsd_ramdisk, initrd, initrd16, multiboot_module, multiboot2_module or xnu_ramdisk』。

對於knetBSD的話，這個映像檔必須要被放到miniroot.kmod裡面，並且這整個miniroot.kmod必須先被讀進去;在kopenbsd則是預設就被設定成disabled。至於初始化ramdisk的其他行為都取決於CLI的參數，數種distros因為這個參數，所以將相關的元件都已經整合到它們的standard ramdisk裡面了，想要了解這部分的話，就要翻一下你的kernel或是distro的文件。有部分的loader像是appleloader, chainloader (BIOS, EFI, coreboot), freedos, ntldr和plan9等等則是沒有提供這個讀取initial ramdisk的功能，如果你的loader是上敘這些不支援initial ramdisk的話，建議可以使用將映像檔裡面的檔案整個複製到相關partition裡面。