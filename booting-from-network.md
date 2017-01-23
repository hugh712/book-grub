如果你的BIOS可以支援Preboot eXecution Environment (PXE)的話，GRUB可以支援PXE網路開機，底下描述一下相關步驟:

# 準備一台TFTP伺服器
```
sudo apt-get install tftp
```

# 產生PXE boot image:

```
grub-mkimage --format=i386-pc-pxe --output=grub.pxe --prefix='(pxe)/boot/grub' pxe pxecmd
```

# 複製相關檔案

將檔案『grub.pxe』，『/boot/grub/*.mod』和『 /boot/grub/*.lst』複製到PXE(TFTP)server上面，並且確保在TFTP server的路徑『/boot/grub/』底下的『*.mod』和『*.lst』可以被存取。