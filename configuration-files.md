# 組態結構

GRUB最主要的組態主要是『grub.cfg』，通常是在『/boot/grub』底下，這個檔案會一直很常在變動，通常大部份的使用者不需要自己去動到這個檔案。

如下圖所示，組態的更新主要由『update-grub』來觸發：
1. 當GRUB套件被自動更新時。
2. Linux kernel被更新時。
3. 使用superuser權限呼叫『update-grup』時。

![](Imgs/Config/nsystem.png)

這個指令被觸發後，它會去執行在『/etc/grub.d/』裡面的script和『/etc/default/grub』裡面的設定，並且還有將『/usr/lib/grub』裡面相關的模組和image給複製過去。

<font color="red">
這邊要熟記兩條規則：<br>
1. 沒事不要直接改『grub.cfg』，因為隨時都會被蓋掉。<br>
2. 修改其他檔案後，記得執行一下『update-grub』，不然不會更新。 </font>


## menu : /boot/grub/grub.cfg
grub.cfg是用來取代GRUB 0.97的menu.lst，這個檔案包含了GRUB2的menu 資訊，但是它不像GRUB 0.97的 menu.lst一樣通常可以直接修改，就像上面有提到的，這個檔案是上面各個部份的輸出，而各個部份都負責不一樣的功能。

這個檔案你實際去看會分很多個section，每個section都會使用『###BEGIN###』開始，和使用『###END###』結束，代表的是每個『/etc/grub.d』底下的檔案。

在早期的GRUB2版本，這個檔案其實是唯讀的，即使連『root』也不例外，但是因為開發者發現有時候簡單的改變這個檔案會對使用者比較方便，所以後來就開放可以編輯，這部份使用者自己要了解的是，當你或系統執行『update-grub』時，之前的修改又會被覆寫掉就對了，所以，最好還是由上圖的流程去修改你要的檔案，然後在執行『update-grub』的話會比較正規。而且官方上面還有說如果你自己手動修改的話，有可能造成『update-grub』執行時會造成更新出問題，導致無法更新grub.cfg，所以再次強調，可以的話還是照正規途徑修改吧。



## 使用者設定: /etc/default/grub
這個組態檔包含了之前舊版的menu.lst裡面的資訊，主要就是一些額外的環境變數，像是『backgrounds』和『theme』之類的，還有要傳給kernel line的參數等等。

## Script : /etc/grub.d/
在這個資料夾裡面的檔案都是script，執行的結果都會輸出到『grub.cfg』裡，也就是說如果你想要你的script結果被輸出到『grub.cfg』的話，你的檔案或是script就必須要是可執行的。

像之前說過的『grub.cfg』裡面的內容會有很多個section，每個section都會以『###BEGIN###』開始，和使用『###END###』結束，這每個section的內容都是在這個資料夾裡面輸出的，至於執行順序的話，因為這個資料夾裡面檔案的格式前面都會有個兩碼的數字，而執行的順序會以這個數字為主，數字越低的越先執行，像是『10_linux』就會比 『20_memtest』還要快執行，如果有開頭非數字的script的話，則這個檔案就會在所有數字開頭的script執行完以後才會執行。

這個資料夾裡面主要的檔案描述如下：


### 00_header
設定一些環境變數，像是系統檔案位置，video設定，上一個儲存的entry資訊，而且這個檔案也會負責匯入『/etc/default/grub』裡面的設定。使用者通常不用去更動到這個檔案的內容。

### 05_debian_theme
設定GRUB2的背景影像，文字顏色，themes主題和highlight的顏色等等。

### 10_linux
這個script會辨識目前在使用中的作業系統，root device中的kernel版本，並且建立相關的menu entry，如果有允許recovery mode的話也會將其寫入menu entry。在GRUB 1.99之後，規則就變成只有最新的kernel才會顯示在主要的menu上，其他的版本都會顯示在『submenu』裡面，不然當每次kernel更新時，你會發現你的menu越長越多是一件很恐怖的事。並且，submenu不會存在在non-Linux的作業系統上或是其它的partitions上的kernel上。

### 20_memtest86+
搜尋『/boot/memtest86+.bin』，並且將其包含在GRUB2裡面的menu entry裡面，如果你想要在menu entry上將這個選項移除的話，可以直接將這個檔案的executable bit移除掉，然後在執行『update-grub』如下所示：
```
sudo chmod -x /etc/grub.d/20_memtest86+
sudo update-grub
```

### 30_os-prober
這個script裡面會使用『os-prober』，就是用一個作業系統的探測器來搜尋Linux和其他的作業系統，並且將其結果給輸出到menu entry上。目前支援的作業系統包含Windows，Linux，OSX和Hurd等等。如果你想要關閉這個『os-prober』的功能，並且自己在檔案『40_custom』裡面寫入自己的entry的話，當然你也是要將這個檔案的『executable bit』移除掉，這樣它就不會被執行，然後在執行『update-grub』如下所示：
```
sudo chmod -x /etc/grub.d/30_os-prober
sudo update-grub
```
<font color="red">不過建議使用『GRUB_DISABLE_OS_PROBER』就好，盡量不要去設定這個檔案的『executable bit』。</font>

預設這個『os-prober』會忽略任何擁有『dmraid signature』的磁碟，如果你有安裝『dmraid』的話，你可以使用底下指令來列出相關的清單：
```
sudo dmraid -r -c
```

如果這個script裡面有找到其他的Ubuntu/Linux作業系統的話，它將會直接使用包含在『10_linux section』裡面的title來將其輸出到『grub.cfg』上，如果找不到的話就會使用從實際上找的的資訊建構出相關的menu entry。

### 40_custom
所有客製化的資訊或是menu entry都要被加入這個檔案裡，通常在正常程序裡面，這個script的優先權是最低的。

使用這個custom menu有底下幾個優點:<br>
1.只有在使用者修改這個檔案時才會更新，意思是當你的套件還是kernel更新時不會影響到它的位置。<br>
2.menuentry的標題很好改動。<br>
3.在menu裡面就不用管順序。<br>
4.可以特別為指定的entry設定密碼保護。<br>

有優點當然就有缺點，缺點如下:<br>
1.缺少更新機制。<br>
2.有些『/etc/default/grub』裡面的使用者資訊可能會抓不到。<br>



