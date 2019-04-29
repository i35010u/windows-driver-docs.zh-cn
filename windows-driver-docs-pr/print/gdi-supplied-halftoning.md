---
title: GDI 提供的半色调
description: GDI 提供的半色调
ms.assetid: c7f3d148-4620-4060-bbf8-253e9e35c397
keywords:
- GDI 提供半色调 WDK Unidrv
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d7c0c9abbdf8db43f14fbd86a9bda5e29ca72bca
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63363196"
---
# <a name="gdi-supplied-halftoning"></a>GDI 提供的半色调





如果指定的颜色格式是另一个为其每像素位数用于呈现图像 (\*DrvBPP) 每像素位数相同打印机支持的 (\*DevBPP 乘以\*DevNumOfPlanes)，然后半色调操作由 GDI 处理。 例如， \*DrvBPP 值为 4，与\*DevBPP 等于 1 和\*DevNumOfPlanes 等于 4。

这种情况下，唯一允许的半色调方法是指那些 GDI 提供。 这些半色调方法由在 GPD 文件中的标准半色调选项名称，下列出[标准选项](standard-options.md)。 若要指定你想 Unidrv 以便为您的打印机的 GDI 支持半色调方法，指定在其名称\*选项半色调功能的条目。 (半色调功能是一个标准[打印机功能](printer-features.md)。)

如果在 GPD 文件中，指定几个半色调方法和颜色模式，并且你想要限制可以使用哪些颜色模式，使用选择的半色调方法[选项约束](option-constraints.md)。

Unidrv 使用标准 HT\_PATSIZE\_如果 GPD 文件中未不指定任何半色调选项自动选项。 HT\_PATSIZE\_自动选项将使 Unidrv 使用适于所选的分辨率和颜色模式的标准半色调方法。 这使用户能够在各种分辨率和颜色模式，而无需知道任何特定组合的最佳半色调选项组合之间进行切换。

如果使用 GDI 提供半色调功能，则可以提供[微型驱动程序提供半色调模式](minidriver-supplied-halftone-patterns.md)。

有关颜色格式的详细信息，请参阅[处理颜色格式](handling-color-formats.md)。

 

 




