# GRUB 可用的命令
這一章要來探討一下到底GRUB裡面有多少的命令,但是特別注意的是在『開機階段』控制權在GRUB階段時可用的命令，不是控制權給kernel以後的相關GRUB命令。

GRUB的命令分為兩個群組:
1. 只能在menu使用。
2. menu和command-line都能使用(general commands)。

# menu only
- menuentry
- submenu

## menuentry
```
Command: menuentry title [--class=class …] [--users=users] [--unrestricted] [--hotkey=key] { command; … }
```
這個命令用來定義GRUB menu entry的title。當在menu上這個entry被選到時，GRUB會將變數『chosen』的值設定成這個title，然後執行大括弧裡面的所有命令，如果最後一行的命令執行成功，沒有什麼意外而回傳err的話，kernel就應該被讀取，且自動執行『boot』命令。



## submenu
```
Command: submenu title [--class=class …] [--users=users] [--unrestricted] [--hotkey=key] { menu entries … }
```



# general commands

- serial
- terminal_input
- terminal_output
- terminfo
- acpi	  	
- badram	  	
- blocklist	  	
- boot	  	
- cat	  	
- chainloader	  	
- cmp	  	
- configfile	  	
- cpuid	  	
- crc	  	
- date 	
- drivemap	  	
- echo  	
- export	  	
- false	  	
- gettext	  	
- gptsync	  	
- halt	  	
- help  	
- initrd	  	
- initrd16	  	
- insmod	  	
- keystatus	  	
- linux	  	
- linux16	  	
- list_env	  	
- load_env	  	
- loopback	  	
- ls	  	
- normal	  	
- normal_exit	  	
- parttool	  	
- password	  	
- password_pbkdf2	  	
- play	  	
- pxe_unload	  	
- read  	
- reboot	  	
- save_env	  	
- search	  	
- sendkey	  	
- set	  	
- true	  	
- unset	  	
- uppermem	


## serial
## terminal_input
## terminal_output
## terminfo
## acpi	  	
## badram	  	
## blocklist	  	
## boot	  	
## cat	  	
## chainloader	  	
## cmp	  	
## configfile	  	
## cpuid	  	
## crc	  	
## date 	
## drivemap	  	
## echo  	
## export	  	
## false	  	
## gettext	  	
## gptsync	  	
## halt	  	
## help  	
## initrd	  	
## initrd16	  	
## insmod	  	
## keystatus	  	
## linux	  	
## linux16	  	
## list_env	  	
## load_env	  	
## loopback	  	
## ls	  	
## normal	  	
## normal_exit	  	
## parttool	  	
## password	  	
## password_pbkdf2	  	
## play	  	
## pxe_unload	  	
## read  	
## reboot	  	
## save_env	  	
## search	  	
## sendkey	  	
## set	  	
## true	  	
## unset	  	
## uppermem
    	