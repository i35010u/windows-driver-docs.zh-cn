---
title: 透明 Blt
description: 透明 Blt
ms.assetid: bc2f4159-cd5d-43db-8bc3-e6fbf1e594fb
keywords:
- surface DirectDraw，blitting
- 绘制 blt WDK DirectDraw，透明 blt
- DirectDraw blitting WDK Windows 2000 显示，透明 blt
- blitting WDK DirectDraw，透明 blt
- blt WDK DirectDraw，透明
- 颜色键 WDK DirectDraw
- 透明 blts WDK DirectDraw
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bb8c81c03499ff311e6bb00860822057cf0aeb59
ms.sourcegitcommit: b84d760d4b45795be12e625db1d5a4167dc2c9ee
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/17/2020
ms.locfileid: "90717584"
---
# <a name="transparent-blt"></a>透明 Blt


## <span id="ddk_transparent_blt_gg"></span><span id="DDK_TRANSPARENT_BLT_GG"></span>


在 *透明的 blt*中，颜色键通常指定将不移动的颜色。 源颜色键类似于动作图片中使用的蓝屏。 颜色将与每个像素进行比较，如果匹配，则不会复制该像素。 如果二者不匹配，则复制该像素。 DirectDraw 还支持范围为的颜色键。

在某些情况下，可能仅部分硬件支持透明 blt。 这可能仍比在软件中执行此操作的速度更快。 \_在这些情况下，应设置 DDCAPS COLORKEYHWASSIST 标志。

部分支持的透明 blt 的一个示例是需要使用位掩码而不只是使用颜色键的显示卡。 在这种情况下，将生成单色掩码，而不是使用颜色键来比较每个像素来确定是否复制它。 也就是说，所有像素都将与颜色键进行比较，整个图面转换为位掩码 (通常每个字节一位，具体取决于颜色深度) 。 使用 DirectDraw 时，此操作在图面解锁时完成。

生成 alpha 掩码后，将其与源图面进行比较。 未在 alpha 掩码上设置的所有内容都将复制到目标图面。 这可以实现与源颜色键相同的效果，但要求首先生成掩码，而不是同时进行比较和复制。 设置颜色键时必须重新生成掩码。 它还必须在发生 blt 时检查，因为此时可以指定颜色键重写。 调用应用程序的 **Blt** 函数时，请检查颜色键是否 (传递到 Blt 的唯一颜色键重写) 与在图面上设置的颜色键相同。 如果它们相同，则不是真正的替代，无需重新生成掩码。 如果它们不同，则必须重新生成掩码。  (驱动程序的 [*DdBlt*](/windows/win32/api/ddrawint/nc-ddrawint-pdd_surfcb_blt) 函数始终将颜色键视为替代。 ) 

 

