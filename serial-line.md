在GRUB底下也可以使用serial terminal，如果你有多台電腦或是這些電腦沒有顯示器和鍵盤的話，通過serial port來通訊就變得非常有用。目標GRUB當然需要確定的是要有相關硬體設備，主機的話則需要terminal emulator，我這邊通常是使用『screen』。

在GRUB設定serial terminal其實是非常簡單的:
```
grub> serial --unit=0 --speed=9600
grub> terminal_input serial; terminal_output serial
```
上面這個例子使用命令『serial』然後指定『com1』，然後『Bound Rate』是『9600』，如果你想要用COM2的話，則要將參數改為『--unit=1』，serial這個指令會在後面在介紹其他的參數語用法。

『terminal_input』和『terminal_output』則是選擇你要使用哪種類型的terminal。以上面的case來說，terminal就會是一個serial terminal，但是你仍然可以多傳一個參數『console』，像是底下這個case一樣:

```
terminal_input serial console
```
在上面的例子中，一定要將input跟output打在同一行，不然你將其一的控制權交出去後，你就會發現沒辦法操控了。

要使用serial terminal另外一個限制是，GRUB會假設你的terminal emulator是相容於VT100的，當然以現在來說幾乎所有的case都相容VT100，但是如果沒有相容的話就請看一下你的terminal emulator的手冊。