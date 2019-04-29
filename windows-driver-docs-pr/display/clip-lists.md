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
ms.openlocfilehash: dcb21390ea3a0a40403f643746c8ea5bc38f2106
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63354323"
---
# <a name="clip-lists"></a>剪辑列表


## <span id="ddk_clip_lists_gg"></span><span id="DDK_CLIP_LISTS_GG"></span>


剪切的 blts 永远不会传递到 Microsoft Windows 2000 及更高版本的驱动程序。 **IsClipped**的成员[ **DD\_BLTDATA** ](https://msdn.microsoft.com/library/windows/hardware/ff550474)始终**FALSE**，并裁剪后的列表都会**NULL**。

 

 





