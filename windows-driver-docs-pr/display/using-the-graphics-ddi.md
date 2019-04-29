---
title: 使用图形 DDI
description: 使用图形 DDI
ms.assetid: e48d117b-8c1c-4617-84f8-b0b489b1083a
keywords:
- 绘制 WDK GDI DDI
- GDI WDK Windows 2000 显示 DDI
- 图形驱动程序 WDK Windows 2000 显示 DDI
- DDI WDK 图形
- GDI WDK Windows 2000 显示中函数
- 图形驱动程序 WDK Windows 2000 显示中函数
- 函数 WDK 图形
- 绘制 WDK GDI，函数
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f7c1c3ea3fc87aa17227417af5ae5349a3485d1c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63388984"
---
# <a name="using-the-graphics-ddi"></a>使用图形 DDI


## <span id="ddk_using_the_graphics_ddi_gg"></span><span id="DDK_USING_THE_GRAPHICS_DDI_GG"></span>


在独立于设备的应用程序将调用路由通过图形设备接口 (GDI) 响应，图形驱动程序必须确保其图形设备生成所需的输出。 图形驱动程序通过实现图形设备驱动程序接口 (DDI) 需要尽可能多地控制图形输出。

图形 DDI 函数名称采用*DrvXxx*窗体。 GDI 调用这些*DrvXxx*函数将数据传递给驱动程序。 当应用程序发出请求的 GDI 和 GDI 确定驱动程序支持相关的函数、 GDI 调用该函数。 它是要提供函数的函数完成后返回到 GDI 的驱动程序的责任。

本部分介绍图形的显示和打印机驱动程序的编写器必须注意的 DDI 函数。 图形 DDI 函数声明，结构定义，并且可以在中找到常量*winddi.h*。 有关图形 DDI 函数的详细信息，请参阅[由打印机和显示器驱动程序的 GDI 函数实现](https://msdn.microsoft.com/library/windows/hardware/ff566549)。

在本部分中包含的主题如下所示：

[图形驱动程序函数](graphics-driver-functions.md)

[支持初始化和终止函数](supporting-initialization-and-termination-functions.md)

[在图形驱动程序函数的浮点运算](floating-point-operations-in-graphics-driver-functions.md)

[创建依赖于设备的位图](creating-device-dependent-bitmaps.md)

[支持的图形输出](supporting-graphics-output.md)

[支持图形 DDI 颜色和模式函数](supporting-graphics-ddi-color-and-pattern-functions.md)

[支持图形 DDI 字体和文本函数](supporting-graphics-ddi-font-and-text-functions.md)

[DEVMODEW 结构](the-devmodew-structure.md)

 

 





