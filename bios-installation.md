

# MBR
在傳統PC BIOS平台所使用的『partition table』格式叫做『Master Boot Record(MBR)』，這個格式主要就是四個『primary partitions』和額外的『logical partitions』所組成的。而在這種格式之下，有兩種方式可以安裝GRUB：

1. GRUB可以被嵌在MBR和第一個partition之間的區域，這部份有好多種名字，像是『MBR gap』，『embedding area』，『boot track』等等，而且通常都只有31KiB。

2. core image可以被安裝到一個file system裡面，又或者是可以被安裝到一系列的blocks裡面，這兩種方式都要能確保可以在這個partition的第一個sector裡。

上面的兩種方式都有其缺點，第一種的話，主要是放置在embedding area並無法保證這個保留區域是絕對安全的，又或者是這會牽扯到一些license的限制問題，或者是系統有時候在建制partition的時候沒有在第一個partition留有足夠的空間等等問題。第二種方式就很有可能被一些filesystem的功能所影響，像是『tail packing』還是『fsck』等等會去影響到block的功能，所以其實依賴於filesystem的作法其實也是很脆弱的。並且第二種方式也只能用在『/boot』和BIOS開機的硬碟是同一顆的狀態下才能用。

GRUB的研發團隊通常會建議將GRUB嵌在第一個partition之前，你必須確保第一個partition至少會是在磁碟一開始的31KiB(63 sectors)之後。





# GPT