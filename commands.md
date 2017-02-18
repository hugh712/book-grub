# GRUB 可用的命令

這一章要來探討一下到底GRUB裡面有多少的命令,但是是在『開機階段』控制權還在GRUB階段時可用的命令，不是控制權給kernel以後的相關GRUB命令。

GRUB的命令分為兩個群組:  
1. 只能在menu使用。  
2. menu和command-line都能使用\(general commands\)。

# menu only

* menuentry
* submenu

## menuentry
### 用法
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
結合menu entry與某個熱鍵\(hotkey\)，有可能是單一個字母鍵，或者是別名\(eg. 'backspace', 'tab' 或是 'delete'\)。

## submenu
### 用法
```
Command: submenu title [--class=class …] [--users=users] [--unrestricted] [--hotkey=key] { menu entries … }
```

這個命令定義一個子選單\(sub menu\)，然後一個新的選單 - title就會被加到menu上，當這個menu被選到後，會在顯示一個新的menu，然後這個新的menu上會有其他的entry。這個命令的參數就跟『menuentry』一樣。

# general commands

* serial
* terminal\_input
* terminal\_output
* terminfo
* acpi          
* badram          
* blocklist          
* boot          
* cat          
* chainloader          
* cmp          
* configfile          
* cpuid          
* crc          
* date     
* drivemap          
* echo      
* export          
* false          
* gettext          
* gptsync          
* halt          
* help      
* initrd          
* initrd16          
* insmod          
* keystatus          
* linux          
* linux16          
* list\_env          
* load\_env          
* loopback          
* ls          
* normal          
* normal\_exit          
* parttool          
* password          
* password\_pbkdf2          
* play          
* pxe\_unload          
* read      
* reboot          
* save\_env          
* search          
* sendkey          
* set          
* true          
* unset        
* vbeinfo  

## serial

```
Command: serial [--unit=unit] [--port=port] [--speed=speed] [--word=word] [--parity=parity] [--stop=stop]
```

初始化一個串列設備\(serial device\)，這邊要特別注意的是，這個命令一定要搭配『terminal\_input』和『terminal\_output』的使用。

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

## terminal\_input

```
Command: terminal_input [--append|--remove] [terminal1] [terminal2] …
```

列出或選擇一個輸入terminal。如果沒有輸入參數的話，就是列出所有已啟動  
和可取得的輸入terminal。如果沒有其他參數但是有一系列的terminal名稱的話，就會只讓列出的terminal名稱啟動。

--append,  
後面會接一個/多個terminal的名稱，然後這個選項會將這個terminal加到啟動輸入清單裡面。清單裡面每個terminal都會提供GRUB輸入。

--remove,  
後面會接一個/多個terminal的名稱，然後這個選項會從啟動清單裡面將這個terminal移除掉。

## terminal\_output

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

參數-a\(--ascii\)，-u\(--utf8\)，-v（--visual-utf8\)控制non-ASCII的文字怎麼顯示，『-a』代表ASCII-only; 『-u』代表邏輯順序\(logically-ordered\)的UTF-8，『-v』代表的是視覺邏輯的UTF-8。

## acpi

```
Command: acpi [-1|-2] [--exclude=table1,…|--load-only=table1,…] [--oemid=id] [--oemtable=table] [--oemtablerev=rev] [--oemtablecreator=creator] [--oemtablecreatorrev=rev] [--no-ebda] filename …
```

通常現在的BIOS都有實做Advanced Configuration and Power Interface \(ACPI\)，並且定義描述相容於ACPI的作業系統和韌體之間介面的各種table。在有些case底下，這些預設的table只會支援特定的作業系統，所以有必要的話必須要置換這些table。

正常來說，這個命令將會置換在擴充BIOS資料區域中的Root System Description Pointer \(RSDP\)，這樣才會指到新的table。但是如果你用參數『--no-ebda』的話，這個新的table將只會被GRUB知道，或者是GRUB的EFI模擬系統。

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

如果有用參數『--dos』的話，結尾符號是CLRF的windows格式話就不會特別顯示，但是如果你沒有加這個參數，那結尾就會有一個『&lt;d&gt;』。

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

檢查CPU的功能，這個命令只能支援x86的系統。如果有個參數『-l』的話，當你的CPU支援long mode\(64-bit\)，就會回傳『true』。

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

如果沒有其他的參數的話，會直接將『from\_drive』對映\(map\)到『to\_drive』，通常這樣子的機制會常用在chain-load到某些沒有在第一個drive作業系統上。

