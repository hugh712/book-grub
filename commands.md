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
讀取檔案來當成你的chain-loader，就像是在filesystem底下的檔案讀取程式碼一樣，可以使用『blocklist』的標記，像是用『+1』標記目前partition的第一個sector。

--force,
強制的讀取檔案，不論它是否是正確的signature，通常是在你想要讀取一個有缺陷的boot loader時就需要用到。
	  	
## cmp	  
```
Command: cmp file1 file2
```
比較兩個檔案，如果是size不一樣的話，會顯示像是：
```
Differ in size: 0x1234 [foo], 0x4321 [bar]
```
如果size一樣但是bytes不一樣的話，會顯示像是：
```
Differ at the offset 777: 0xbe [foo], 0xef [bar]
```
至於完全一樣的話，就不會顯示任何東西。
		
## configfile	  
```
Command: configfile file
```
讀取一個檔案當成組態檔，如果檔案裡面定義了menu entry的話，則馬上就會顯示出相關的menu。
		
## cpuid	  	
```
Command: cpuid [-l]
```
檢查CPU的功能，這個命令只能支援x86的系統。如果有個參數『-l』的話，當你的CPU支援long mode(64-bit)，就會回傳『true』。

## crc	
```
Command: crc file
```
顯示一個檔案的CRC32 checksum。

## date 
```
Command: date [[year-]month-day] [hour:minute[:second]]
```
如果沒有任何參數的話，就會顯示目前的日期和時間。但是如果有加其他參數的話就會變成設定新的時間，舉個例子:
```
date 01-01
```
上面這個例子會將現在的時間設定成一月一號，但是年，時間之類的就不會變。

## drivemap	
```
Command: drivemap -l|-r|[-s] from_drive to_drive
```
如果沒有其他的參數的話，會直接將『from_drive』對映(map)到『to_drive』，通常這樣子的機制會常用在chain-load到某些沒有在第一個drive作業系統上。

\-s
執行反對映，也就是說反向將『to_drive』對應到『from_drive』。

\-l
顯示出目前的對應表。

\-r,
reset所有mapping到預設值。

下面舉個例子：
```
drivemap -s (hd0) (hd1)
```
代表將『(hd0)』對應到『(hd1)』。

## echo
```
Command: echo [-n] [-e] string …
```
當然就是顯示字串拉，如果有多個字串的話，輸出就會以空白隔開，如果要顯示變數的值的話，就直接用『${var}』的方式。

\-n,
決定顯示完這次的結果以後是否要加個換行符號。

\-e,
如果你的字串中有需要用到跳脫字元『backslash escapes』的話就要加這個參數，以下列出所有相關的序列，至於沒有在底下的case就是會直接印出那個字元，沒有什麼特殊含意：

\\\
印出backslash。

\a
Beep一聲(BEL)。

\c
不要換行。

\f
印出『form feed』，跟列印有關係。

\n
換行符號。

\r
carriage return，也就是回到這一行的最前頭。

\t
horizontal tab。

\v
vertical tab。

## export	
```
Command: export envvar
```
export環境變數，通常就是給用『configfile』建出來的子組態檔環境看得到這個變數用的，就像是在linux的shell要給其他的shell看到某個變數也是要用export一樣。
    	
## false	
```
Command: false
```
沒什麼用處，主要是拿來在判斷式『if』或『while』用的。
  	
## gettext	  	
```
Command: gettext string
```
將你的輸入字串轉變成你目前的語言，目前的語言可以看變數『lang』，至於翻譯檔的路徑會存在變數『locale_dir』裡面，檔案格式為『mo』，通常預設路徑為『/boot/grub/locale』。

## gptsync
```
Command: gptsync device [partition[+/-[type]]] …
```
使用GUID Partition Table (GPT)的disk因為相容性問題，所以裡面也會有Master Boot Record (MBR) partition table，這樣BIOS和比較舊的作業系統才能讀的到這個table，但是這個MBR只能代表GPT partition entry的限制子集合，無法代表整個GTP。

所以以上所描述到的限制，需要用這個指令來將MBR給"填充"成特殊的partition entry，最多可以有3個partition。

『type』是MBR的partition type code，如果要用16進制的話前面記得加個『0x』，在partition和type之間的區隔可以有『+』和『-』，『+』的話就是讓你的partition active，『-』的話則是讓你的partition inactive，但是狀態的話只能有一個partition處於active的狀態，如果沒有特別強調哪個partition要active的話，則所有的partition都會是inactive。
	
## halt	 
```
Command: halt --no-apm
```
關閉這台電腦。

--no-apm,
不呼叫APM BIOS。

## help  	
```
Command: help [pattern …]
```
顯示所有內建的命令資訊，如果你沒有指定『pattern』，也就是沒有指定命令的話，則將會顯示所有可取得的命令和其簡短說明。

## initrd	  	
```
Command: initrd file
```
讀取一個initial ramdisk映像檔，並且未Linux在記憶體裡的setup區域設定相關的參數，這個指令只在命令『linux』執行以後才有用處。

## initrd16	
```
Command: initrd16 file
```
跟『initrd』指令一樣的效果，只是用在16-bit mode，並且搭配的是『linux16』而不是『linux』，這個命令只能用在x86的系統上。
  	
## insmod	  
```
Command: insmod module
```



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

    