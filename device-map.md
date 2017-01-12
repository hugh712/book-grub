因為早期的歷史因素，所以從BIOS轉移給GRUB時，在BIOS driver和OS device之間的map並不能保證每一次都成功，而GRUB又需要在組態檔裡面使用從BIOS drive numbers所擷取出來的device name，所以就需要用到這個device map來確保對映成功。


因為device map在GRUB2上並不是預設，所以如果要建立出相關的device map需要用到底下的指令：

sudo grub-mkdevicemap

這個指令會將device.map給安裝到/boot/grub/裡面。