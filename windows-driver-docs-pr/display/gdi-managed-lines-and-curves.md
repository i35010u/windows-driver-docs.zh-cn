---
title: GDI 管理的线条和曲线
description: GDI 管理的线条和曲线
keywords:
- GDI WDK Windows 2000 显示，呈现引擎
- 图形驱动程序 WDK Windows 2000 显示，呈现引擎
- 绘制 WDK GDI，呈现引擎
- 渲染引擎 WDK GDI
- 线条 WDK GDI
- GDI WDK Windows 2000 显示，行
- 图形驱动程序 WDK Windows 2000 显示，行
- 绘制 WDK GDI，行
- GDI WDK Windows 2000 显示，曲线
- 图形驱动程序 WDK Windows 2000 显示，曲线
- 绘制 WDK GDI，曲线
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8940b327497f0a6e1e0c13bda6ef16fb45dc28d6
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96796283"
---
# <a name="gdi-managed-lines-and-curves"></a>GDI 管理的线条和曲线


## <span id="ddk_gdi_managed_lines_and_curves_gg"></span><span id="DDK_GDI_MANAGED_LINES_AND_CURVES_GG"></span>


GDI 提供了改进的直线和曲线定义。 行不需要在设备坐标中具有整数端点，这一点对于 Microsoft Windows 2.x 是相同的。 这使得驱动程序无需毛舍入即可转换图形对象。 GDI 中的基本曲线是 (三样条) 而不是椭圆的贝塞尔曲线。 所有 GDI 内部操作都使用贝塞尔曲线来处理，这是大多数高端设备所支持的。 对于不处理贝塞尔曲线的设备，在调用驱动程序来绘制它们之前，GDI 会将曲线分解为线段。

GDI 可以下载以路径和矩形形式填充的区域。 驱动程序可以将路径分解为 trapezoids 或范围以进行填充。

 

 





