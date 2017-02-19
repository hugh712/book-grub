# 關機或重啟時當機

如果因為修改GRUB，造成你的機器在關機或是從重啟時當住(freeze)了，你可以試著修改『/etc/default/grub』，找到『GRUB_CMDLINE_LINUX_DEFAULT』然後加入『reboot=bios』，結果應該如下:
```
GRUB_CMDLINE_LINUX_DEFAULT="quiet splash reboot=bios"
```
然後執行『update-grub』以後重開機試看看。

在特定的硬體上，像是DELL之類的，就要變成『reboot=pci』如下:
```
GRUB_CMDLINE_LINUX_DEFAULT="quiet splash reboot=cpi"
```




