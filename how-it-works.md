
前一章介紹過GRUB和GRUB2的差異，GRUB2的主要功能，根據我的習慣，接下來這一章就要來描繪一下整個GRUB2的大地圖。

<font color="red">(從這一章開始就不特別指名是GRUB或是GRUB2，全部都直接以GRUB來表示GRUB2)</font>


![](Imgs/Flow/nboot.png)

看到上圖，正常的開機流程中，當BIOS/UEFI將控制權交給MBR/GPT中的GRUB後，前兩個重要的步驟就是找到『prefix』和『root』，然後就會使用命令『normal』而進入『normal mode』，如果進入normal mode失敗的話，就會直接進入『rescure mode(救援模式)』
