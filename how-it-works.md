
前一章介紹過GRUB和GRUB2的差異，GRUB2的主要功能，根據我的習慣，接下來這一章就要來描繪一下整個GRUB2的大地圖。

<font color="red">(從這一章開始就不特別指名是GRUB或是GRUB2，全部都直接以GRUB來表示GRUB2)</font>


![](Imgs/Flow/nboot.png)

看到上圖，正常的開機流程中，當BIOS/UEFI將控制權交給MBR/GPT中的GRUB後，前兩個重要的步驟就是找到『prefix』和『root』，然後就會使用命令『normal』讀取組態『/boot/grub/grub.cfg』而進入『normal mode』，如果進入normal mode成功的話，所有的命令，檔案系統的模組(file system modules)和一些加解密的模組都會已經自動加載完成才對，當然GRUB的腳本(script) parser也已經ready了。接下來如果要在載入其他的modules的話就可以直接用命令『insmod』。

另外如果進入normal mode失敗的話，就會直接進入『rescure mode(救援模式)』，原因有可能是你的『prefix』是錯的，裝置順序錯誤，甚至也有可能是你的GRUB安裝不正確...等等。


