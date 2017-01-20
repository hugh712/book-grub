GRUB的multi-boot環境取決於os-prober，也就是在『grub-install』執行以後，GRUB會探測你目前有多少種的kernel和其他作業系統然後幫你輸出到『grub.cfg』裡。

這個章節來介紹一下，怎麼製作一個自製的簡單『multi-boot grub.cfg』:

1. 第一步當然是建立一個獨立的GRUB partition，

