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
除了以上兩種可能以外 - 『數字』和『標頭』以外，還有第三種，就是可以把它設定成『saved』，這個選項主要是藉由選項『GRUB_SAVEDEFAULT』來儲存預設的menu entry，預設的數字是『0』，除了由『GRUB_SAVEDEFAULT』選項來自動儲存以外，你也可以用grub-set-default或是grub-reboot。

- GRUB_SAVEDEFAULT <br>
如果這個選項是被設定成『true』，當你在開機選擇menu entry時，GRUB會將你的選擇儲存起來，這樣下一次開機的預設就會變成這個，接下來，底下兩個說明會有點饒舌，『GRUB_SAVEDEFAULT』只有在『GRUB_SAVEDEFAULT=saved』時有用，但是這又是兩個分開的選項，因為如果伴隨著『grub-set-default』或是『grub-reboot』的話，『GRUB_DEFAULT=saved』只有在沒有『GRUB_SAVEDEFAULT』的狀況才有效。這個選項預設是不啟用，而且依賴於『environment block』，所以可能不適用於所有的case。

- GRUB_TIMEOUT <br>
如果有做相關設定的話，通常在開機倒數時，按下任何鍵就會進入選單，這個選項主要就是在控制多少秒倒數，預設的話是『5』秒，如果設定成『0』的話，代表直接用預設選項啟動不倒數，設定成『-1』的話，代表會一直等下去。

- GRUB_HIDDEN_TIMEOUT
上一個選項是『GRUB_TIMEOUT』，主要是在定義menu出現前要倒數幾秒，如果倒數完之前沒有按任何鍵的話，將會直接以預設的選項開機。這個選項則是相反，主要是設定選單會有多長的時間不被顯示，如果將這個選項直接設定成『0』的話，將不會倒數，除非你直接按某些特定的鍵才會顯示

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






