GRUB最主要的組態主要是『grub.cfg』，通常是在『/boot/grub』底下，這個檔案會一直很常在變動，通常大部份的使用者不需要自己去動到這個檔案。底下先來探討一個比較簡單的設定。


# Simple configuration
『grub-mkconfig』所產生的『grub.cfg』適用在很多的case，當你的distro upgrade時，系統會自動的幫你抓到最新的kernel並且自動產生『menu entry』。

但是grub-mkconfig也有一些限制，像是如果你要增加額外的客製化menu entry的話，你可以藉由編輯『/etc/grub.d/40_custom』或是建立『/boot/grub/custom.cfg』，但是修改menu entry的順序或是修改它們的title也許需要修改在『/etc/grub.d/』裡面的複雜shell script，