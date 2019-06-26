---
title: 剪辑列表
description: 剪辑列表
ms.assetid: 73383093-ab83-4955-b017-cc370009fd0e
keywords:
- WDK DirectDraw 图阵的图面
- 绘制 blt WDK DirectDraw，剪辑列表
- DirectDraw 图阵 WDK Windows 2000 显示剪辑的属性列
- 平面闪 WDK DirectDraw，剪辑列表
- blt WDK DirectDraw，剪辑列表
- 剪辑列出 WDK DirectDraw
- 剪辑 blts WDK DirectDraw
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7f10669cfae7b403840832cd5b4ed9362da32004
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67370701"
---
# <a name="clip-lists"></a>剪辑列表


## <span id="ddk_clip_lists_gg"></span><span id="DDK_CLIP_LISTS_GG"></span>


剪切的 blts 永远不会传递到 Microsoft Windows 2000 及更高版本的驱动程序。 **IsClipped**的成员[ **DD\_BLTDATA** ](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-_dd_bltdata)始终**FALSE**，并裁剪后的列表都会**NULL**。

 

 





