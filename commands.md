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

--class,  
這個參數是用來將不同的menu entry給設定成相同的class群組，menu的theme有可能會根據不同的class風格而呈現不同的效果。

--users,
這個參數主要是授權給特殊的使用者才能使用這個menu entry。

--unrestricted,
授權給所有使用者來存取特殊的menu entry。

--hotkey
結合menu entry與某個熱鍵(hotkey)，有可能是單一個字母鍵，或者是別名(eg. 'backspace', 'tab' 或是 'delete')。

## submenu
```
Command: submenu title [--class=class …] [--users=users] [--unrestricted] [--hotkey=key] { menu entries … }
```
這個命令定義一個子選單(sub menu)，然後一個新的選單 - title就會被加到menu上，當這個menu被選到後，會在顯示一個新的menu，然後這個新的menu上會有其他的entry。這個命令的參數就跟『menuentry』一樣。


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
初始化一個串列設備(serial device)，

--unit,
代表哪個serial port會被使用，範圍是0~3，預設的話是0，對應port的話是COM1。

--port,
代表哪個I/O port UART會被找到。

--speed,
這是傳輸速率，預設是9600。

--word,
--stop,
word和stop是data bits和stop bits，data bits必須是5~8，stop bits必須是1或2，預設的話是data bits - 8和stop bit - 1。

--parity,
parity的值會是『no』,『odd』,『even』其一，預設的話是『no』。








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
    	