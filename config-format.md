grub.cfg是用GRUB內建的語法寫的，但是其語法跟GNU Bash或是其它的Bourne Shell分支的語法很像，底下大概講一些格式規則:

# Words - 字組

一個word是一系列的字元組成，那GRUB當然是以一個word為單位，多個word是以字符(metacharacters)隔開的，像是空白字元，『tab』，換行字元還有底下的幾個字元:

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
前兩個部份講解過許多不能用的word或字元，『Quoting』就是用來消除這些特殊含意，這樣就可以將『metacharacters』給夾雜在你的word裡面，或是可以將『Reserved Word』拿來當個人用途(不過最好不要拉)。

以機制來說，『Quoting』分為三種:

- escape character (跳脫字元) <br>
跳脫字元就是『\』，跳脫字元的下一個字元/字組就會被消除它本身的意義，像是如果你要在你的變數裡面用『!』，你就要把它變成『\!』。

- single quotes (單引號) <br>
在兩個單引號之間的字元/字組都會消除它原本的特性，但是單個引號卻不能存在於兩個單引號之間，即使用跳脫字元也不行。像是要用驚嘆號的話就要像這樣:『'!'』，但是不能像這樣:『'''』。

- double quotes (雙引號)
將字元/文字放在兩個雙引號之間的話也會消除其特性，但是無法消除『$』和『\』的特性。跳脫字元『\』只有背後是接空白或是『$』,『"』,『\』才有意義，因為這樣會消除這四個特殊字元的特性。此外，雙引號可以使用跳脫字元的方式被包括在另一組雙引號中間(eg. "\"\"")。


# Variable expansion - 變數/判斷式
GRUB裡面的變數/判斷式/迴圈等等都跟Bourne shell差不多，這部分有需要的可以直接參考鳥哥 - 『[BASH](http://linux.vbird.org/linux_basic/0320bash.php)』和『[Shell Script](http://linux.vbird.org/linux_basic/0340bashshell-scripts.php)』。
# Comments - 註解
當一個字組的前面有個『#』時，跟Bourne shell一樣，代表接下來的內容都會變成註解，不會被執行。

# Compound commands

# Built-in Commands



