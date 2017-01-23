如果你的BIOS可以支援Preboot eXecution Environment (PXE)的話，GRUB可以支援PXE網路開機，底下描述一下相關步驟:

# 準備一台TFTP伺服器

# 產生PXE boot image:

```
grub-mkimage --format=i386-pc-pxe --output=grub.pxe --prefix='(pxe)/boot/grub' pxe pxecmd
```