-s  
執行反對映，也就是說反向將『to\_drive』對應到『from\_drive』。

-l  
顯示出目前的對應表。

-r,  
reset所有mapping到預設值。

下面舉個例子：

```
drivemap -s (hd0) (hd1)
```

代表將『\(hd0\)』對應到『\(hd1\)』。

## echo

```
Command: echo [-n] [-e] string …
```

當然就是顯示字串拉，如果有多個字串的話，輸出就會以空白隔開，如果要顯示變數的值的話，就直接用『${var}』的方式。

-n,  
決定顯示完這次的結果以後是否要加個換行符號。

-e,  
如果你的字串中有需要用到跳脫字元『backslash escapes』的話就要加這個參數，以下列出所有相關的序列，至於沒有在底下的case就是會直接印出那個字元，沒有什麼特殊含意：

\  
印出backslash。

\a  
Beep一聲\(BEL\)。

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

將你的輸入字串轉變成你目前的語言，目前的語言可以看變數『lang』，至於翻譯檔的路徑會存在變數『locale\_dir』裡面，檔案格式為『mo』，通常預設路徑為『/boot/grub/locale』。

## gptsync

```
Command: gptsync device [partition[+/-[type]]] …
```

使用GUID Partition Table \(GPT\)的disk因為相容性問題，所以裡面也會有Master Boot Record \(MBR\) partition table，這樣BIOS和比較舊的作業系統才能讀的到這個table，但是這個MBR只能代表GPT partition entry的限制子集合，無法代表整個GTP。

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

匯入相關的GRUB模組。

## keystatus

```
Command: keystatus [--shift] [--ctrl] [--alt]
```

根據後面的參數來判斷『shift』，『control』和『alt』是否有被按，通常這個指令都是用在script裡面。

這個指令只在某些平台上才支援，如果你不加參數直接呼叫的話，沒有回傳『true』就代表這個指令在你的平台不支援。

## linux

```
Command: linux file …    
```

讀取Linux kernel的映像檔，第一個參數後來的空間可以用來傳遞kernel command-line參數，所有的initrd命令必須要在這個指令以後才能從新載入。

在x86系統，kernel將會使用32-bit的boot protocol來啟動，意思是『vga=』的參數已經不能用了，如果你想要設定特殊的video mode的話，就必須要設定GRUB的環境變數，像是『set gfxpayload=1024x768』或是『set gfxpayload=keep』，但是其實GRUB會自動偵測『vga=』，並且將其轉換成『gfxpayload』的設定，但是命令『linux16』將會完全的避免這個限制。

## linux16

```
Command: linux16 file …
```

在16-bit模式中讀取Linux kernel的映像檔，第一個參數後來的空間可以用來傳遞kernel command-line參數，所有的initrd命令必須要在這個指令以後才能從新載入，但是這個指令只能用在x86系統。

用這個指令的話，kernel將會使用傳統16-bit的boot protocol來啟動，所以就不會有在指令『Linux』所提到的『vga=』的參數問題。

## list\_env

```
Command: list_env [-f file]
```

顯示出『environment block』檔案的變數。

-f,  
這個參數將會蓋過預設位址。

## load\_env

```
Command: load_env [-f file]
```

從『environment block』檔案裡面讀取所有環境變數。

-f,  
這個參數將會蓋過預設位址。

## loopback

```
Command: loopback [-d] device file
```

這個指令有點像是linux裡的『mount -t loop』的感覺，主要就是將『device』名稱對映到檔案系統裡的映像檔內容，舉個例子：

```
loopback loop0 /path/to/image
ls (loop0)/
```

-d,  
刪除掉之前用這個命令建立的一個裝置對應關係。

## ls

```
Command: ls [arg …]
```

列出裝置或是檔案，如果沒有加任何參數的話，就會印出GRUB所知道的所有裝置。如果參數是一個像是『\(hd0\)』這樣用括弧刮起來的裝置名稱的話，則會列出裝置根目錄的所有檔案。如果參數是絕對路徑的資料夾名稱的話，則會直接列出這個資料夾的內容。

## normal

```
Command: normal [file]
```

進入『normal mode』並且顯示GRUB menu，如果進入normal mode成功的話，所有的命令，檔案系統的模組\(file system modules\)和一些加解密的模組都會已經自動加載完成才對，當然GRUB的腳本\(script\) parser也已經ready了。接下來如果要在載入其他的modules的話就可以直接用命令『insmod』。

