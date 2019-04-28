---
title: 贝塞尔曲线
description: 贝塞尔曲线
ms.assetid: 322ff79b-e5b8-4247-99eb-1aa3779216ef
keywords:
- GDI WDK Windows 2000 显示，曲线贝塞尔
- 图形驱动程序 WDK Windows 2000 显示，曲线贝塞尔
- 绘制 WDK GDI，贝塞尔曲线
- 三次方自由绘制曲线 WDK GDI
- 贝塞尔曲线 WDK GDI
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 156092e5ea14faa556a31f5bad0e70a1ded45f5a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63346968"
---
# <a name="bezier-curves"></a>贝塞尔曲线


## <span id="ddk_bezier_curves_gg"></span><span id="DDK_BEZIER_CURVES_GG"></span>


一些高级的硬件设备可以绘制包含贝塞尔曲线 （三次方自由绘制曲线），这是常规用途的曲线基元的路径。 如果因此，该驱动程序可以包括支持在这些曲线[ **DrvStrokePath** ](https://msdn.microsoft.com/library/windows/hardware/ff556316)函数。

当 GDI 必须在设备管理的图面上绘制贝塞尔曲线路径时，它将测试 GCAPS\_贝赛尔曲线标志 (在[ **DEVINFO** ](https://msdn.microsoft.com/library/windows/hardware/ff552835)结构) 来确定是否应调用[ **DrvStrokePath**](https://msdn.microsoft.com/library/windows/hardware/ff556316)。 如果调用，此函数执行请求的操作，或决定不处理它，就像几何宽线条的操作一样。 在后一种情况下，GDI 细分请求为更简单的操作，例如，通过将曲线转换为行大概确定的。

 

 





