---
title: 管理和优化字体
description: 管理和优化字体
ms.assetid: 5cfc2174-c605-4399-97a6-62f51df21c16
keywords:
- 字体 WDK 图形，管理和优化
- GDI WDK Windows 2000 显示，字体，管理和优化
- 图形驱动程序 WDK Windows 2000 显示、字体、管理和优化
- 发生器 WDK 图形
- 消费者 WDK GDI
- 字形信息 WDK 图形
- GDI WDK Windows 2000 显示、文本输出、管理和优化
- 图形驱动程序 WDK Windows 2000 显示、文本输出、管理和优化字体
- 绘制 WDK GDI，字体，管理和优化
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f6b5a5a3469bcb88c248fe09d0cb2865ce5c5060
ms.sourcegitcommit: b84d760d4b45795be12e625db1d5a4167dc2c9ee
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/17/2020
ms.locfileid: "90715310"
---
# <a name="managing-and-optimizing-fonts"></a>管理和优化字体


## <span id="ddk_managing_and_optimizing_fonts_gg"></span><span id="DDK_MANAGING_AND_OPTIMIZING_FONTS_GG"></span>


生成 *者是可以生成字体的驱动* 程序。 它生成字形信息作为输出，包括字形度量、位图和轮廓。 使用 *者* 是使用字体的驱动程序。 它接受标志符号信息作为用于生成文本输出的输入，并且必须在设备管理的图面上绘制自己的字体或硬件。 驱动程序可以是制造者和使用者。 例如，在处理[**DrvTextOut**](/windows/win32/api/winddi/nf-winddi-drvtextout)调用时，打印机驱动程序可以充当制造者，同时服务于[**DrvQueryFontData**](/windows/win32/api/winddi/nf-winddi-drvqueryfontdata)调用来提供字形度量值并作为使用者。

仅当驱动程序是字体制造者或字体使用者时，才需要使用驱动程序来处理字体。 如果硬件具有驻留字体，则驱动程序必须向 GDI 提供有关此字体的信息，包括 [**IFIMETRICS**](/windows/win32/api/winddi/ns-winddi-_ifimetrics) 结构中的字体指标、从 Unicode 到各个标志符号标识、单个标志符号特性和字偶间距调整表的映射。 还存在驱动程序必须支持的函数。 某些函数是使用特定于驱动程序或设备特定字体的字体驱动程序和驱动程序所必需的。 其他只是字体驱动程序所必需的。

字体函数的支持取决于驱动程序的能力。 一般类型为：

[度量值函数](font-metric-functions.md)

[字形函数](font-driver-functions.md)

[TrueType 函数](truetype-font-driver-functions.md)

 

