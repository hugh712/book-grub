# 關機或重啟時當機

如果你在修改GRUB時造成你的機器在關機或是從重啟時當住(freeze)了，你可以試著修改『/etc/default/grub』，找到『GRUB_CMDLINE_LINUX_DEFAULT』然後加入『reboot=bios』，結果應該如下:
```
GRUB_CMDLINE_LINUX_DEFAULT="quiet splash reboot=bios"
```

