---
title: 剪辑列表
description: 剪辑列表
ms.assetid: 73383093-ab83-4955-b017-cc370009fd0e
keywords:
- surface DirectDraw，blitting
- 绘制 blt WDK DirectDraw，剪辑列表
- DirectDraw blitting WDK Windows 2000 显示，剪辑列表
- blitting WDK DirectDraw，剪辑列表
- blt WDK DirectDraw，剪辑列表
- 剪辑列表 WDK DirectDraw
- 剪裁 blts WDK DirectDraw
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9c47a04b156532cc177fd75489172b02bb4eea30
ms.sourcegitcommit: b84d760d4b45795be12e625db1d5a4167dc2c9ee
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/17/2020
ms.locfileid: "90717522"
---
# <a name="clip-lists"></a>剪辑列表


## <span id="ddk_clip_lists_gg"></span><span id="DDK_CLIP_LISTS_GG"></span>


剪辑的 blts 绝不会传递到 Microsoft Windows 2000 和更高版本上的驱动程序。 [**DD \_ BLTDATA**](/windows/win32/api/ddrawint/ns-ddrawint-_dd_bltdata)的**IsClipped**成员始终为**FALSE**，而剪裁列表始终为**NULL**。

 

