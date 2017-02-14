# GRUB2系統救援
我想大部分的人會想要來動到GRUB，通常應該都是因為無法開機了，或者是MBR/GPT的磁區損壞了，這章會把Ubuntu 社群的相關救援主題整理一下。

## via Boot-Repair Graphical Tool
Boot-Repair是一套可以修復多種GRUB2問題的GUI軟體。這個軟體可以被使用在LiveCD, 它自己的CD或是在一般的Ubuntu session上都可以用。

當你在Ubuntu上面遇到開機的問題，或是當你安裝完其它的Linux dirtros/Windows之類的造成無法開機，安裝完Ubuntu以後Windows無法開機等等，Boot-Repair是最簡單的一套工具可以協助你處理這些疑難雜症。

![](Imgs/Fix/Fix001.PNG)


這套軟體除了可以使用GUI以外，它也有一些進階的功能，像是：
1.	可以備份『table partition』。
2.	備份『boot sectors』。
3.	可以建立Boot-info，Boot-info主要是使用script來收集各種系統的資訊，這些資訊會讓你的問題在社群或是IRC上比較好被辨識。
4.	還可以修改預設的repair參數，像是設定GRUB組態，增加kernel options，刪除GRUB，改動預設的OS，回復Windows相容的 MBR，修復損壞的檔案系統，特別指定GRUB要安裝到哪裡等等的資訊。

![](Imgs/Fix/Fix002.PNG)

## 取得Boot-Repair

###方式一
取得Boot-Repair最簡單的方式為建立包含這個工具的disk，像是『[Boot-Repair-Disk](http://sourceforge.net/p/boot-repair-cd/home)』，然後透過這個disk開機就好。建議直接將這個ISO檔燒錄成『live-USB』，製作『live-USB』可以透過工具『[UnetBootin](http://unetbootin.sourceforge.net/)』，『[LiliUSB](http://www.linuxliveusb.com/)』或是『[Universal USB Installer](http://www.pendrivelinux.com/universal-usb-installer-easy-as-1-2-3/)』，如果你的電腦有預先安裝的Win8或是你的boot是EFI模式的話建議不要燒錄成DVD，否則會有問題。

###方式二
1.	從Ubuntu的live-session。
2.	如果你的Ubuntu還可以存取的話，也可以從你的Ubuntu-session。

當然第一，一定要有網路的存取，然後打開terminal，並且輸入底下指令：
```
sudo add-apt-repository ppa:yannubuntu/boot-repair
sudo apt-get update
sudo apt-get install -y boot-repair && boot-repair
```



## 使用 Boot-Repair
1.	啟動Boot-Repair，可使用『Dash』啟動或是直接CMD輸入『boot-repair』。
2.	直接按『Recommended repair』按鈕，系統就會開始幫你處理。
3.	修復完之後，如果有出現一個URL像是『paste.ubuntu.com/XXXXX』，記得先將其記起來，然後重開機，看是否已經解決問題了。
4.	如果還是不能開機，就將上面的URL給論壇或是mail-list上的人，他們也許會幫助你。










## via GRUB2 Rescue mode


## via the LiveCD terminal


## via Partition Files Copy


## via ChRoot