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

支援其他



Load multiples modules



Load a configuration file



Provide a menu interface



Have a flexible command-line interface



Support multiple filesystem types



Support automatic decompression



Access data on any installed device





Be independent of drive geometry translations





Detect all installed RAM



Support Logical Block Address mode



Support network booting



Support remote terminals







