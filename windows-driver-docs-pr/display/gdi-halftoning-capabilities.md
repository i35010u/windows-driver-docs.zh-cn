---
title: GDI 半色调功能
description: GDI 半色调功能
keywords:
- GDI WDK Windows 2000 显示，呈现引擎
- 图形驱动程序 WDK Windows 2000 显示，呈现引擎
- 绘制 WDK GDI，呈现引擎
- 渲染引擎 WDK GDI
- GDI WDK Windows 2000 显示，半色调
- 图形驱动程序 WDK Windows 2000 显示，半色调
- 绘制 WDK GDI，半色调
- 半色调 WDK GDI
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fb74d11881592c43860f4b99efda65c6f98b049f
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96820371"
---
# <a name="gdi-halftoning-capabilities"></a>GDI 半色调功能


## <span id="ddk_gdi_halftoning_capabilities_gg"></span><span id="DDK_GDI_HALFTONING_CAPABILITIES_GG"></span>


GDI 半色调产生质量抖动或彩色半色调图像，用于打印设备或显示尚未内置此类功能的设备。 颜色半色调提供：

-   在给定的设备上能够获得最高质量的颜色和灰度复制。

-   使用一组有限的强度级别提高了视觉分辨率。

-   改善了不同输出设备的颜色相关性。

传统模拟半色调是使用半色调屏幕的移动电话进程。 半色调屏幕包含大小相等的单元格，具有固定单元间距的中心到中心。 固定单元间距可容纳墨迹粗细，而每个单元格中的圆点大小可能会改变，从而产生连续色调的印象。

在计算机上，大部分打印或屏幕底纹也使用固定单元像素大小。 若要模拟可变点大小，可通过组合群集像素来模拟半色调屏幕。 在基于 Windows NT 的操作系统中，GDI 包含了半色调默认参数，这些参数可提供良好的第一个近似值。 其他特定于设备的信息可添加到系统中，以改进输出。

 

 





