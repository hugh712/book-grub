GRUB裡面的環境變數(environment variables)，就像是Unix-like系統一樣，都有個名字，而且是unique的存在，這些變數都可以被set，unset和loooked up。底下介紹一個大概的變數，其中分為兩個部份，第一個部份的變數都對GRUB有特殊的含意，不可以亂用，而第二個部分的變數就可以在組態檔裡面自由的使用。

# Special environment variables

• biosnum:	
  	
• chosen:	
  	
• color_highlight:	  	

• color_normal:	  	

• debug:	  	

• default:	  	

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