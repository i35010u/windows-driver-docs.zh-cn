---
title: 半色调
description: 半色调
ms.assetid: 94cf0d87-055d-470e-94ca-225d519aeb14
keywords:
- GDI WDK Windows 2000 显示、 半色调
- 图形驱动程序 WDK Windows 2000 显示、 半色调
- 绘制 WDK GDI、 半色调
- 半色调 WDK GDI
- 修复了单元格间距 WDK GDI
- 大小 WDK GDI 半色调
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 16d3e65adc066313f68e8ba660de1bd98e77cd76
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56545120"
---
# <a name="halftoning"></a>半色调


## <span id="ddk_halftoning_gg"></span><span id="DDK_HALFTONING_GG"></span>


传统的模拟半色调使用半色调屏幕上，组成相等大小，使用固定单元格间距中心为中心的单元格。 固定单元格间距可容纳墨迹的粗细，虽然每个单元格内的一个点的大小可以不同生成的连续色调印象。

在计算机上，大多数打印或屏幕明暗度还使用固定单元格像素大小。 若要模拟的可变点大小，群集像素为单位的组合模拟半色调屏幕。 GDI 包括提供良好的第一个近似的半色调默认参数。 其他特定于设备的信息可以添加到系统，以改进输出。

驱动程序将发送 GDI 的设备相关规范的 GDI 只需通过半色调[ **GDIINFO** ](https://msdn.microsoft.com/library/windows/hardware/ff566484)由返回结构[ **DrvEnablePDEV**](https://msdn.microsoft.com/library/windows/hardware/ff556211)函数。 该驱动程序指定使用的模式大小**ulHTPatternSize** GDIINFO，用于定义半色调的首选的输出格式的成员。 对于特定设备，半色调与半色调模式大小。 GDI 提供了许多预定义的模式大小为 2 x 2 到 16 x 16。

对于每个标准模式大小，还有的修改的版本。 它由后缀"\_M"标准模式大小的名称。 例如，标准 6-6 模式的定义的名称是 HT\_PATSIZE\_6x6，修改后的 6-6 模式的名称时 HT\_PATSIZE\_6x6\_M)。 修改后的版本提供了更大颜色分辨率，但可以产生负面影响的水平或垂直的干扰。 此外，由于每个这些模式大小是依赖于分辨率的设备，合适的模式大小取决于特定设备。

由模式大小决定 （空间解决方法） 的模式大小和颜色分辨率之间的权衡。 更大的半色调模式生成更好的颜色分辨率，而较小的模式会导致空间的最佳分辨率。 确定最佳的模式大小通常是一种试用和错误。 有关详细信息，请参阅[ **GDIINFO**](https://msdn.microsoft.com/library/windows/hardware/ff566484)。

另一种影响半色调 GDIINFO 结构成员是**flHTFlags**，其中包含描述所需的半色调设备分辨率标志。

GDI 句柄的颜色调整请求从应用程序，并将传递到通过图形 DDI 的驱动程序功能的信息。 如果应用程序选择半色调并在图面是一种标准格式*DIB*，GDI 处理之后，使用能力半色调的位图位图发送到设备。 PostScript 驱动程序，在[ **EngStretchBlt** ](https://msdn.microsoft.com/library/windows/hardware/ff565025)函数可以将该位图发送到使用打印机[ **DrvCopyBits** ](https://msdn.microsoft.com/library/windows/hardware/ff556182)或[ **DrvBitBlt** ](https://msdn.microsoft.com/library/windows/hardware/ff556180) （在 SRCCOPY 模式下） 的函数。

让 GDI 执行而不是 PostScript 打印机半色调，例如，提供所见即所得质量更好的速度更快的输出。 PostScript 驱动程序的接口允许用户调整半色调，并提供一个复选框以关闭 GDI 半色调，如果将打印机的内置半色调功能是首选。

[ **DrvDitherColor** ](https://msdn.microsoft.com/library/windows/hardware/ff556202)函数可以返回 DCR\_半色调值，请求 GDI 近似使用现有的设备 （半色调） 调色板的颜色。 DCR\_半色调可用于显示驱动程序仅当设备包含设备 （半色调） 面板中的，如 VGA 16 适配器卡，因为它具有固定面板的标准。 单色驱动程序，包括大多数光栅打印机，可以使用*iMode*中的参数*DrvDitherColor*以获得良好的灰度效果。

**请注意**   Windows 2000 及更高版本不支持 24 位 （或更高版本） 设备上半色调。

 

 

 





