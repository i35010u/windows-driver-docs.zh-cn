---
title: GDI 管理的线条和曲线
description: GDI 管理的线条和曲线
ms.assetid: 1a7625ec-6994-488c-a722-cf436a83e213
keywords:
- GDI WDK Windows 2000 显示，呈现引擎
- 图形驱动程序 WDK Windows 2000 显示，呈现引擎
- 绘制 WDK GDI，呈现引擎
- 呈现引擎 WDK GDI
- 行 WDK GDI
- GDI WDK Windows 2000 显示中行
- 图形驱动程序 WDK Windows 2000 显示行
- 绘制 WDK GDI，行
- GDI WDK Windows 2000 显示曲线
- 图形驱动程序 WDK Windows 2000 显示曲线
- 绘制 WDK GDI，曲线
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 737e734d23f1ab355bb2ad16ef0f2812215e46e5
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63325450"
---
# <a name="gdi-managed-lines-and-curves"></a>GDI 管理的线条和曲线


## <span id="ddk_gdi_managed_lines_and_curves_gg"></span><span id="DDK_GDI_MANAGED_LINES_AND_CURVES_GG"></span>


GDI 提供改进的直线和曲线的定义。 行不需要具有整数终结点设备坐标中一样是适用于 Microsoft Windows 3.x。 这样，要将图形对象转换而无需毛舍入的驱动程序。 GDI 中的基本曲线而不是一个椭圆是贝塞尔曲线 （三次方样条）。 处理所有 GDI 内部操作则仅都处理最高端设备所支持的贝塞尔曲线。 对于不处理贝塞尔曲线的设备，GDI 细分曲线为直线段之前调用以绘制它们的驱动程序。

GDI 可以下载要填写的路径，以及矩形窗体区域。 驱动程序可以将路径分解成梯形或填充的范围。

 

 





