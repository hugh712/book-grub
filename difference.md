# GRUB和GRUB2的主要差異

GRUB2是修改GRUB而成的，主要的差異如下:

* 組態檔名稱由『menu.lst』或是『grub.conf』改成『grub.cfg』，有新語法，新指令跟新結構，所以GRUB的語法沒辦法直接拿過來GRUB2用。

* 『grub.cfg』是由『grub-mkconfig』自動產生的，是一個各種script的輸出結合，處理kernel的更新會更方便更直覺，因為每一次kernel的更新(新增/移除)都會自動的呼叫『update-grub』。

* 主要關於menu『顯示』設定的組態，預設都在『/etc/default/grub』。

* 設定menu的組態不只『/etc/default/grub』，還有其他許多的組態在『 /etc/grub.d/ 』。

* 使用者可以建立你得客製化選單(menu)，預設的話，客製化的檔案要被放在『/etc/grub.d/named 40_custom』。

* Partition number由『1』開始而不是之前的『0』，但是第一個裝置(device/drive)預設依然是『hd0』，但是這些設定可以在『/boot/grub/device.map 』裡面被修改。

* 組態檔會更接近script語言，像是有變數，條件式和迴圈等等。

* 有部分的裝置在經過重新啟動之後仍然可以在GRUB2中取得，這部份實做是透過指令『save\_env』，『load\_env』還有『grub-editenv』。

* 具有更好的方式來找到檔案和在多磁碟的系統上找到kernel元件，並且也可以藉由system label或是UUID來找到裝置。

* GRUB2支援更多非x86的系統。

* 支援更多的檔案系統。

* 可直接由LVM和RAID上去讀取檔案。

* 可使用圖形化介面來編輯。

* GRUB2的介面可以被轉換。

* 映像檔檔案的組成跟之前不一樣，Stage 1, Stage 1.5和 Stage 2已經不存在了，在grub的prompt(cmd)上已經沒有辦法使用指令『/find boot/grub/stage1』。

* GRUB2將許多的功能都改成動態模組\(Dynamically loaded modules\)，所以主要的映像檔可以更小更有彈性。

* 救援模式的支援。

* 可以從硬碟裡面的LiveCD ISO images直接啟動。

* <span>在Ubuntu 9.10或是之後的版本，如果沒有其它的作業系統的話，預設GRUB2將會直接開機到桌面系統或是你的login shell不會顯示任何的menu。要在開機時按住右邊的『SHIFT』鍵或是『ESC』鍵才會顯示menu。</span>


# 其他差異
如同上面所描述的，Stage 1, Stage 1.5 和 Stage 2已經不存在了，因為GRUB2本來就和舊版的設計不一樣，底下列出一些舊版GRUB使用者會很常問的相關差異:

## stage1
舊版的stage 1到GRUB2以後就變成『boot.img』，它們有相同功能。

## *_stage1_5
在舊版的stage 1.5會引入足夠的檔案系統功能，這樣接下來才能在在這個階段支援更大的檔案，但是在GRUB2裡，這部分的功已經被『core.img』所取代掉，而且『core.img』會比舊版的更穩定，功能更強大；在GRUB2裡面提供了『rescue shell』，這樣就算你在無法讀取任何的module的狀況下，也可以手動的復原。『core.img』是用更加有彈性的方式來建立的，它允許GRUB2支援其他更進階的檔案系統類型，像是LVM和RAID。

舊版的可以在某些限制底下單獨執行Stage 1 或是 Stage 2，但是GRUB2的話則是一定需要『core.img』的存在。

## stage2
GRUB2已經沒有單獨的Stage 2 映像檔，相對的是在run-time時載入『/boot/grub』裡面的模組。

## stage2_eltorito
在GRUB2裡面，從CD-ROM開機的image現在都用『cdboot.img』和『core.img』來處理，確保裡面包含了『iso9660』的模組，如果想要建立救援碟的話，這部分可以直接用『grub-mkrescue』來達成。

## nbgrub
在GRUB2裡面沒有相對應nbgrub的功能。

## pxegrub
在GRUB2裡面，用網路啟動的PXE image現在都用『pxeboot.img』和『core.img』來達成。