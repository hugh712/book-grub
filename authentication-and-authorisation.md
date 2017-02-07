#GRUB的權限和授權

Bootloader的預設應該是只要使用者可以取得實體的console的話，任何人都可以存取，而且任何人都可以選擇和編輯『menu entry』，而且任何人都可以直接存取GRUB的shell prompt。

對於大部分的系統來說，像這樣只要你能實體存取GRUB的話，確實可以取得任何權限是很合理的，如果使用GRUB這個boot loader level 還要先取得授權的話，如果想要復原損壞的系統還要這樣真的是很麻煩。


