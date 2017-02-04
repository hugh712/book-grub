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
```
Command: serial [--unit=unit] [--port=port] [--speed=speed] [--word=word] [--parity=parity] [--stop=stop]
```


初始化一個串列設備(serial device)，這邊要特別注意的是，這個命令一定要搭配『terminal_input』和『terminal_output』的使用。

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
```
Command: terminal_input [--append|--remove] [terminal1] [terminal2] …
```


列出或選擇一個輸入terminal。如果沒有輸入參數的話，就是列出所有已啟動
和可取得的輸入terminal。如果沒有其他參數但是有一系列的terminal名稱的話，就會只讓列出的terminal名稱啟動。

--append,
後面會接一個/多個terminal的名稱，然後這個選項會將這個terminal加到啟動輸入清單裡面。清單裡面每個terminal都會提供GRUB輸入。

--remove,
後面會接一個/多個terminal的名稱，然後這個選項會從啟動清單裡面將這個terminal移除掉。


## terminal_output
```
Command: terminal_output [--append|--remove] [terminal1] [terminal2] …
```
列出或選擇一個輸出terminal。如果沒有輸入參數的話，就是列出所有已啟動
和可取得的輸出terminal。如果沒有其他參數但是有一系列的terminal名稱的話，就會只讓列出的terminal名稱啟動。

--append,
後面會接一個/多個terminal的名稱，然後這個選項會將這個terminal加到啟動輸出清單裡面。清單裡面每個terminal都會接到GRUB的輸出資訊。

--remove,
後面會接一個/多個terminal的名稱，然後這個選項會從啟動清單裡面將這個terminal移除掉。

## terminfo

```
Command: terminfo [-a|-u|-v] [term]
```
這個命令會定義你的terminal的顯示功能，主要是藉由在terminfo database裡面給定一個entry的名字來設定，如果沒有任何參數的話，就會直接顯示目前的terminal類型。

目前可取得的terminal類型是『vt100』，『vt100-color』， 『ieee1275』和 『dumb』，如果你還想要加入其他的類型的支援的話，這方面需要和官方聯繫。

參數-a(--ascii)，-u(--utf8)，-v（--visual-utf8)控制non-ASCII的文字怎麼顯示，『-a』代表ASCII-only; 『-u』代表邏輯順序(logically-ordered)的UTF-8，『-v』代表的是視覺邏輯的UTF-8。



## acpi	  
```
Command: acpi [-1|-2] [--exclude=table1,…|--load-only=table1,…] [--oemid=id] [--oemtable=table] [--oemtablerev=rev] [--oemtablecreator=creator] [--oemtablecreatorrev=rev] [--no-ebda] filename …
```
通常現在的BIOS都有實做Advanced Configuration and Power Interface (ACPI)，並且定義描述相容於ACPI的作業系統和韌體之間介面的各種table。在有些case底下，這些預設的table只會支援特定的作業系統，所以有必要的話必須要置換這些table。

正常來說，這個命令將會置換在擴充BIOS資料區域中的Root System Description Pointer (RSDP)，這樣才會指到新的table。但是如果你用參數『--no-ebda』的話，這個新的table將只會被GRUB知道，或者是GRUB的EFI模擬系統。	
				
## badram
```
Command: badram addr,mask[,addr,mask...]
```
這個命令會通知記憶體管理哪個記憶體的區域必須被過濾掉，被過濾掉的原因通常是因為這個區域已經毀損了。當GRUB將控制權交給kernel時，也會有一份memory map，這些被濾掉的記憶體當然也會包含在其中，所以你的作業系統也會知道哪些記憶體區塊是有問題的。但是並不是所有的kernel都會支援這個行為，有支援的kernel包含了Linux, GNU Mach和FreeBSD等等。

這部份的語法會跟[Memtest86+ utility](http://www.memtest.org/)一樣，就是一系列的address/mask。
	  	
## blocklist	
```
Command: blocklist file
```
印出檔案裡的block list。block list的語法請參考之前介紹過的『GRUB的命名規則』。

  	
## boot	  	
```
Command: boot
```

啟動已經載入的作業系統或是chain-loader，但是這個指令通常只會在互動式的cmd才需要，因為在menu entry的最後面會自動呼叫。

## cat	  	
```
Command: cat [--dos] file
```
顯示檔案的內容，通常是用來看你的partition table的:

```
grub> cat /etc/fstab
```
如果有用參數『--dos』的話，結尾符號是CLRF的windows格式話就不會特別顯示，但是如果你沒有加這個參數，那結尾就會有一個『&lt;d>』。

## chainloader
```
Command: chainloader [--force] file
```


	  	
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
    	