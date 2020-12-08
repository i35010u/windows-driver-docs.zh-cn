---
title: 剪辑列表
description: 剪辑列表
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
ms.openlocfilehash: b3d9cc8b9d35c54d2ab96931cb2460e50ea51ce1
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96810301"
---
# <a name="clip-lists"></a>剪辑列表


## <span id="ddk_clip_lists_gg"></span><span id="DDK_CLIP_LISTS_GG"></span>


剪辑的 blts 绝不会传递到 Microsoft Windows 2000 和更高版本上的驱动程序。 [**DD \_ BLTDATA**](/windows/win32/api/ddrawint/ns-ddrawint-dd_bltdata)的 **IsClipped** 成员始终为 **FALSE**，而剪裁列表始终为 **NULL**。

 

