---
title: 支持图形 DDI 字体和文本函数
description: 支持图形 DDI 字体和文本函数
keywords:
- 字体 WDK 图形
- GDI WDK Windows 2000 显示，字体
- 图形驱动程序 WDK Windows 2000 显示，字体
- GDI WDK Windows 2000 显示，文本输出
- 图形驱动程序 WDK Windows 2000 显示，文本输出
- 文本输出 WDK 图形
- 绘制 WDK GDI，字体
- 绘制 WDK GDI，文本输出
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c801fb3c7ce144d7999289ee139550a90ef61368
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96832367"
---
# <a name="supporting-graphics-ddi-font-and-text-functions"></a>支持图形 DDI 字体和文本函数


## <span id="ddk_supporting_graphics_ddi_font_and_text_functions_gg"></span><span id="DDK_SUPPORTING_GRAPHICS_DDI_FONT_AND_TEXT_FUNCTIONS_GG"></span>


对于很多设备，GDI 可以处理所有字体功能。 不过，某些驱动程序可以在设备表面上绘制自己的字体或其设备自己的字体。 其他驱动程序是字体驱动程序，可以提供字形位图和/或轮廓，还可以提供 GDI 的字形指标。 在这些情况下，驱动程序必须支持一些可用的字体函数。

文本输出是更为通用的函数。 如果图面为标准格式的位图，则 GDI 可以处理所有文本输出，除非驱动程序调用以提高性能。 对于设备管理的图面，驱动程序必须支持文本输出。

以下主题提供有关字体和文本管理功能支持的信息。

[管理和优化字体](managing-and-optimizing-fonts.md)

[绘制文本](drawing-text.md)

 

 





