---
title: 透明 Blt
description: 透明 Blt
ms.assetid: bc2f4159-cd5d-43db-8bc3-e6fbf1e594fb
keywords:
- WDK DirectDraw 图阵的图面
- 绘制 blt WDK DirectDraw、 透明 blt
- DirectDraw 图阵 WDK Windows 2000 显示，透明 blt
- 平面闪 WDK DirectDraw 透明 blt
- blt WDK DirectDraw，透明
- 颜色密钥 WDK DirectDraw
- 透明 blts WDK DirectDraw
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f1cfd50222efaecf78a8ff4fb0dac8f2b7442e1e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63389781"
---
# <a name="transparent-blt"></a>透明 Blt


## <span id="ddk_transparent_blt_gg"></span><span id="DDK_TRANSPARENT_BLT_GG"></span>


在中*透明 blt*，颜色键通常指定不会移动的颜色。 源颜色键是类似于蓝屏运动图片中使用。 颜色比较为每个像素，并且如果它们匹配，则不会复制像素。 如果不匹配，将复制像素。 DirectDraw 还支持是范围的颜色键。

在某些情况下，透明 blt 可能仅部分支持的硬件。 这可能是仍比在软件中执行速度更快。 DDCAPS\_COLORKEYHWASSIST 标志应设置在这些情况下。

部分支持的透明 blt 的一个示例是显示卡所需的位掩码，而不是只使用颜色键。 在这种情况下，而不是将每个像素的颜色键以确定是否将其复制与进行比较，生成了单色屏蔽。 也就是说，所有像素的颜色键与进行比较和整个图面转换为位掩码 （通常每个字节，具体取决于颜色深度的一位）。 在使用 DirectDraw，这可在图面处于解锁状态时。

Alpha 掩码生成后，将与源图面进行比较。 未在 alpha 掩码中设置的所有内容复制到目标图面。 这样可实现相同的效果，为源颜色键，但需要首先，而不是比较和复制在同一时间生成的掩码。 掩码必须重新生成任何时间将设置颜色键。 它还必须检查 blt 每当发生因为可以在该时间指定颜色密钥替代。 当应用程序的**Blt**函数被调用时，颜色键重写 （唯一颜色键传递给 blt） 的检查是图面设置的颜色键相同。 如果它们是相同的它并不是重写和掩码不需要重新生成。 如果它们不同，必须重建掩码。 (在驱动程序[ *DdBlt* ](https://msdn.microsoft.com/library/windows/hardware/ff549205)函数始终将其视为重写的颜色键。)

 

 





