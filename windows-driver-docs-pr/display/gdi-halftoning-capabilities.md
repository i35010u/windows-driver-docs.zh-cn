---
title: GDI 半色调功能
description: GDI 半色调功能
ms.assetid: 57274fd5-fdf6-4041-b52c-4e409465d159
keywords:
- GDI WDK Windows 2000 显示，呈现引擎
- 图形驱动程序 WDK Windows 2000 显示，呈现引擎
- 绘制 WDK GDI，呈现引擎
- 呈现引擎 WDK GDI
- GDI WDK Windows 2000 显示、 半色调
- 图形驱动程序 WDK Windows 2000 显示、 半色调
- 绘制 WDK GDI、 半色调
- 半色调 WDK GDI
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 935fb1ac5cc4162e174ebf38c75706bd2fae111a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56565395"
---
# <a name="gdi-halftoning-capabilities"></a>GDI 半色调功能


## <span id="ddk_gdi_halftoning_capabilities_gg"></span><span id="DDK_GDI_HALFTONING_CAPABILITIES_GG"></span>


GDI 半色调生成打印设备或没有内置此类功能的显示设备的质量抖动或半色调的颜色图像。 颜色半色调提供：

-   最高质量颜色和灰度而擅自复制可以在给定设备上。

-   利用一组有限的强度级别增加 visual 解析。

-   改进的颜色不同的输出设备之间的关联。

传统的模拟半色调是使用半色调屏幕的移动电话进程。 半色调屏幕组成相等大小，使用固定单元格间距中心为中心的单元格。 固定单元格间距可容纳墨迹的粗细，虽然每个单元格内的一个点的大小可以不同生成的连续色调印象。

在计算机上，大多数打印或屏幕明暗度还使用固定单元格像素大小。 若要模拟的可变点大小，群集像素为单位的组合模拟半色调屏幕。 在基于 Windows NT 的操作系统，GDI 包括提供良好的第一个近似的半色调默认参数。 其他特定于设备的信息可以添加到系统，以改进输出。

 

 





