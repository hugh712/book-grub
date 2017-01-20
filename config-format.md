grub.cfg是用GRUB內建的語法寫的，但是其語法跟GNU Bash或是其它的Bourne Shell分支的語法很像，底下大概講一些格式規則:

# Words - 字

一個word是一系列的字元組成，那GRUB當然是以一個word為單位，多個word是以字符隔開的，像是空白字元，『tab』，換行字元還有底下的幾個字元:

`{ } | & $ : < >`

如果想要把上面提到的所有字元給放到word裡面的話就需要用到『Quoting』的跳脫字元(escape character)，底下會介紹。

# Reserved words - 保留字
Reserved Word對GRUB來說是有特殊的意義，所以這些Reserved Word千萬不要用:
```
! [[ ]] { }
case do done elif else esac fi for function
if in menuentry select then time until while
```
當然不是全部的字都有目的，有些是為了未來可能會使用，所以先保留下來的。

# Quoting

# Variable expansion

# Comments

# Simple commands

# Compound commands

# Built-in Commands