如果後面有加檔案名稱，這個命令就會從檔案裡面讀取組態，否則的話，就會從『$prefix/grub.cfg』裡面讀取。

這個指令也可以在『normal mode』裡面呼叫，藉此建立一個巢狀的環境，通常都會藉由『configfile』命令來達成這個目的。

## normal\_exit

```
Command: normal_exit
```

離開『normal mode』，如果你並不是在一個巢狀『normal mode』的話，則呼叫這個指令就會變成救援模式。

## parttool

```
Command: parttool partition commands
```

這個工具可以修改partition table的entry。每個子命令只有兩個類型的輸入，一種就是『boolean』格式，另一種就是『command=value』的格式，如果是『boolean』格式的話，後面必須要有一個沒有空格的加號或減號\(+/-\)代表啟動\(enable\)或不啟動\(disable\)這個partition。

目前『parttool』這個工具只適用在MBR的格式，可使用的子命令如下所示：

'boot’ \(boolean\)  
當選項啟動時，會把所選的disk上的partition設定成啟動，並且清除其他的partition上的active flag。注意這個子命令只能在primary partition上用。

‘type’ \(value\)  
更改既存partition的類型，數值必須在0-0xFF之間。

‘hidden’ \(boolean\)  
當這個選項設定成『enabled』時，將會藉由設定partition type code上的hidden bit來隱藏所選的partition，相對而言，當這個選項設定成『disabled』時，就會清除這個bit然後顯示這個partition。這個子命令只有在當起動『DOS』，『Windows』或是其他的multiple primary FAT partition存在同一顆硬碟上時有用。

## password

```
Command: password user clear-password
```

定義一組使用者名稱和其密碼。

## password\_pbkdf2

```
Command: password_pbkdf2 user hashed-password
```

定義一組使用者名稱和雜湊演算法\(hash\)的密碼，這個密碼可以使用工具『grub-mkpasswd-pbkdf2』來產生。

## play

```
Command: play file | tempo [pitch1 duration1] [pitch2 duration2] ...
```

發出一個聲響，如果參數是一個檔案名稱，則將會播放檔案裡面的記錄。檔案格式為第一個拍子\(tempo\)為一個unsigned 32-bit的little-endian數字，接下來的是一對unsigned的16-bit little-endian數字，主要是音調\(pitch\)和周期\(duration\)。

如果參數是一系列的數字的話，則播放其音調。

tempo的計算，60的話代表1秒，120代表半秒，依此類推，pitch是以Hz.為單位，如果將pitch設定成0的話就代表休止符。

## pxe\_unload

```
Command: pxe_unload
```

卸載PXE的環境，這個命令只能在PC BIOS系統上使用。

## read

```
Command: read [var]
```

等待使用者輸入，如果在後面有指定一個參數的話，代表的就是使用者輸入的資料會存到這個變數裡。

## reboot

```
Command: reboot
```

從新啟動這台電腦。

## save\_env

```
Command: save_env [-f file] var …
```

將指定的環境變數存到『environment block』檔案裡

-f,  
這個參數代表覆蓋『environment block』的預設位置。

## search

```
Command: search [--file|--label|--fs-uuid] [--set [var]] [--no-floppy] name
```

藉由file\(-f, --file\)，filesystem label\(-l, --label\)，filesystem UUID\(-u, --fs-uuid\)來搜尋裝置。

--set,  
如果有設定這個選項，則第一個找到的裝置將會設定成後面的變數，預設的變數應該為『root』。

--no-floppy,  
這個選項防止搜尋『floppy device』\(也就是軟碟\)，以防止拖累速度。

這個指令有其他種用法，像是『search.file』，『search.fs\_label』， 和 『search.fs\_uuid』分別對應『search --file』，『search --label』和 『search --fs-uuid』。

## sendkey

```
Command: sendkey [--num|--caps|--scroll|--insert|--pause|--left-shift|--right-shift|--sysrq|--numkey|--capskey|--scrollkey|--insertkey|--left-alt|--right-alt|--left-ctrl|--right-ctrl ‘on’|‘off’]… [no-led] keystroke
```

在啟動系統送一些特定的『keystrokes』到keyboard的buffer裡面，這個機制是因為有時候一個作業系統或是chainloaded boot loader需要明確的按鍵被按，舉個例子來說，有可能需要按某個key來進入安全模式或是chainload其他的boot loader需要模擬按鍵盤來選擇menu之類的。

