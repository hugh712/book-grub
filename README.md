# 關於此篇文章

『BootLoader』，繼BIOS以後，第一個執行的程式，主要的工作是讀取kernel到RAM裡面以後將控制權交給kernel，所以bootloader的重要性可想而知，這篇文章想要研究一下用在許多distros上的bootloader - 『GRUB2』。

雖然Ubuntu已經有中文的[Grub2網站](https://wiki.ubuntu-tw.org/index.php?title=Grub2)，但是沒有什麼比自己找資料，實做學的更多了，所以我還是想要寫一篇Grub2的文章，內容主要是參考英文的『[Ubuntu Wiki](https://help.ubuntu.com/community/Grub2)』和『[GNU官方手冊](https://www.gnu.org/software/grub/manual/html_node/)』的內容，就是兩個官方/社群的文件都被我翻譯並整理過了。

<font color="red">本文還在架構中，預計2017-03月前release。</font>

Copyright \(C\)  2017 Hugh Chao.  
  Permission is granted to copy, distribute and/or modify this document under the terms of the GNU Free Documentation License, Version 1.2 or any later version published by the Free Software Foundation;  
  with no Invariant Sections, no Front-Cover Texts, and no Back-Cover Texts.  A copy of the license is included in the section entitled \`\`GNUFree Documentation License''.

# Note
* 有些專有名詞我會盡量保持英文。
* 因為這篇文章整合了兩個官方文件，我會盡量將Ubuntu相依的用藍色字體區分出來，通常有提到Ubuntu的部份都會在GRUB 版本1.99以後。
* 裡面有許多的GRUB2，和GRUB會混用，理論上就是如果是舊版的GRUB，我會特別強調，像是用版本，或是用『舊版GRUB』，或是『GRUB Legacy』。

to do

* 統一名詞
  * options
  * parameter 
  * 映像檔 - images


# Revised History
|日期|內容|
|:--|:--|
|2017-02-16|草稿完成|

