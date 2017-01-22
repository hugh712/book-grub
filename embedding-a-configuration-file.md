GRUB可以將組態檔直接給嵌到core image裡面，所以在進入『normal mode』之前這個組態會被讀取。這種case的話，通常會用在你無法直接找到真正的組態檔，或是在讀取這個檔案時遇到問題需要debug時會蠻有用的。『grub-install』會在沒有使用BIOS的磁碟functions或是當安裝磁碟與『/boot/grub』不一樣時會使用這個功能(通常不同位置時需要用到search命令來找到『/boot/grub』)。

要組態檔嵌入到core image裡面，需要在『grub-mkimage』使用選項『-c』，然後組態檔就會被複製進去core image，當你使用這個image開機時，GRUB將會先讀取『normal module』，裡面會先讀取真實的組態 - 『$prefix/grub.cfg』，所以必須要先把變數『root』設定成root的裝置名稱，像是prefix也許是"(hd0,1)/boot/grub"，那root就必須是"hd0,1"。因此，在大部分的case中，其實只要設定『prefix』和『root』就好，然後其他流程就交給GRUB的正常程序去執行就好。通常，一個官方的典型案例如下所示（當然這個case必須要先把模組『search_fs_uuid』給掛載起來）：

```
search.fs_uuid 01234567-89ab-cdef-0123-456789abcdef root
set prefix=($root)/boot/grub
```
上面這個只是個簡單的例子，因為它只設定了『root』和『prefix』，如果想要操作更複雜的case的話，像是從其他的組態檔裡面去讀取設定，或是從其他的資料夾裡面去讀取組態的話，必須要先把『configfile』和『normal』
模組包含在core image裡面，然後在某個組態檔裡面去呼叫命令『configfile』來讀取其他的檔案，底下舉個官方的例子，這個例子需要三個模組『echo』，『search_label』和『test』在core image裡面：
```
search.fs_label grub root
if [ -e /boot/grub/example/test1.cfg ]; then
    set prefix=($root)/boot/grub
    configfile /boot/grub/example/test1.cfg
else
    if [ -e /boot/grub/example/test2.cfg ]; then
        set prefix=($root)/boot/grub
        configfile /boot/grub/example/test2.cfg
    else
        echo "Could not find an example configuration file!"
    fi
fi
```






