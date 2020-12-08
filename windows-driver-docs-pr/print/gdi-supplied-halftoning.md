---
title: GDI 提供的半色调
description: GDI 提供的半色调
keywords:
- GDI 提供的半色调 WDK Unidrv
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f7d1a00590bbe1d06c464d31972c56fbfc4f25d2
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96836019"
---
# <a name="gdi-supplied-halftoning"></a>GDI 提供的半色调





如果指定的颜色格式是用于呈现图像的每个像素的位数 (\* DrvBPP) 与打印机支持的每个像素位数 (\* 乘以 \* DevNumOfPlanes) ，则由 GDI 处理半色调运算。 例如 \* ，DrvBPP 的值为4， \* DevBPP 等于 one， \* DevNumOfPlanes 等于4。

对于这种情况，只允许使用 GDI 的半色调方法。 这些半色调方法通过标准半色调选项名称（在 " [标准选项](standard-options.md)" 下列出）在 GPD 文件中表示。 若要指定 Unidrv 允许用于打印机的支持 GDI 的半色调方法，请在 \* 半色调功能的选项条目中指定其名称。  (半色调功能是标准 [打印机功能](printer-features.md)之一。 ) 

如果在 GPD 文件中指定了几个半色调方法和颜色模式，并且要限制可使用哪些颜色模式选择的半色调方法，请使用 [选项约束](option-constraints.md)。

\_ \_ 如果在 GPD 文件中未指定半色调选项，Unidrv 将使用标准的 HT PATSIZE AUTO 选项。 HT \_ PATSIZE \_ AUTO 选项导致 Unidrv 使用最佳的标准半色调方法，该方法对于选定的分辨率和颜色模式是最佳的。 这使用户能够在分辨率和颜色模式的各种组合之间切换，而无需了解任何特定组合的最佳半色调选项。

使用 GDI 提供的半色调功能时，可以提供 [微型驱动程序提供的半色调模式](minidriver-supplied-halftone-patterns.md)。

有关颜色格式的详细信息，请参阅 [处理颜色格式](handling-color-formats.md)。

 

 




