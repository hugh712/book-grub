想要在UNIX-like的機器上安裝GRUB，這部分就必須要用superuser來呼叫『grub-install』，這個程式使用方式很簡單，只要一個參數，就是你想要把grub安裝到哪裡，也就是一個裝置檔\(eg. /dev/sda\)。像是底下這個case，Linux會將GRUB安裝到第一個IDE disk的MBR上面:

`# grub-install /dev/hda`



