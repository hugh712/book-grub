# GRUB和GRUB2的主要差異

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

# GRUB的功能

GRUB2的主要設計兼容於『[Multiboot Specification](https://www.gnu.org/software/grub/manual/multiboot/multiboot.html#Top)』，並且根據底下的需求:

* 基本功能對使用者必須很直覺。
* 必須對kernel開發者的支援。
* 對於FreeBSD, NetBSD, OpenBSD和 Linux的向下相容，對於『Proprietary kernels』\(eg.  DOS, Windows, OS/2\)則是使用chain-loading的方式。

除了一些特殊的相容模式以外\(chain-loading和Linux piggyback格式\)，所有個kernel都會以Multiboot Spec.上的狀態啟動。除了以上的基本需求外，底下列出所有的功能:

### Recognize multiple executable formats

支援許多的a.out格式，並且也可以讀取Symbol table。

### Support non-Multiboot kernels

支援許多其他32-bit不支援Multiboot的kernel，也支援其他boot loader的Chain-loading。

### Load multiples modules

支援多種的modules。

### Load a configuration file

支援可讀的文字組態檔，也可以動態讀取其它的組態檔或是將預先設定好的組態檔給嵌到GRUB的映像檔裡。

### Provide a menu interface

支援圖形化介面，列出所有目前的boot指令。

### Have a flexible command-line interface

提供一個相當有彈性的command-line\(命令列\)介面，可以從menu那邊存取，也可以編輯任何的命令，又或者是你想要編輯一個全新的boot command set，如果沒有組態的話，GRUB2會直接進入command-line裡面。而GRUB2的command-line支援使用tab-completion，可以根據內容來列出裝置，partitions和檔案。

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

### Support automatic decompression

會自動解壓縮gzip或是Xz2壓縮檔，可以節省很多空間和傳輸時間。但是因為像是kernel module一定會是壓縮檔，所以像類似這種的檔案就要需要用特殊的module-loading命令。

### Access data on any installed device



Be independent of drive geometry translations

Detect all installed RAM

Support Logical Block Address mode

Support network booting

Support remote terminals
