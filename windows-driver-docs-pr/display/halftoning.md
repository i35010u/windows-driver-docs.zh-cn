---
title: 半色调
description: 半色调
ms.assetid: 94cf0d87-055d-470e-94ca-225d519aeb14
keywords:
- GDI WDK Windows 2000 显示，半色调
- 图形驱动程序 WDK Windows 2000 显示，半色调
- 绘制 WDK GDI，半色调
- 半色调 WDK GDI
- 固定单元间距 WDK GDI
- 大小 WDK GDI 半色调
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e99ddb1f2d27578ad14659a2f033d834d6e1fa23
ms.sourcegitcommit: eba1bbec165d56f64d4c1ab5c3f7465dcd299ae3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/29/2020
ms.locfileid: "91510624"
---
# <a name="halftoning"></a>半色调


## <span id="ddk_halftoning_gg"></span><span id="DDK_HALFTONING_GG"></span>


传统模拟半色调使用半色调网屏，其中包含大小相等的单元格，并具有固定单元间距。 固定单元间距可容纳墨迹粗细，而每个单元格中的圆点大小可能会改变，从而产生连续色调的印象。

在计算机上，大部分打印或屏幕底纹也使用固定单元像素大小。 若要模拟可变点大小，可通过组合群集像素来模拟半色调屏幕。 GDI 包含了半色调默认参数，可提供良好的第一个近似值。 其他特定于设备的信息可添加到系统中，以改进输出。

驱动程序通过[**DrvEnablePDEV**](/windows/win32/api/winddi/nf-winddi-drvenablepdev)函数返回的[**GDIINFO**](/windows/win32/api/winddi/ns-winddi-gdiinfo)结构向 gdi 发送与设备相关的规范，gdi 需要执行半色调。 驱动程序通过 GDIINFO 的 **ulHTPatternSize** 成员指定模式大小，此成员定义半色调的首选输出格式。 对于特定设备，半色调与半色调模式大小相关。 GDI 提供了许多预定义的模式大小（从 2 x 2 到 16 x 16）。

对于每个标准模式大小，还会有一个修改后的版本。 它由 \_ 标准模式大小名称上的后缀 "M" 标识。 例如，标准 6 x 6 模式的定义名称为 HT \_ PATSIZE \_ 6x6，而修改后的 6 x 6 模式的名称为 ht \_ PATSIZE \_ 6x6 \_ M) 。 修改后的版本提供了更多的颜色分辨率，但可能会产生水平或垂直噪音的副作用。 此外，由于每种模式大小都与设备分辨率相关，因此适当的模式大小取决于特定的设备。

模式大小 (空间解析) 和颜色解析之间的权衡取决于模式大小。 较大的半色调模式产生更好的颜色分辨率，而较小的模式则会产生最佳的空间分辨率。 确定最佳的模式大小通常是一种试验和错误。 有关详细信息，请参阅 [**GDIINFO**](/windows/win32/api/winddi/ns-winddi-gdiinfo)。

影响半色调的 GDIINFO 结构成员的另一个是 **flHTFlags**，其中包含描述半色调所需设备分辨率的标志。

GDI 处理来自应用程序的颜色调整请求，并通过图形 DDI 将信息传递给驱动程序函数。 如果应用程序选择了半色调，并且图面为标准格式的 *DIB*，则 GDI 将使用其半色调功能处理位图，之后会将位图发送到设备。 在 PostScript 驱动程序中， [**EngStretchBlt**](/windows/win32/api/winddi/nf-winddi-engstretchblt) 函数可以使用 SRCCOPY 模式) 函数中的 [**DrvCopyBits**](/windows/win32/api/winddi/nf-winddi-drvcopybits) 或 [**DrvBitBlt**](/windows/win32/api/winddi/nf-winddi-drvbitblt) (将位图发送到打印机。

例如，允许 GDI 执行半色调，而不是 PostScript 打印机，以提供更快的所见即所得质量的输出。 PostScript 驱动程序的接口允许用户调整半色调，并提供一个复选框，以便在首选打印机内置半色调功能时关闭 GDI 半色调。

[**DrvDitherColor**](/windows/win32/api/winddi/nf-winddi-drvdithercolor)函数可以返回 DCR \_ 半色调值，该值请求 GDI 使用现有设备 (半色调) 调色板来接近颜色。 \_仅当设备包含设备 (半色调) 调色板（如 VGA-16 适配器卡，因为它具有标准固定调色板）时，DCR 半色调才能与显示器驱动程序一起使用。 单色驱动程序（包括大多数光栅打印机）可以使用*DrvDitherColor*中的*iMode*参数来获取良好的灰度效果。

**注意**   Windows 2000 和更高版本不支持24位 (或更高) 设备上的半色调。

 

 

