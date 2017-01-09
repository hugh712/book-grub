# 關於此篇文章

『BootLoader』，繼BIOS以後，第一個執行的程式，主要的工作是讀取kernel到RAM裡面以後然後將控制權交給kernel，所以bootloader的重要性可想而知，這篇文章想要研究一下用在各個distros上的bootloader - 『GRUB2』。

雖然Ubuntu已經有中文的[Grub2網站](https://wiki.ubuntu-tw.org/index.php?title=Grub2)，但是沒有什麼比自己找資料，實做學的更多了，所以我還是想要寫一篇Grub2的文章，  
主要是參考英文的[Ubuntu Wiki](https://help.ubuntu.com/community/Grub2)的結構，採用邊實做邊翻譯的方式，並且會在參考Ubuntu 中文wiki和archLinux的中文手冊來補強缺少的知識。

