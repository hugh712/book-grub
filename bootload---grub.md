# Bootloader - GRUB

Ubuntu從版本『9.10(Karmic Koala)』開始就一直用GRUB2當它的預設bootloader，我在寫這篇文章的時候，用的Ubuntu版本是『16.04(Xenial Xerus)』，GRUB2的版本是『2.02~beta2-36ubuntu3.1』。

簡單來說，一個『boot loader』是當電腦開起來以後第一個跑的軟體\(當然看架構，像是PC上第一個跑得應該是BIOS，然後在將控制權交給boot loader\)，主要的工作是讀取kernel到RAM裡面以後然後將控制權交給kernel，然後kernel接力以後在啟動所有的硬體，其他的subsystems，將root filesystem掛載起來，最後在啟動init程序。如果想要大概了解一下BIOS的開機程序可以參考一下這篇文章『[即將換掉傳統 BIOS 的 UEFI，你懂了嗎？](http://www.techbang.com/posts/4356)』，裡面有介紹了傳統BIOS和UEFI BIOS的開機流程。




_Gordon Matzigkeit_，一個GRUB狂熱者，對GRUB的描述是(有興趣者請自行體會，我就不翻譯了):

『_Some people like to acknowledge both the operating system and kernel when they talk about their computers, so they might say they use “GNU/Linux” or “GNU/Hurd”. Other people seem to think that the kernel is the most important part of the system, so they like to call their GNU operating systems “Linux systems.”

I, personally, believe that this is a grave injustice, because the_boot loader_is the most important software of all. I used to refer to the above systems as either “LILO”or “GRUB” systems.

Unfortunately, nobody ever understood what I was talking about; now I just use the word “GNU” as a pseudonym for GRUB.

So, if you ever hear people talking about their alleged “GNU” systems, remember that they are actually paying homage to the best boot loader around… GRUB!_』



從以上看得出來Gordon對GRUB的狂熱，GRUB其中一個特質就是它的靈活性，因為GRUB知道許多file system和kernel的格式，所以你可以直接讀取任何一個你想要的作業系統，並不需要知道他在磁碟上的實體位置，只要由kernel在的disk上的partition和你的檔案名稱就可以了。



