# GRUB2 基本console操作概念

在GRUB2上有很多的開機問題都是因為路徑有問題還是找不到需要的檔案，當然也是有可能是因為裝置描述有問題。但是大部分的問題其實都可以在GRUB2的terminal/console mode/command line模式底下來修復。

在terminal底下，你必須要有基本的能力來搜尋相關的硬碟，partitions，還有存取相關的檔案，並且為了要成功開機，或者是修復已經有問題的系統，至少也要有相關的能力將變數『root』，『prefix』，『linux』和『initrd』給設定正確，只要這四個參數有一個不對的話，那你的系統就會啟動失敗。
