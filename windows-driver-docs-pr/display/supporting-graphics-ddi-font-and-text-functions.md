---
title: 支持图形 DDI 字体和文本函数
description: 支持图形 DDI 字体和文本函数
ms.assetid: c8abf3bd-7a5a-4a48-988e-a1de1b426656
keywords:
- 字体 WDK 图形
- GDI WDK Windows 2000 显示字体
- 图形驱动程序 WDK Windows 2000 显示字体
- GDI WDK Windows 2000 显示、 文本输出
- 图形驱动程序 WDK Windows 2000 显示、 文本输出
- 文本输出 WDK 图形
- 绘制 WDK GDI，字体
- 绘制 WDK GDI，文本输出
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a3f8d85aad1255505674b5672949cd426fb44d72
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56522788"
---
# <a name="supporting-graphics-ddi-font-and-text-functions"></a>支持图形 DDI 字体和文本函数


## <span id="ddk_supporting_graphics_ddi_font_and_text_functions_gg"></span><span id="DDK_SUPPORTING_GRAPHICS_DDI_FONT_AND_TEXT_FUNCTIONS_GG"></span>


对于许多设备，GDI 可以处理所有字体函数。 但是，某些驱动程序，可以绘制其自己的字体或其设备表面上的设备的字体。 其他驱动程序是字体驱动程序，它可以向 GDI 提供标志符号位图和/或大纲中，以及字形度量值。 在这些情况下，该驱动程序必须支持的某些可用字体函数。

文本输出是一个更为通用的函数。 如果在图面是一个标准格式位图，GDI 可以处理所有文本输出，除非该驱动程序挂钩掉对的调用来增强性能。 设备管理的面，该驱动程序必须支持文本输出。

以下主题提供有关支持的字体和文本的信息管理功能。

[管理和优化字体](managing-and-optimizing-fonts.md)

[绘制文本](drawing-text.md)

 

 





