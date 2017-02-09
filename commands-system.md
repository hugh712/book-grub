# GRUB的作業系統命令
除了之前的章節介紹了在GRUB上的命令只能用在GRUB上或是menu entry上以外，GRUB還有許多能在作業系統上呼叫的命令，這章節統一介紹，

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




## grub-mkconfig
```
grub-mkconfig [OPTION]
```



## grub-mkpasswd-pbkdf2
```
grub-mkpasswd-pbkdf2 [OPTION...] [OPTIONS]
```



## grub-mkrescue
```
grub-mkrescue [OPTION...] [OPTION] SOURCE...
```



## grub-probe
```
grub-probe [OPTION...] [OPTION]... [PATH|DEVICE]
```

## grub-reboot

## grub-set-default

## grub-fstest


