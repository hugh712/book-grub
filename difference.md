GRUB2是修改GRUB而成的，主要的差異如下:

* 組態檔名稱由『menu.lst』或是『grub.conf』改成『grub.cfg』，有新語法跟新的指令，所以GRUB的語法沒辦法直接拿過來GRUB2用。
* 『grub.cfg』是由『grub-mkconfig』自動產生的，所以處理kernel更新會更方便更直覺。
* Partition number由『1』開始而不是之前的『0』。
* 組態檔會更接近script語言，像是有變數，條件式和迴圈等等。
* 有部分的裝置在經過重新啟動之後仍然可以在GRUB2中取得，這部份要使用『save\_\_env』和『load\_\_env』指令還有『grub-editenv』軟體。
* 具有更好的方式來找到檔案和在多磁碟的系統上找到kernel元件，並且也可以藉由system label或是UUID來找到裝置。
* GRUB2支援更多的系統。

* 支援更多的檔案系統。

* 可直接由LVM和RAID上去讀取檔案。

* 可使用圖形化介面來編輯。

* GRUB2的介面可以被轉換。

* image files的組成跟之前不一樣，Stage 1, Stage 1.5和 Stage 2已經不存在了。

* GRUB2將許多的功能都改成動態模組\(Dynamically loaded modules\)，所以主要的映像檔可以更小更有彈性。



