# GRUB2 基本console檔案操作

在GRUB2上有很多的開機問題都是因為路徑有問題，還是找不到需要的檔案，當然也是有可能是因為裝置描述有問題所造成的。但是大部分的問題其實都可以在GRUB2的console mode模式底下來修復。

而在terminal底下，你必須要有基本的能力來搜尋相關的硬碟和partitions，還有存取相關的檔案，並且為了要成功開機，或者是修復已經有問題的系統，至少也要有相關的能力將變數『root』，『prefix』，『linux』和『initrd』給設定正確，只要這四個參數有一個不對的話，那你的系統就會啟動失敗。

上個章節介紹過GRUB2下對於裝置的命名規則，和檔案的存取方式，底下會在列出幾個Ubuntu官方網站的例子，以加強印象。

(在底下的所有例子中，『X』就是硬碟代號，『Y』則是partition number，記得要根據你自己的狀況帶入相關的值)。

|命令|用途|
|:--|:--|
|ls|搜尋整個PC的裝置和partitions。|
|ls /|搜尋root裝置的root資料夾，如果你有正確設定你的『root』的話。|
|ls (hdX,Y)|檢查partition的資訊，像是格式，大小，UUID等等。|
|ls (hdX,Y)/|檢查這個partition的root內容。|
|ls (hdX,Y)/boot/|列出資料夾『/boot』裡面的檔案內容，正常來講裡面應該有kernel和initrd的images。|
|ls (hdX,Y)/boot/grub/|列出資料夾『/boot/grub』裡面的內容。|

底下列出幾個重要檔案的預設路徑：

|檔案名稱|預設路徑|
|:--|:--|
|grub.cfg|(hdX,Y)/boot/grub/ 或是 /boot/grub/|
|vmlinuz|(hdX,Y)/ 或是 /|
|linux-3.2.0-14*|(hdX,Y)/boot/ 或是 /boot/|
|initrd|(hdX,Y)/ 或是 /|
|initrd.img-3.20-14|(hdX,Y)/ 或是 /boot/|

像上面說過得，有四個設定一定要正確才能開機，底下列出相關的例子：

|任務|命令||
|:--|:--|:--|
|設定prefix|set prefix=(hdX,Y)/boot/grub|設定grub的路徑。|
|設定root|set root=(hdX,Y)||
|設定kernel|linux /vmlinuz root=/dev/sda1 ro|如果在『/』有kernel image的捷徑在的話。|
|設定kernel|linux (hdX,Y)/boot/vmlinuz-3.0.2-14 root=/dev/sda1 ro|用絕對路徑設定kernel。|
|設定initrd image|initrd /initrd.img|如果在『/』有initrd image的捷徑在的話。|
|設定initrd image|initrd (hdX,Y)/boot/initrd.img-3.0.2-14|用絕對路徑設定initrd。|