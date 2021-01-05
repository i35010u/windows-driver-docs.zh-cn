---
title: 使用图形 DDI
description: 使用图形 DDI
keywords:
- 绘制 WDK GDI，DDI
- GDI WDK Windows 2000 显示器，DDI
- 图形驱动程序 WDK Windows 2000 显示器，DDI
- DDI WDK 图形
- GDI WDK Windows 2000 显示，功能
- 图形驱动程序 WDK Windows 2000 显示，功能
- 函数 WDK 图形
- 绘制 WDK GDI，函数
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0b1d8dd8c52fb03a4be14269d2fa6ecca8048fdf
ms.sourcegitcommit: abd90176b0416a1170b1c0232943b60543dd6b98
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/29/2020
ms.locfileid: "97812587"
---
# <a name="using-the-graphics-ddi"></a>使用图形 DDI

为了响应通过图形设备接口 (GDI) 的与设备无关的应用程序调用，图形驱动程序必须确保其图形设备生成所需的输出。 图形驱动程序通过实现尽可能多的图形设备驱动程序界面 (DDI) 来控制图形输出。

图形 DDI 函数名称采用 *DrvXxx* 格式。 GDI 调用这些 *DrvXxx* 函数将数据传递给驱动程序。 当应用程序发出 GDI 请求，且 GDI 确定驱动程序支持相关函数时，GDI 将调用此函数。 驱动程序负责提供函数并在函数完成时返回到 GDI。

本部分介绍了显示和打印机驱动程序的编写器必须知道的图形 DDI 函数。 图形 DDI 函数声明、结构定义和常量可以在 *winddi* 中找到。

本节中包含的主题如下所示：

[图形驱动程序函数](graphics-driver-functions.md)

[支持初始化和终止函数](supporting-initialization-and-termination-functions.md)

[图形驱动程序函数中的浮点运算](floating-point-operations-in-graphics-driver-functions.md)

[创建设备相关的位图](creating-device-dependent-bitmaps.md)

[支持图形输出](supporting-graphics-output.md)

[支持图形 DDI 颜色和模式函数](supporting-graphics-ddi-color-and-pattern-functions.md)

[支持图形 DDI 字体和文本函数](supporting-graphics-ddi-font-and-text-functions.md)

[DEVMODEW 结构](the-devmodew-structure.md)

 

