GRUB的圖形化介面支援客製化的外觀主題，這部份主要是透過一些參數的設定如下：

# Colors
顏色的話可以透過三種方式來描述:

- HTML-style的格式，像是"#RRGGBB", "RGB", RGB都是16進位的數值(e.g. "#8899FF")。
- 用逗號隔開的三組10進位數字 (e.g. "128, 128, 255")。
- 使用SVG1.0的顏色名稱，一定要用小寫(e.g. cornflowerblue)。

# Fonts
GRUB字體的部分使用『PFF2 font format bitmap』，都是以字體的名稱來描述這些文字。在GRUB裡面字體都是用命令『loadfont』讀取，至於有什麼字體可以讀取呢，這部份就要用命令『loadfont』來看，如果字體太多了，你的螢幕沒辦法一次顯示的話，這時候要記得用『set pager=1』，這個環境變數會有類似『less』的效果。

# Progress Bar

# Circular Progress Indicator

# Labels

# Boot Menu

# Styled Boxes

# Creating Styled Box Images

