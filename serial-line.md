在GRUB底下也可以使用serial terminal，如果你有多台電腦或是這些電腦沒有顯示器和鍵盤的話，通過serial port來通訊就變得非常有用。目標GRUB當然需要確定的是要有相關硬體設備，主機的話則需要terminal emulator，我這邊通常是使用『screen』。

在GRUB設定serial terminal其實是非常簡單的:
```
grub> serial --unit=0 --speed=9600
grub> terminal_input serial; terminal_output serial
```

