# GRUB的作業系統命令
除了之前的章節介紹了在GRUB上的命令只能用在GRUB上或是menu entry上以外，GRUB還有許多能在作業系統上呼叫的命令，這章節統一介紹。

<font color="red">(options - 『help』和『version』因為都差不多，所以我就省略了，太佔篇幅了)</font>

這邊的命令清單有:
- grub-editenv.
- grub-file
- grub-fstest
- grub-glue-efi
- grub-install.
- grub-kbdcomp
- grub-menulst2cfg
- grub-mkconfig.
- grub-mkdevicemap
- grub-mkimage
- grub-mklayout
- grub-mkrelpath
- grub-mkstandalone
- grub-mount
- grub-script-check
- grub-syslinux2cfg
- grub-mkpasswd-pbkdf2.
- grub-mkrescue.
- grub-probe.
- grub-reboot.
- grub-set-default.
- update-grub.
- update-grub2.



## grub-editenv

### 用法
```
grub-editenv [OPTION...] FILENAME COMMAND
```
在環境變數那個章節有介紹過『environment block』，這個工具主要就是編輯這個block，如果你的檔案名稱為『-』的話，那就會使用預設的『/boot/grub/grubenv』，而如果你想要刪除整個『environment block』的話，則直接用『rm /boot/grub/grubenv』。

### grub-editenv接受底下的COMMAND:

- create <br>
 建立一個空的environment block檔案。
 
- list <br>
列出目前的所有變數。

- set [NAME=VALUE ...] <br>
設定一個或多個變數。

- unset [NAME ...] <br>
刪除一個或多個變數。

### grub-editenv接受底下的options:


- -v, --verbose <br>
顯示出更多的訊息。


## grub-file



## grub-fstest


## grub-glue-efi

## grub-install

### 用法
```
grub-install [OPTION...] [OPTION] [INSTALL_DEVICE]
```
grub-install在大部分平台上就等於『grub-mkimage』加『grub-setup』，這個命令會將GRUB安裝在你的裝置上，所以你必須特別註明哪個裝置，像是:
```
grub-install install_device
```
裝置名稱『install_device』會是一個作業系統的裝置名稱或是GRUB的裝置名稱。

### grub-install接受底下的options:

- --boot-directory=dir
將GRUB映像檔安裝到資料夾『/dir/grub』下，這個命令在當你想要將GRUB安裝到個別的partition上或是一個可移除的裝置上非常有用，如果沒有特別注命這個option的話，預設會是『/boot』，所以下面兩個命令其實是相等的:
```
grub-install /dev/sda
grub-install --boot-directory=/boot/ /dev/sda
```

下面這個例子是將你個別的partition給掛載到『/mnt/boot』上後，然後在將GRUB給安裝到這個partition上:
```
grub-install --boot-directory=/mnt/boot /dev/sdb
```

- --recheck
重新檢查device map，即使『/boot/grub/device.map』已經存在了，官方建議當你加入/移除某個裝置到你的電腦時，一定要加入這個option。



## grub-kbdcomp

## grub-menulst2cfg

## grub-mkconfig

### 用法
```
grub-mkconfig [OPTION]
```
為GRUB產生一個組態檔，用法像是:
```
grub-mkconfig -o /boot/grub/grub.cfg
```

### grub-mkconfig接受底下的options:
<br>

-o file
--output=file
系統預設是將產生的組態檔輸出到standard output，所以要記得用這個option將組態給輸出到特定檔案上。

## grub-mkdevicemap

## grub-mkimage

## grub-mklayout

## grub-mkrelpath

## grub-mkstandalone

## grub-mount

## grub-script-check

## grub-set-default

## grub-syslinux2cfg


## grub-mkpasswd-pbkdf2

### 用法
```
grub-mkpasswd-pbkdf2 [OPTION...] [OPTIONS]
```
為GRUB產生加密過的密碼。


### grub-mkpasswd-pbkdf2接受底下的options:

- -c number
- --iteration-count=number
設定底下演算法的疊代次數，當然疊代越多次越安全，預設是1000次。

- -l number
- --buflen=number
產生hash的長度，預設是64。

- -s number
- --salt=number
雜訊『salt』的長度，預設是64。

## grub-mkrescue

### 用法
```
grub-mkrescue [OPTION...] [OPTION] SOURCE...
```
產生一個可開機的GRUB救援映像檔，用法如下:
```
grub-mkrescue -o grub.iso
```

這個命令裡面會使用另一個命令『mkisofs』來產生硬像檔，只要你的options並不是『grub-mkrescue』的options，則將會直接傳給『mkisofs』模式裡的『xorriso』當成參數，簡單來說就是只要在『--』之後的參數不屬於『grub-mkrescue』的話就會直接變成『mkisofs』的參數。

