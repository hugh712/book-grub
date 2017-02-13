# 上次啟動失敗或是進入救援模式

如果你上次啟動失敗或是PC啟動後進入救援模式的話，你的menu應該會一直存在，直到你再次做了選擇。在這種情況之下，如果你想要改變這行為的話，你必須修改檔案『/etc/default/grub』，並且加入變數『GRUB_RECORDFAIL_TIMEOUT』，設定這個變數的方式就跟『GRUB_TIMEOUT』類似:

- **GRUB_RECORDFAIL_TIMEOUT=-1**<br>
將不會有倒數，menu會直接顯示。

- **GRUB_RECORDFAIL_TIMEOUT=0**<br>
即使啟動失敗，menu也不會顯示。

- **GRUB_RECORDFAIL_TIMEOUT>=1**
menu將會根據指定的秒數來顯示。