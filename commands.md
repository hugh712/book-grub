# GRUB 可用的命令
這一章要來探討一下到底GRUB裡面有多少的命令,但是特別注意的是在『開機階段』控制權在GRUB階段時可用的命令，不是控制權給kernel以後的相關GRUB命令。

GRUB的命令分為兩個群組:
1. 只能在menu使用。
2. menu和command-line都能使用(general commands)。

# menu only


## menuentry

## submenu


# general commands

## serial

## terminal_input

## terminal_output

## terminfo

 acpi:	  	
• badram:	  	
• blocklist:	  	
• boot:	  	
• cat:	  	
• chainloader:	  	
• cmp:	  	
• configfile:	  	
• cpuid:	  	
• crc:	  	
• date:	  	
• drivemap:	  	
• echo:	  	
• export:	  	
• false:	  	
• gettext:	  	
• gptsync:	  	
• halt:	  	
• help:	  	
• initrd:	  	Load a Linux initrd
• initrd16:	  	Load a Linux initrd (16-bit mode)
• insmod:	  	Insert a module
• keystatus:	  	Check key modifier status
• linux:	  	Load a Linux kernel
• linux16:	  	Load a Linux kernel (16-bit mode)
• list_env:	  	List variables in environment block
• load_env:	  	Load variables from environment block
• loopback:	  	Make a device from a filesystem image
• ls:	  	List devices or files
• normal:	  	Enter normal mode
• normal_exit:	  	Exit from normal mode
• parttool:	  	Modify partition table entries
• password:	  	Set a clear-text password
• password_pbkdf2:	  	Set a hashed password
• play:	  	Play a tune
• pxe_unload:	  	Unload the PXE environment
• read:	  	Read user input
• reboot:	  	Reboot your computer
• save_env:	  	Save variables to environment block
• search:	  	Search devices by file, label, or UUID
• sendkey:	  	Emulate keystrokes
• set:	  	Set an environment variable
• true:	  	Do nothing, successfully
• unset:	  	Unset an environment variable
• uppermem:	  	Set the upper memory size