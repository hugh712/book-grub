# GRUB2的功能

GRUB2的主要設計是兼容於『[Multiboot Specification](https://www.gnu.org/software/grub/manual/multiboot/multiboot.html#Top)』，並且根據底下的需求來設計的:

* 基本功能對使用者必須很直覺。
* 必須有對kernel開發者的支援。
* 對於FreeBSD, NetBSD, OpenBSD和 Linux系統的向下相容，對於『Proprietary kernels』(像是DOS, Windows, OS/2等等)則是使用chain-loading的方式。

除了一些特殊的相容模式以外(chain-loading和Linux piggyback格式)，所有的kernel都會以『Multiboot Spec.』上的狀態啟動。除了以上的基本需求外，底下列出其他額外的功能:

## 能辨識許多種的執行檔格式
支援許多的『a.out』格式，並且也可以讀取Symbol table。

## 支援non-Multiboot kernels
支援許多其他32-bit不支援Multiboot的kernel，也支援其他bootloader的Chain-loading。

## 支援多種的modules

## 自動搜尋其他作業系統
每當『update-grub』被執行時，裡面會有個『os prober』都會自動的去偵測所有已安裝的作業系統，然後被放置於GRUB2的menu裡。


## 讀取組態檔
支援可讀的文字組態檔，也可以動態讀取其它的組態檔或是將預先設定好的組態檔給嵌到GRUB2的image裡。

## 支援圖形化選單介面
支援圖形化選單介面，可列出所有目前的boot指令。

## 提供一個相當有彈性的command-line介面
提供一個相當有彈性的command-line(命令列)介面，如果沒有組態的話，GRUB2會直接進入command-line裡面。而GRUB2的command-line支援使用『tab-completion』，可以根據內容來列出裝置，partitions和檔案。

## 支援多種filesystem類型
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
## 支援自動解壓縮
會自動解壓縮gzip或是Xz2壓縮檔，可以節省很多空間和傳輸時間。但是因為像是kernel module一定會是壓縮檔，所以像類似這種的檔案就要需要用特殊的讀取module命令。

## 支援讀取各種BIOS可辨認磁碟裡面的資料

## 可偵測所有已經安裝的RAM
GRUB2可以在PC兼容的PC上找到所有已經安裝的RAM，這部分是使用進階的BIOS技術來找到所有記憶體的區間，但是並不是所有的kernel都會用到這個資訊就對了。

## 支援Logical Block Address mode
在比較傳統的磁碟呼叫(traditional disk calls)(也叫做CHS mode)中，存在著一個幾何的轉換問題，就是BIOS無法存取超過磁碟的1024磁柱，所以空間的存取就被限制在508MB到8GB之間。因為各個平台之間這部分並沒有標準的介面，所以GRUB2也無法去解決這個問題。然而，也有一些比較新的平台有支援新的介面，叫做Logical Block Address (LBA) mode，只要GRUB2自動偵測到支援這個模式的話就會去採用它，在LBA模式底下，GRUB可以存取到整顆硬碟。

## 支援網路開機
雖然基礎上來說GRUB2是個以磁碟為基礎的bootloader，但是它也支援網路功能，像是它可以使用TFTP協定從網路讀取作業系統映像檔來開機。

## 支援遠端terminals操控
有些電腦沒有支援console模式，所以GRUB2提供了remote terminal的功能，這樣你就可以從遠端的host來操控GRUB2。
