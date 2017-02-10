# 關於此篇文章

『BootLoader』，繼BIOS以後，第一個執行的程式，主要的工作是讀取kernel到RAM裡面以後將控制權交給kernel，所以bootloader的重要性可想而知，這篇文章想要研究一下用在各個distros上的bootloader - 『GRUB2』。

雖然Ubuntu已經有中文的[Grub2網站](https://wiki.ubuntu-tw.org/index.php?title=Grub2)，但是沒有什麼比自己找資料，實做學的更多了，所以我還是想要寫一篇Grub2的文章，內容主要是參考英文的『[Ubuntu Wiki](https://help.ubuntu.com/community/Grub2)』和『[GNU官方手冊](https://www.gnu.org/software/grub/manual/html_node/)』的結構，並且會在參考Ubuntu 中文wiki和archLinux的中文手冊來補強缺少的知識。



  Copyright (C)  2017 Hugh Chao.
  Permission is granted to copy, distribute and/or modify this document
  under the terms of the GNU Free Documentation License, Version 1.2
  or any later version published by the Free Software Foundation;
  with no Invariant Sections, no Front-Cover Texts, and no Back-Cover
  Texts.  A copy of the license is included in the section entitled ``GNU
  Free Documentation License''.

- 有些專有名詞我會盡量保持英文。
- 因為這篇文章整合了兩個官方文件，我會盡量將Ubuntu相依的用藍色字體區分出來。

to do 
- 統一名詞
    - options
    - parameter 
    - 映像檔 -> images

