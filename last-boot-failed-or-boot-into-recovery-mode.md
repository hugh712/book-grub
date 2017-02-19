# 上次啟動失敗或是進入救援模式

雖然Ubuntu的官方文件有說明這個部份，但是我實際上看GRUB的官方文件，還有GRUB2的source code和git history卻找不到，找了一下網路資料，『[This GRUB does not start (in Ubuntu)](https://thelastmaimou.wordpress.com/2013/11/11/this-grub-does-not-start-in-ubuntu/)』也跟我有一樣的疑慮，它的猜測是Ubuntu自己修改並加進這個參數的。

<span>
如果你上次啟動失敗或是PC啟動後進入救援模式的話，你的menu應該會一直存在，直到你再次做了選擇。在這種情況之下，如果你想要改變這行為的話，你必須修改檔案『/etc/default/grub』，並且加入變數『GRUB_RECORDFAIL_TIMEOUT』，設定這個變數的方式就跟『GRUB_TIMEOUT』類似:

- **GRUB_RECORDFAIL_TIMEOUT=-1**<br>
將不會有倒數，menu會直接顯示。

- **GRUB_RECORDFAIL_TIMEOUT=0**<br>
即使啟動失敗，menu也不會顯示。

- **GRUB_RECORDFAIL_TIMEOUT>=1**<br>
menu將會根據指定的秒數來顯示。

更新完以後記得要執行一下『update-grub』，不然會沒作用阿。如果在有些狀況之下修改『GRUB_RECORDFAIL_TIMEOUT』這個變數沒作用的話，請直接修改檔案『/etc/grub.d/00_header』，將在function -『make_timeout』裡面的這個部份
```
if [ "\${recordfail}" = 1 ] ; then
  set timeout=${GRUB_RECORDFAIL_TIMEOUT:-30}
else
```
直接修改成-1如下:
```
if [ "\${recordfail}" = 1 ] ; then
  set timeout=-1
else
```
然後更新完以後記得要執行一下『update-grub』。
<span>


