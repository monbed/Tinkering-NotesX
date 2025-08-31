---
title: Snipaste截图调用Pot-OCR备忘
pubDate: 2025-08-31
categories: ['']
description: ''
---

#### Snipaste控制→全局快捷键中添加

### 截屏翻译

```
snip -o "%USERPROFILE%\AppData\Local\com.pot-app.desktop\pot_screenshot_cut.png";silent;exec(powershell /c curl "127.0.0.1:60828/ocr_translate?screenshot=false")
```

### 截屏OCR

```
snip -o "%USERPROFILE%\AppData\Local\com.pot-app.desktop\pot_screenshot_cut.png";silent;exec(powershell /c curl "127.0.0.1:60828/ocr_recognize?screenshot=false")
```