# 取得GRUB

跟其他的open source一樣，你可以取得比較穩定的版本，也可以取得目前比較新的開發版本，比較穩定的版本可以經由ftp:

[ftp://ftp.gnu.org/gnu/grub/](ftp://ftp.gnu.org/gnu/grub/)

至於如果你想要研究source code或是想要嘗試一下目前的新功能，可以經由repo上的source code:

```
git clone git://git.savannah.gnu.org/grub.git
```

如果是開發者想要由ssh存取:

```
git clone <membername>@git.sv.gnu.org:/srv/git/grub.git
```

# 如何建置

因為GRUB需要套件binutils-2.9.1.0.23版本以上，所以記得先安裝相關的套件，當然也不要忘記其他的相關建置工具:

