GRUB裡面的環境變數(environment variables)，就像是Unix-like系統一樣，都有個名字，而且是unique的存在，這些變數都可以被set，unset和loooked up。底下介紹一個大概的變數，其中分為兩個部份，第一個部份的變數都對GRUB有特殊的含意，不可以亂用，而第二個部分的變數就可以在組態檔裡面自由的使用。

# Special environment variables

• **biosnum**: <br>	
  	當chain-loading到其他的boot loader時，GRUB可能需要知道與root device相關的BIOS drive number，這樣它才可以去設定registers。這部分的話也可以透過命令『devicemap』來達成。

• **chosen**: <br>	
  	這個變數需要搭配『GRUB_SAVEDEFAULT』和『GRUB_DEFAULT』的使用，因為設定成會儲存上一次的選擇，才會用到這個變數。底下兩張圖可以看到我將『GRUB_SAVEDEFAULT』設定為true和『GRUB_DEFAULT』設定為saved，然後第一次開機自己選擇用kernel 4.4.0-31開機後，在下一次開機時，『chosen』和『default』就會把我上一次所選擇的版本給儲存起來了。
  
  ![](Imgs/env/env002.PNG)

  ![](Imgs/env/env001.PNG)
  
• **color_highlight**:	  	
這個變數主要就是如果你現在terminal螢幕上有highlight的地方的話，它的文字顏色/背景顏色各是什麼。預設的話是『black/white』。其他可挑選的顏色請參考『color_normal』。

• **color_normal**:	
主要在terminal螢幕上的文字/背景顏色，預設為『white/black』，有沒有發現剛好跟『highlight』的預設是相反的。可用的顏色列出如下：
  - black
  - blue
  - green
  - cyan
  - red
  - magenta
  - brown
  - light-gray
  - dark-gray
  - light-blue
  - light-green
  - light-cyan
  - light-red
  - light-magenta
  - yellow
  - white	  	

• default:	  	
  這個變數如果有被設定的話，代表有預設的menu entry，通常是在某個timeout以後就會進入這個menu entry裡面，這個menu entry有可能是一個數字或是一串文字。這個變數通常都會經過『GRUB_DEFAULT』，『grub-set-default』或是『grub-reboot』來設定。
  
• fallback:	  	

• gfxmode:	  	

• gfxpayload:	  	

• gfxterm_font:	  	

• icondir:	  	

• lang:	  	

• locale_dir:	  	

• menu_color_highlight:	  	

• menu_color_normal:	  	

• net_pxe_boot_file:	  	

• net_pxe_dhcp_server_name:	  	

• net_pxe_domain:	  	

• net_pxe_extensionspath:	  	

• net_pxe_hostname:	  	

• net_pxe_ip:	  	

• net_pxe_mac:	  	

• net_pxe_rootpath:	  	

• pager:	  	

• prefix:	  	

• pxe_blksize:	  	

• pxe_default_gateway:	  	

• pxe_default_server:	  	

• root:	  	

• superusers:	  	

• theme:	  	

• timeout:	  	



# The GRUB environment block