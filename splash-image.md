這章主要來講解一下在GRUB2裡面的『splash image』機制，也就是為GRUB2加一個背景圖片(非使用GRUB2 theme)。
# Splash Images

sudo apt-get install grub2-splashimages

/usr/share/images/grub


## 影像限制
GRUB2背景影像可以使用PNG，JPG/JPEG和TGA格式的影像，除了影像格式以外，還需要有底下的幾個限制:
1. JPG/JPEG必須是8-bit(256色)，否則你會得到如下的訊息『Too many Huffman tables』，如果你不想要被限制只能用256色的話，你就得要用PNG格式的影像。
2. 
3. 


