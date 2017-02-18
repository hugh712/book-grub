這部分官方有提供三種作業系統的說明- 『DOS/Windows』，『GNU/Linux』和『GNU/Hurd』，但是這邊我只會說明『GNU/Linux』的部分，其他有興趣的就請去翻閱官方的手冊吧。

在GRUB裡想要啟動GNU/Linux算是相對的簡單，因為Linux本身就整合成Multiboot兼容的作業系統，這邊你只要記得，想要手動啟動GNU/Linux，至少需要有底下四種資訊:
- prefix
- root
- kernel
- initrd

通常一般的步驟會如下所示:

1. 將GRUB的root device設定成跟Linux一樣，可以利用底下的指令幫你完成這部份的功能。
```
search --set=root --file /vmlinuz
```
2. 使用指令『linux』來讀取kernel:
```
grub> linux /vmlinuz root=/dev/sda1
```
至於如果你想要加一些kernel的參數的話，可以直接加到後面，像是底下的例子，主要是將acpi給設定成off:
```
grub> linux /vmlinuz root=/dev/sda1 acpi=off
```
其他的kernel參數，因為我一直找不到官方的文件，好像已經刪掉了，但是有一個我很常看的機構『free-electrons』上面有，有興趣的可以參考一下 - 『[kernel-parameters](http://lxr.free-electrons.com/source/Documentation/kernel-parameters.txt)』。
而有些BIOS像是APM或是EDD並沒有提供32-bit的協定，所以在這些比較特殊的BIOS上你就要使用『linux16』:
```
grub> linux16 /vmlinuz root=/dev/sda1 acpi=off
```
3. 如果你有initrd的話，直接在指令『linux』後面使用:
```
grub> initrd /initrd
```
跟指令『linux』一樣，如果不支援32位元的話，請用:
```
grub> initrd16 /initrd
```
4. 最後一步，使用『boot』啟動。