如果要在你的映像檔裡面加一些檔案的話，就要建立資料夾，並且指定它，用法如下，它會將檔案『my_file1』給包到硬像檔裡面:

```
mkdir -p disk/boot/grub
cp my_file1 disk/boot/grub/
grub-mkrescue -o grub.iso disk
```

### grub-mkrescue接受底下的options:

- -o file
- --output=file
這個option是必要的，會將輸出存到檔案裡。

- --modules=modules
決定哪些模組你要預先包到這個映像檔裡，多個模組的話要使用空白鍵隔開，所以如果在script裡面用的話要記得用『" "』。

- --rom-directory=dir
如果是要為QEMU還是Coreboot產生映像檔，則這個選項會將qemu.img或是 coreboot.elf給複製到這個映像檔裡。

- --xorriso=file
如果你有自己的xorriso程式的話，可以用這個option指定，不然就會用內建的程式。

- --grub-mkimage=file
如果你有自己的grub-mkimage程式的話，可以用這個option指定，不然就會用內建的程式。

## grub-probe

### 用法
```
grub-probe [OPTION...] [OPTION]... [PATH|DEVICE]
```
這個程式會萃取你指定裝置/路徑的資訊，用法如下:

```
grub-probe --target=fs /boot/grub
grub-probe --target=drive --device /dev/sda1
```

### grub-probe必須指定裝置或是路徑，並且接受底下的options:

- -d
- --device
如果有這個option的話，那就代表你想要知道的資訊是一個系統裝置檔，像是『/dev/sda1』，換而言之，如果沒有這個option的話，代表就是filesystem的路徑，像是『/boot/grub』，則grub-probe就會印出包含這個filesystem的裝置資訊。

- -m file
- --device-map=file
通常預設的device map會在『/boot/grub/device.map』裡，但是如果指定這個option的話就會用指定的檔案當成你的device map。

- -t target
- --target=target
特別指定要印出哪些更細的分類資訊，可取得的分類如下:

 - ‘fs’
GRUB filesystem module.

 - ‘fs_uuid’
Filesystem Universally Unique Identifier (UUID).

 - ‘fs_label’
Filesystem label.

 - ‘drive’
GRUB的裝置名稱.

 - ‘device’
系統的裝置名稱。

 - ‘partmap’
GRUB partition map module.

 - ‘abstraction’
GRUB的抽象模組(abstraction module) (e.g. ‘lvm’).

 - ‘cryptodisk_uuid’
加密過的裝置UUID。

 - ‘msdos_parttype’
MBR partition type code (會是兩個16進制的編碼).

 - ‘hints_string’
可以傳進命令『search』的平臺search hints字串。

 - ‘bios_hints’
PC BIOS平臺的Search hints。

 - ‘ieee1275_hints’
IEEE1275平臺的Search hints。

 - ‘baremetal_hints’
這個search hints主要是disk是直接定址而不是透過firmware。

 - ‘efi_hints’
EFI平臺的Search hints。

 - ‘arc_hints’
ARC平臺的Search hints。

 - ‘compatibility_hint’
對於這個裝置給一個預測的GRUB裝置名稱。

 - ‘disk’
整個硬碟的系統裝置名稱

- -v
- --verbose
印出更多的訊息。

## grub-reboot

### 用法
```
grub-reboot [OPTION] MENU_ENTRY
```
設定GRUB的預設啟動entry，在下次啟動才有效。

### grub-reboot接受底下的options:

- --boot-directory=DIR
使用你自己的GRUB映像檔，而不是系統預設的『/boot/grub』，所以用這個option的話，路徑應該會像『DIR/grub』才對。

這個行為其實可以不用這個命令，只要修改相關組態在用命令『update-grub』也可以。

## grub-set-default

### 用法
```
grub-set-default [OPTION] MENU_ENTRY
```
設定GRUB下一次開機預設的啟動entry，這個命令跟『grub-reboot』主要的差別是這個命令必須要將『/etc/default/grub』裡面的『GRUB_DEFAULT』設定成『GRUB_DEFAULT=saved』，只要這個設定沒改的話，接下來每次選定不同的entry開機都會被紀錄起來，而命令『grub-reboot』則不會被紀錄起來。

### grub-reboot接受底下的options:

- --boot-directory=DIR
使用你自己的GRUB映像檔，而不是系統預設的『/boot/grub』，所以用這個option的話，路徑應該會像『DIR/grub』才對。

## update-grub
## update-grub2

### 用法
```
update-grub
update-grub2
```
這兩個指令其實是一樣的，都是等於『grub-mkconfig -o  /boot/grub/grub.cfg』這個命令，就是產生GRUB2的組態檔。


