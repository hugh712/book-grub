GRUB有兩種不同的啟動方式，第一種是直接讀取作業系統，第二種是chain-load其他的boot loader，而這個boot loader會在讀取其他的作業系統。實質上來說，第一種比較方便，因為你就不需要安裝並且維護其他的boot loader，而且GRUB會自動的在這個磁碟或是partition上辨識並讀取你的作業系統。但是第二種方式也是有需要存在，因為GRUB並不完全支援現存的所有作業系統。

# 直接啟動作業系統
Multiboot是GRUB本來就有支援的格式，而且Linux, FreeBSD, NetBSD 和OpenBSD也都支援，除了上敘以外，如果你想要啟動其他的作業系統，你就需要用到chain-load。

在kernel和root filesystem都載入的狀況之下，要直接啟動作業系統的話，只要一個指令-『boot』就好了，這部份只要先知道這個就好，後面會有完整的case。而如果是要啟動DOS或是Windows的話，需要有特殊的作法，這邊就不探討，有需要的可以直接看官方手冊。

# 使用Chain-loading
