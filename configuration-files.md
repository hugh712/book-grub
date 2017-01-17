GRUB最主要的組態主要是『grub.cfg』，通常是在『/boot/grub』底下，這個檔案會一直很常在變動，通常大部份的使用者不需要自己去動到這個檔案。底下先來探討一個比較簡單的設定。


# Simple configuration
『grub-mkconfig』所產生的『grub.cfg』適用在很多的case，當你的distro upgrade時，系統會自動的幫你抓到最新的kernel並且自動產生『menu entry』。

檔案『/etc/default/grub』控制了『grub-mkconfig』的功能，這個檔案會由Shell Script所套用，所以記得必須遵守POSIX的Shell input，裡面的值都只是一堆的『KEY=value』，如果值有空白字元或是其它的特殊字元的話，則必須用引號『""』來處理，像是:

```
GRUB_TERMINAL_INPUT="console serial"
```

底下列出所有可用的『KEY』和其說明:

- GRUB_DEFAULT<br>
設定預設的menu entry，可以是一個數字，或者是menu entry的標頭，如果是數字的話，代表的是從0開始數的menu entry編號；如果你的menu entry很多的話，建議可以直接用你的menu entry的標頭就好，不然你還要在那邊數，很麻煩。
舉例來說，如果你有個menu entry如下:
```
menuentry 'Example GNU/Linux distribution' --class gnu-linux {
	...
}
```
那你的GRUB_DEFAULT就變成:

```
GRUB_DEFAULT='Example GNU/Linux distribution'
```
除了以上兩種可能以外 - 『數字』和『標頭』以外，還有第三種，就是可以把它設定成『saved』，

- GRUB_SAVEDEFAULT

- GRUB_TIMEOUT

- GRUB_HIDDEN_TIMEOUT

- GRUB_HIDDEN_TIMEOUT_QUIET

- GRUB_DEFAULT_BUTTON  
- GRUB_TIMEOUT_BUTTON  
- GRUB_HIDDEN_TIMEOUT_BUTTON  
- GRUB_BUTTON_CMOS_ADDRESS  

- GRUB_DISTRIBUTOR

- GRUB_TERMINAL_INPUT

- GRUB_TERMINAL_OUTPUT

- GRUB_TERMINAL

- GRUB_SERIAL_COMMAND

- GRUB_CMDLINE_LINUX

- GRUB_CMDLINE_LINUX_DEFAULT

- GRUB_CMDLINE_NETBSD
- GRUB_CMDLINE_NETBSD_DEFAULT

- GRUB_CMDLINE_GNUMACH

- GRUB_CMDLINE_XEN
- GRUB_CMDLINE_XEN_DEFAULT

- GRUB_CMDLINE_LINUX_XEN_REPLACE
- GRUB_CMDLINE_LINUX_XEN_REPLACE_DEFAULT

- GRUB_DISABLE_LINUX_UUID

- GRUB_DISABLE_RECOVERY

- GRUB_VIDEO_BACKEND

- GRUB_GFXMODE

- GRUB_BACKGROUND

- GRUB_THEME

- GRUB_GFXPAYLOAD_LINUX

- GRUB_DISABLE_OS_PROBER

- GRUB_INIT_TUNE

- GRUB_BADRAM

- GRUB_PRELOAD_MODULES






