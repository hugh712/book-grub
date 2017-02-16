代表進入救援模式，出現這個代表GRUB2無法找到資料夾『grub』，或者是無法讀取『normal』modules，在這個模式底下，可以使用的modules和命令有限制，所以如果要用的話，就必須要設定好相對的『prefix』和『root』環境變數，然後在透過『insmod』來導入相關的modules。可藉由指令『normal』來回到標準的『console mode』。處理的流程如下：

(一樣，在強調一下。在底下的所有例子中，『X』就是硬碟代號，『Y』則是partition number，記得要根據你自己的狀況帶入相關的值)。

1.設定『root』
這個變數必須指到Ubuntu安裝的硬碟和partition上。
```
set root=(hdX,Y)
```
2.設定『prefix』
```
set prefix=(hdX,Y)/boot/grub
```
3.導入『normal』 module
呆回需要這個指令，所以要先導入相關模組。
```
Insmod normal
```
如果找不到相關模組的話，可以是看看底下這個路徑，因為有些平台的狀況不太一樣，你可以試看看底下這個路徑：
```
insmod (hdX,Y)/usr/lib/grub/i386-pc/normal.mod
```
4.切換模式 – 『normal mode』
```
normal
```
5.導入『linux』module
需要導入『linux』module，待回才能載入Linux Kernel。
```
Insmod linux
```
6.設定『kernel』
可以使用『root』底下的kernel捷徑，如果沒有捷徑的話請使用全路徑，通常是在『/boot』底下
```
linux /vmlinuz root=/dev/sdXY ro
```
7.設定『initrd』
選擇最新的initrd image，跟kernel一樣，可能會在『root』底下會有捷徑，沒有的話也應該要在『/boot底下找到』。
```
initrd /initrd.img
```
8.以剛才的設定啟動
```
boot
```

成功啟動後，記得去修改相對應的檔案，然後執行『update-grub』更新組態。
如果有需要的話也可以執行『grub-install』或是『boot-repair』來重新安裝GRUB。




