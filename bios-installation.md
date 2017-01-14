

# MBR
在傳統PC BIOS平台所使用的『partition table』格式叫做『Master Boot Record(MBR)』，這個格式主要就是四個『primary partitions』和額外的『logical partitions』所組成的。而在這種格式之下，有兩種方式可以安裝GRUB：

1. GRUB可以被嵌在MBR和第一個partition之間的區域，這部份有好多種名字，像是『MBR gap』，『embedding area』，『boot track』等等，而且通常都只有31KiB。

2. core image可以被安裝到一個file system裡面，又或者是可以被安裝到一系列的blocks裡面，這兩種方式都要能確保可以在這個partition的第一個sector裡。







# GPT