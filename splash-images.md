# Splash Images的troubleshooting

如果你有設定影像，但是在你的GRUB2 menu上卻沒有顯示相關影像，請照著底下的步驟檢察:

1. 如果在更新『update-grub』時沒有顯示『Found background image』，則請確定一下檔名或是路徑有沒有錯誤。
2. 檔案是否是適當的size和格式(8-bit JPG/JPEG, PNG, or TGA)。
3. 檔案應該是一個RGB, non-indexed的影像。
4. 在『/dev/default/grub』底下沒有啟動console mode。
5. 請確定你有執行『update-grub』。
6. 如果你也不知道問題在哪裡，那至少可以將你的影像檔置換成由『grub2-splashimages』套件所提供的影像試看看。