『keystrokes』的限制，最多可到16個，因為這就是BIOS keyboard buffer的長度，『keystrokes』的名稱可以是大寫，小寫，數字，或者是底下表格的值:  


|Name | Key |
| :--- | :--- |
| escape | Escape |
| exclam | ! |
| at | @ |
| numbersign | #  |
| dollar |  $ |
| percent |  % |
| caret |  ^ |
| ampersand | &  |
| asterisk |  * |
| parenleft |  ( |
| parenright |  ) |
| minus |  -  |
| underscore | _  |
| equal |  = |
| plus | +  |
| backspace | Backspace |
| tab |  Tab |
| bracketleft | [  |
| braceleft | {  |
| bracketright | ]  |
| braceright | } |
| enter | Enter |
| control |  press and release Control |
| semicolon | ;  |
| colon | : |
| quote |  ’|
| doublequote | "  |
| backquote | ‘ |
| tilde |  ~ |
| shift | press and release left Shift |
| backslash | \\ |
| bar |  	| |
| comma | ,  |
| less |  < |
| period |  . |
| greater |  > |
| slash |  / |
| question | ? |
| rshift | press and release right Shift |
| alt | press and release Alt |
| space |  space bar |
| capslock | Caps Lock |
| F1 | F1 |
| F2 | F2|
| F3 | F3|
| F4 | F4|
| F5 | F5|
| F6 | F6|
| F7 | F7|
| F8 | F8|
| F9 | F9|
| F10 | F10|
| F11 | F11|
| F12 | F12|
| num1 | 1 (numeric keypad) |
| num2 | 2 (numeric keypad) |
| num3 | 3 (numeric keypad) |
| num4 | 4 (numeric keypad) |
| num5 | 5 (numeric keypad) |
| num6 | 6 (numeric keypad) |
| num7 | 7 (numeric keypad) |
| num8 | 8 (numeric keypad) |
| num9 | 9 (numeric keypad) |
| num0 | 0 (numeric keypad) |
| numperiod | .  (numeric keypad) |
| numend | End (numeric keypad) |
| numdown | Down  (numeric keypad) |
| numpgdown | Page Down  (numeric keypad) |
| numleft | Left  (numeric keypad) |
| numcenter | 5  with Num Lock inactive (numeric keypad) |
| numright | Right (numeric keypad) |
| numhome | Home (numeric keypad) |
| numup | Up (numeric keypad) |
| numpgup |  Page Up (numeric keypad) |
| numinsert |  Insert  (numeric keypad) |
| numdelete |  Delete  (numeric keypad) |
| numasterisk | *  (numeric keypad) |
| numminus |  -  (numeric keypad) |
| numplus |  +  (numeric keypad) |
| numslash |  /  (numeric keypad) |
| numenter | Enter (numeric keypad) |
| delete | Delete |
| insert | Insert |
| home |  Home |
| end | End |
| pgdown | Page Down|
| pgup |  Page Up |
| down |  Down |
| up |  Left |
| left | Left |
| right | Right |

除了『keystrokes』以外，這個命令也有各種影響BIOS keyboard status flag的options。這類型的options的參數為『on』或『off』，表是相對應的status flag是set還是unset。如果省略某個status flag的options將會讓這個flag在啟動時保持著初始的狀態。

options 『--num』，『--caps』，『--scroll』和『--insert』會模擬相對應的模式，而『--capskey』，『--capskey』，『--scrollkey』和『--insertkey』則是模擬持續按著相對應的鍵，

如果有設定『--no-led』，則status flag options將不會影響鍵盤的LED。
如果這個命令持續送了好幾次的話，則只有最後一次的呼叫會有影響。
因為這個命令是藉由操作BIOS的keyboard buffer來達成相關的目的，所以有可能在某些系統上會造成當機，重啟或是其它不可預知的行為。或者是在GRUB之後的作業系統或是boot loader是用自己的keyboard driver，而不是BIOS的keyboard functions，在這種案例之下則這個命令將不會有任何的效果，而且還有一個限制就是這個命令只在PC BIOS下才有效果





## set

```
Command: set [envvar=value]
```

設定一個環境變數的值，如果沒有任何參數的話，就會印出所有的環境變數和其值。

## true

```
Command: true
```

沒什麼用處，主要是拿來在判斷式『if』或『while』用的。

## unset

```
Command: unset envvar
```

unset 特定的環境變數。

## vbeinfo
