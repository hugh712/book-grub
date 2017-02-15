# 完全重新安裝GRUB2

在『grub-install』和『purging & reinstalling』 GRUB之間的差別，主要是後者是可以完全的移除所有GRUB的檔案和系統設定，有些GRUB的錯誤主要是因為就的組態有問題，檔案損毀，或是檔案/資料夾被不小心刪掉了了等等，所以就算你在安裝在多次，那些有問題的檔案或組態依然存在，所以真的一直有問題的話，就是看看刪除後在重新安裝吧。GRUB套件的刪除和重新安裝的程序包含的『grub-pc』，『grub-common』和『grub-gfxpayload-lists』。

因為這項操作會讓你暫時沒有bootloader，所以請再三確保你在刪除GRUB套件之前你是可以存取網路，並且可以存取相關的repo。想要完全刪除GRUB並且重新安裝的話有兩種方式 - 『Boot-Repair』和『Terminal』，底下有詳細說明。

## via Boot-Repair Graphical Tool
之前的章節有介紹過『Boot-Repair』這套工具，首先當然是一樣先執行它，然後直接選擇『Advanced options』->『GRUB options』->『Purge GRUB and reinstall it』，然後按Apply就好了(我這個版本一開始就已經預設是這個選項)。
![](Imgs/trouble/trouble001.PNG)

## via Terminal Commands