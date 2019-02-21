---
title: 使用 GetOptions 和 SetOptions
description: 使用 GetOptions 和 SetOptions
ms.assetid: c8b5c235-0b74-47c8-b6ba-eba810a8467b
keywords:
- GetOptions
- SetOptions
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f75feac586ffc1d281ddafac7157d09e178c262d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56520791"
---
# <a name="using-getoptions-and-setoptions"></a>使用 GetOptions 和 SetOptions





**GetOptions**可以调用以检索其关键字列出指向的缓冲区中的功能的驱动程序的当前设置*pmszFeaturesRequested*输入的参数。

例如，在调用**GetOptions**，假设该*pmszFeaturesRequested*输入的缓冲区包含此字符串 (在多\_SZ 格式):

```cpp
"PageSize\0Duplex\0Resolution\0\0"
```

之后**GetOptions**方法返回时，输出*pmszFeatureOptionBuf*可能包含以下字符串 (也在多\_SZ 格式):

```cpp
"PageSize\0Letter\0Duplex\0DuplexTumble\0Resolution\0300dpi\0\0"
```

此示例演示**GetOptions** PageSize （字母）、 双工 (DuplexTumble) 和分辨率 (300 dpi) 检索选项关键字。

**SetOptions**可以调用以进行更改的驱动程序的当前设置，根据在功能/选项关键字对*pmszFeatureOptionBuf*输入的缓冲区。

有两种类别的支持的功能：

[PPD 功能](ppd-features.md)

[驱动程序功能](driver-features.md)

 

 




