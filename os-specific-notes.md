這部分官方有提供三種作業系統的說明- 『DOS/Windows』，『GNU/Linux』和『GNU/Hurd』，但是這邊我只會說明『GNU/Linux』的部分，其他有興趣的就請去翻閱官方的手冊吧。

在GRUB裡想要啟動GNU/Linux算是相對的簡單，因為Linux本身就整合成Multiboot兼容的作業系統，通常一般的步驟會如下所示:

1. 將GRUB的root device設定成跟Linux一樣，可以利用底下的指令幫你完成這部份的功能。

```
search --set=root --file /vmlinuz
```

2. 使用指令『linux』來讀取kernel:


```
grub> linux /vmlinuz root=/dev/sda1
```

