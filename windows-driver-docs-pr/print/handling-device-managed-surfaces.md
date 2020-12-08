---
title: 处理设备管理的图面
description: 处理设备管理的图面
keywords:
- Unidrv，设备管理的图面
- 设备管理的图面 WDK Unidrv
- surface 设备托管的 WDK Unidrv
- 挂钩图形 DDI 函数 WDK Unidrv
- DrvTextOut
- Unidrv WDK 打印
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3e0ad7b53d0fa76f22fc524727eaaa9ff1d73dcb
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96835835"
---
# <a name="handling-device-managed-surfaces"></a>处理设备管理的图面





当 Unidrv 呈现打印页图像时，它使用 GDI 托管的绘图图面。 所有图像呈现为位图。 对于具有此方案无法利用的功能的设备（如绘制向量的能力），可以为设备托管的绘图图面提供自定义的驱动程序支持。 若要支持设备管理的图面，你必须提供实现以下内容的呈现插件：

-   所有 Unidrv 支持的图形 DDI 绘图函数的一组挂钩函数。 必须挂钩以下函数： [**DrvAlphaBlend**](/windows/win32/api/winddi/nf-winddi-drvalphablend) 
     [**DrvBitBlt**](/windows/win32/api/winddi/nf-winddi-drvbitblt) 
     [**DrvCopyBits**](/windows/win32/api/winddi/nf-winddi-drvcopybits) 
     [**DrvDitherColor**](/windows/win32/api/winddi/nf-winddi-drvdithercolor) 
     [**DrvFillPath**](/windows/win32/api/winddi/nf-winddi-drvfillpath) 
     [**DrvGradientFill**](/windows/win32/api/winddi/nf-winddi-drvgradientfill) 
     [**DrvLineTo**](/windows/win32/api/winddi/nf-winddi-drvlineto) 
     [**DrvPlgBlt**](/windows/win32/api/winddi/nf-winddi-drvplgblt) 
     [**DrvRealizeBrush**](/windows/win32/api/winddi/nf-winddi-drvrealizebrush) 
     [**DrvStretchBlt**](/windows/win32/api/winddi/nf-winddi-drvstretchblt) 
     [**DrvStretchBltROP**](/windows/win32/api/winddi/nf-winddi-drvstretchbltrop) 
     [**DrvStrokeAndFillPath**](/windows/win32/api/winddi/nf-winddi-drvstrokeandfillpath) 
     [**DrvStrokePath**](/windows/win32/api/winddi/nf-winddi-drvstrokepath) 
     [**DrvTextOut**](/windows/win32/api/winddi/nf-winddi-drvtextout) 
     [**DrvTransparentBlt**](/windows/win32/api/winddi/nf-winddi-drvtransparentblt) DrvPlgBlt DrvRealizeBrush DrvStretchBlt DrvStretchBltROP DrvStrokeAndFillPath DrvStrokePath DrvTextOut DrvTransparentBlt
-   [**IPrintOemUni：： EnableDriver**](/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemuni-enabledriver)方法，用于为 Unidrv 提供指向图形 DDI 挂钩函数的指针。

-   [**IPrintOemUni：:D riverdms**](/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemuni-driverdms)方法，该方法通知 Unidrv 要使用的设备托管的图面，并指定要用于该图面的定义的挂钩函数。

在设备管理的图面上进行绘制时，挂钩函数不能回叫 GDI 的 Eng 支持服务。 不过，他们可以创建一个临时位图图面，然后将该图面的控点传递给 Eng 前缀的绘图函数 (参阅 [渲染打印作业](rendering-a-print-job.md)) 。

每次要呈现打印作业时都将调用 [**IPrintOemUni：:D riverdms**](/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemuni-driverdms) 方法，因此呈现插件可以为每个作业指定 (GDI 管理的或设备管理的) 呈现图面的类型。 在用户界面中，选择 "选择" 选项上的 "表面" 选项要求您同时提供 [用户界面插件](user-interface-plug-ins.md)。

### <a name="drawing-text-on-a-device-managed-surface"></a>在 Device-Managed 图面上绘制文本

呈现插件必须将 Unidrv 的 [**DrvTextOut**](/windows/win32/api/winddi/nf-winddi-drvtextout) 函数与) 的所有其他图形 DDI 绘图函数一起挂钩 (。 为设备管理的图面创建文本涉及以下四个函数之间的交互：

-   Unidrv 的 [**DrvTextOut**](/windows/win32/api/winddi/nf-winddi-drvtextout) 函数

-   呈现插件的 [**DrvTextOut**](/windows/win32/api/winddi/nf-winddi-drvtextout) 挂钩函数

-   Unidrv 的 [**IPrintOemDriverUni：:D rvunitextout**](/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemdriveruni-drvunitextout) 方法

-   呈现插件的 [**IPrintOemUni：： TextOutAsBitmap**](/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemuni-textoutasbitmap) 方法

在设备管理的表面上显示文本所涉及的步骤如下所示：

1.  GDI 调用 Unidrv 的 [**DrvTextOut**](/windows/win32/api/winddi/nf-winddi-drvtextout) 函数。

2.  Unidrv 调用呈现插件的 [**DrvTextOut**](/windows/win32/api/winddi/nf-winddi-drvtextout) 挂钩函数。

3.  挂钩函数将命令发送到设备，以指定文本的画笔、旋转和剪辑区域。

4.  挂钩函数调用 Unidrv 的 [**IPrintOemDriverUni：:D rvunitextout**](/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemdriveruni-drvunitextout) 方法，该方法使用已下载的字体输出文本。 此方法还处理基于字形的剪辑。

5.  如果 [**IPrintOemDriverUni：:D rvunitextout**](/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemdriveruni-drvunitextout) 不能使用可下载字体 (因为该字体不可用或) 旋转，它将调用呈现插件的 [**IPrintOemUni：： TextOutAsBitmap**](/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemuni-textoutasbitmap) 方法，该方法将文本绘制为位图。

6.  [**IPrintOemDriverUni：:D rvunitextout**](/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemdriveruni-drvunitextout)返回后， [**DrvTextOut**](/windows/win32/api/winddi/nf-winddi-drvtextout)挂钩函数必须根据 **DrvTextOut** 函数的 *prclExtra* 参数所指定的矩形绘制下划线和删除线，并在支持) 时使用向量命令 (。

 

