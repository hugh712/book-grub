# GRUB和GRUB2的主要差異

GRUB2是修改GRUB而成的，主要的差異如下:

* 組態檔名稱由『menu.lst』或是『grub.conf』改成『grub.cfg』，有新語法跟新的指令，所以GRUB的語法沒辦法直接拿過來GRUB2用。
* 『grub.cfg』是由『grub-mkconfig』自動產生的，所以處理kernel的更新會更方便更直覺。
* Partition number由『1』開始而不是之前的『0』。
* 組態檔會更接近script語言，像是有變數，條件式和迴圈等等。
* 有部分的裝置在經過重新啟動之後仍然可以在GRUB2中取得，這部份實做是透過指令『save\_env』和『load\_env』還有『grub-editenv』。
* 具有更好的方式來找到檔案和在多磁碟的系統上找到kernel元件，並且也可以藉由system label或是UUID來找到裝置。
* GRUB2支援更多的系統。

* 支援更多的檔案系統。

* 可直接由LVM和RAID上去讀取檔案。

* 可使用圖形化介面來編輯。

* GRUB2的介面可以被轉換。

* image files的組成跟之前不一樣，Stage 1, Stage 1.5和 Stage 2已經不存在了。

* GRUB2將許多的功能都改成動態模組\(Dynamically loaded modules\)，所以主要的映像檔可以更小更有彈性。

<hr>

# GRUB的功能

GRUB2的主要設計兼容於『[Multiboot Specification](https://www.gnu.org/software/grub/manual/multiboot/multiboot.html#Top)』，並且根據底下的需求:

* 基本功能對使用者必須很直覺。
* 必須對kernel開發者的支援。
* 對於FreeBSD, NetBSD, OpenBSD和 Linux的向下相容，對於『Proprietary kernels』\(eg.  DOS, Windows, OS/2\)則是使用chain-loading的方式。

除了一些特殊的相容模式以外\(chain-loading和Linux piggyback格式\)，所有個kernel都會以Multiboot Spec.上的狀態啟動。除了以上的基本需求外，底下列出所有的功能:

<hr>

### Recognize multiple executable formats

支援許多的a.out格式，並且也可以讀取Symbol table。

### Support non-Multiboot kernels

支援許多其他32-bit不支援Multiboot的kernel，也支援其他boot loader的Chain-loading。

<hr>

### Load multiples modules

支援多種的modules。

<hr>

### Load a configuration file

支援可讀的文字組態檔，也可以動態讀取其它的組態檔或是將預先設定好的組態檔給嵌到GRUB的映像檔裡。

<hr>

### Provide a menu interface

支援圖形化介面，列出所有目前的boot指令。

<hr>

### Have a flexible command-line interface

提供一個相當有彈性的command-line\(命令列\)介面，可以從menu那邊存取，也可以編輯任何的命令，又或者是你想要編輯一個全新的boot command set，如果沒有組態的話，GRUB2會直接進入command-line裡面。而GRUB2的command-line支援使用tab-completion，可以根據內容來列出裝置，partitions和檔案。

<hr>

### Support multiple filesystem types

支援很多種的檔案系統，而且可以直接用blocklist來指定檔案，目前支援的有:

* _Amiga Fast FileSystem \(AFFS\)_

* _AtheOS fs_

* _BeFS_

* _BtrFS _

  ```
  包含: raid0, raid1, raid10, gzip 和 lzo。
  ```

* _cpio_

  ```
  包含: little- 和 big-endian bin, odc 和 newc variants。
  ```

* _Linux ext2/ext3/ext4_

* _DOS FAT12/FAT16/FAT32_

* _exFAT_

* _HFS_

* _HFS+_

* _ISO9660_

  ```
  包含 Joliet, Rock-ridge 和 multi-chunk files。
  ```

* _JFS_

* _Minix fs_

  ```
  包含 versions 1, 2 和 3。
  ```

* _nilfs2_

* _NTFS_

  ```
  包含壓縮。
  ```

* _ReiserFS_

* _ROMFS_

* _Amiga Smart FileSystem \(SFS\)_

* _Squash4_

* _tar_

* _UDF_

* _BSD UFS/UFS2_

* _XFS_

* _ZFS_

  ```
  包含lzjb, gzip, zle, mirror, stripe, raidz1/2/3 和 AES-CCM/AES-GCM加密。
  ```
<hr>

### Support automatic decompression

會自動解壓縮gzip或是Xz2壓縮檔，可以節省很多空間和傳輸時間。但是因為像是kernel module一定會是壓縮檔，所以像類似這種的檔案就要需要用特殊的module-loading命令。

<hr>

### Access data on any installed device

支援讀取各種BIOS可辨認的磁碟。

<hr>

### Detect all installed RAM

Grub2可以在PC兼容的PC上找到所有已經安裝的RAM，這部分是使用進階的BIOS技術來找到所有記憶體的區間，但是並不是所有的kernel都會用到這個資訊就對了。

<hr>

### Support Logical Block Address mode

在比較傳統的磁碟呼叫\(traditional disk calls\)\(也叫做_CHS mode_\)中，存在著一個幾何的轉換問題，就是BIOS無法存取超過磁碟的1024磁柱，所以空間的存取就被限制在508MB到8GB之間。因為各個平台之間這部分並沒有標準的介面，所以GRUB也無法去解決這個問題。然而，也一些比較新的平台有著一個新的介面，叫做Logical Block Address \(_LBA_\) mode，只要GRUB自動去偵測到支援這個模式的話就會去採用它，在LBA模式底下，GRUB可以存取到整顆硬碟。

<hr>

### Support network booting

雖然基礎上來說GRUB是個以磁碟為基礎的bootloader，但是它也支援網路功能，像是可以使用TFTP協定從網路讀取作業系統映像檔。

<hr>

### Support remote terminals

有些電腦沒有支援console模式，所以GRUB提供了remote terminal的功能，這樣你就可以從遠端的host來操控GRUB。
<hr>
# 主要模式差異
因為GRUB2本來就和舊版的設計不一樣，底下列出一些舊版GRUB使用者會很常問的相關差異:

### stage1
舊版的stage 1到GRUB2以後就變成『boot.img』，它們有相同功能。

### *_stage1_5
在舊版的stage 1.5會引入足夠的檔案系統功能，這樣接下來才能在在這個階段支援更大的檔案，但是在GRUB2裡，這部分的功已經被『core.img』所取代掉，而且『core.img』會比舊版的更穩定，功能更強大；而且在GRUB2裡面提供了『rescue shell』，這樣就算你在無法讀取任何的module的狀況下，也可以手動的復原。『core.img』是用更加有彈性來建立的，它允許GRUB2支援其他更進階的檔案系統類型，像是LVM和RAID。

舊版的可以在某些限制底下單獨執行Stage 1 或是 Stage 2，但是GRUB2的話則是一定需要『core.img』的存在。

### stage2
GRUB2已經沒有單獨的Stage 2 image，相對的是在run-time時載入『/boot/grub』裡面的模組。

### stage2_eltorito
在GRUB2裡面，從CD-ROM開機的image現在都用『cdboot.img』和『core.img』來處理，確保裡面包含了『iso9660』的模組，如果想要建立救援碟的話，這部分可以直接用『grub-mkrescure』來達成。

### nbgrub
在GRUB2裡面沒有相對應nbgrub的功能。

### pxegrub
在GRUB2裡面，用網路啟動的PXE image現在都用『pxeboot.img』和『core.img』來達成。