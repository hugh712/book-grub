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
這個選項主要就是在控制進入menu後會倒數幾秒，預設的話是『5』秒; 如果設定成『0』的話，代表直接用預設選項不進入menu; 設定成『-1』的話，代表會停在menu處一直等下去。如果這個值為非0的話，就不該啟用『GRUB_HIDDEN_TIMEOUT』，但是如果你『GRUB_TIMEOUT』設定為非0值，但是你的『GRUB_HIDDEN_TIMEOUT』也有設定的話，則只會看到menu出現之前的倒數，不會看到menu的倒數。

![](Imgs/Config/config002.PNG)

- GRUB_HIDDEN_TIMEOUT <br>
上一個選項是『GRUB_TIMEOUT』，主要是在定義menu出現"後"要倒數幾秒，如果倒數完之前沒有按任何鍵的話，將會直接以預設的選項開機。這個選項則是相反，主要是設定menu出現"前"會倒數幾秒，如果將這個選項直接設定成『0』的話，將不會倒數，除非你直接按某些特定的鍵才會顯示，在Ubuntu裡面則是用『Shift』。

![](Imgs/Config/config001.PNG)

- GRUB_HIDDEN_TIMEOUT_QUIET <br>
通常會跟『GRUB_HIDDEN_TIMEOUT』一起共用，
	- 如果將這個設定成『true』的話，將不會顯示倒數計時器。
	- 設定成『false』的話則會顯示，但是我在Ubuntu上面怎麼設定都是false就對了。

- GRUB_DEFAULT_BUTTON <br>  
- GRUB_TIMEOUT_BUTTON  <br>
- GRUB_HIDDEN_TIMEOUT_BUTTON <br>  
- GRUB_BUTTON_CMOS_ADDRESS  <br>
有些筆電(laptop)的供應商會在啟動特定的作業系統時，提供額外的開機按鈕，像是『Asus EeePC 1005PE』，『Dell XPS M1530』等等，而GRUB也支援這部份的需求，這部分的需求請直接看手冊，主要是藉由在這個地方寫入CMOS裡的位址。

- GRUB_DISTRIBUTOR <br>
主要由你的GRUB的distro來設定這個選項，把它設定成他們的辨識名稱，這樣通成會在menu entry 標題的部份產生更多的資訊。

- GRUB_TERMINAL_INPUT
選擇終端機(terminal)的輸入裝置，當然你可以在這邊選擇多重的裝置，中間請用空白隔開。有效的terminal輸入名稱其實取決於你的平台，但是通常會有以下的幾個(預設都是使用系統原生的terminal輸入):
	- console (PC BIOS 和 EFI consoles)
	- serial (serial terminal)
	- ofconsole (Open Firmware console)
	- at_keyboard (PC AT keyboard, 主要會用在Coreboot)
	- usb_keyboard (主要是使用HID boot protocol的USB鍵盤，這部分是以防firmware沒有去處理這部分)。

- GRUB_TERMINAL_OUTPUT
選擇終端機(terminal)的輸出裝置，當然你可以在這邊選擇多重的裝置，中間請用空白隔開。有效的terminal輸出名稱其實取決於你的平台，但是通常會有以下的幾個(預設都是使用系統原生的terminal輸出):
	- console (PC BIOS 和 EFI consoles)
	- serial (serial terminal)
	- gfxterm (graphics-mode output)
	- ofconsole (Open Firmware console)
	- vga_text (VGA text output, 主要是用在Coreboot).

底下舉個例子，將OUTPUT改成console的話，圖型化介面就會變成底下這樣:
![](Imgs/Config/config003.PNG)

- GRUB_TERMINAL <br>
	- 如果有設定這個選項，則會將『GRUB_TERMINAL_INPUT』和『GRUB_TERMINAL_OUTPUT』覆寫成相同的值。像是:
	`GRUB_TERMINAL=console` <br>
	統一將input和output都設定成console

- GRUB_SERIAL_COMMAND
如果你的GRUB想要使用serial console的話就要設定這個serial port，語法的話後面的章節會介紹。

- GRUB_CMDLINE_LINUX
要加入到menu entry的Command-line的參數，不論是一般或者是救援模式，主要是傳給kernel的。

- GRUB_CMDLINE_LINUX_DEFAULT
就像是『GRUB_CMDLINE_LINUX』和『GRUB_CMDLINE_LINUX_DEFAULT』，但是是給NetBSD用的。
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






