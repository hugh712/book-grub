# GRUB的作業系統命令
除了之前的章節介紹了在GRUB上的命令只能用在GRUB上或是menu entry上以外，GRUB還有許多能在作業系統上呼叫的命令，這章節統一介紹。

<font color="red">(options - 『help』和『version』因為都差不多，所以我就省略了，太佔篇幅了)</font>

## grub-editenv
```
grub-editenv [OPTION...] FILENAME COMMAND
```




## grub-install
```
grub-install [OPTION...] [OPTION] [INSTALL_DEVICE]
```
grub-install在大部分平台上就等於『grub-mkimage』加『grub-setup』，這個命令會將GRUB安裝在你的裝置上，所以你必須特別註明哪個裝置，像是:
```
grub-install install_device
```
裝置名稱『install_device』會是一個作業系統的裝置名稱或是GRUB的裝置名稱。

grub-install接受底下的options:

--boot-directory=dir
將GRUB映像檔安裝到資料夾『/dir/grub』下，這個命令在當你想要將GRUB安裝到個別的partition上或是一個可移除的裝置上非常有用，如果沒有特別注命這個option的話，預設會是『/boot』，所以下面兩個命令其實是相等的:
```
grub-install /dev/sda
grub-install --boot-directory=/boot/ /dev/sda
```

下面這個例子是將你個別的partition給掛載到『/mnt/boot』上後，然後在將GRUB給安裝到這個partition上:
```
grub-install --boot-directory=/mnt/boot /dev/sdb
```

--recheck
重新檢查device map，即使『/boot/grub/device.map』已經存在了，官方建議當你加入/移除某個裝置到你的電腦時，一定要加入這個option。

## grub-mkconfig
```
grub-mkconfig [OPTION]
```
為GRUB產生一個組態檔，用法像是:
```
grub-mkconfig -o /boot/grub/grub.cfg
```

grub-mkconfig接受底下的options:
<br>

-o file
--output=file
系統預設是將產生的組態檔輸出到standard output，所以要記得用這個option將組態給輸出到特定檔案上。



## grub-mkpasswd-pbkdf2
```
grub-mkpasswd-pbkdf2 [OPTION...] [OPTIONS]
```
為GRUB產生加密過的密碼。


grub-mkpasswd-pbkdf2接受底下的options:

-c number
--iteration-count=number
設定底下演算法的疊代次數，當然疊代越多次越安全，預設是1000次。

-l number
--buflen=number
產生hash的長度，預設是64。

-s number
--salt=number
雜訊『salt』的長度，預設是64。

## grub-mkrescue
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

grub-mkrescue接受底下的options:

-o file
--output=file


--modules=modules


--rom-directory=dir

--xorriso=file

--grub-mkimage=file

## grub-probe
```
grub-probe [OPTION...] [OPTION]... [PATH|DEVICE]
```

## grub-reboot

## grub-set-default

## grub-fstest


