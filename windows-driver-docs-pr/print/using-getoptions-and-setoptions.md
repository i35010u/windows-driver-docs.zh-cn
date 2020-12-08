---
title: 使用 GetOptions 和 SetOptions
description: 使用 GetOptions 和 SetOptions
keywords:
- GetOptions
- SetOptions
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d7f43f4cb5267e1260cac4954c1c9a4ad6da8922
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96835427"
---
# <a name="using-getoptions-and-setoptions"></a>使用 GetOptions 和 SetOptions





可以调用 **GetOptions** 来检索驱动程序的当前设置，其关键字在 *pmszFeaturesRequested* 输入参数指向的缓冲区中列出。

例如，在对 **GetOptions** 的调用中，假定 *pmszFeaturesRequested* 输入缓冲区包含此字符串 (采用多个 \_ SZ 格式) ：

```cpp
"PageSize\0Duplex\0Resolution\0\0"
```

**GetOptions** 方法返回后，输出 *pmszFeatureOptionBuf* 可以包含以下字符串 (以多个 \_ SZ 格式) ：

```cpp
"PageSize\0Letter\0Duplex\0DuplexTumble\0Resolution\0300dpi\0\0"
```

此示例显示， **GetOptions** 检索到 PageSize 的选项关键字 (Letter) 、双工 (DuplexTumble) 和分辨率 (300dpi) 。

可以调用 **SetOptions** ，以根据 *pmszFeatureOptionBuf* 输入缓冲区中的功能/选项关键字对更改驱动程序的当前设置。

支持的功能有两类：

[PPD 功能](ppd-features.md)

[驱动程序功能](driver-features.md)

 

 




