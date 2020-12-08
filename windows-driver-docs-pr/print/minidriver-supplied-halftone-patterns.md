---
title: 微型驱动程序提供的半色调模式
description: 微型驱动程序提供的半色调模式
keywords:
- GDI 提供的半色调 WDK Unidrv
- 微型驱动程序提供的半色调 WDK Unidrv
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 94c607b2e53f927c650afb4574c99574dfad4406
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96807847"
---
# <a name="minidriver-supplied-halftone-patterns"></a>微型驱动程序提供的半色调模式





如果使用的是 GDI 支持的半色调方法，则 GDI 允许指定自定义半色调模式。 若要指定自定义的半色调模式，请使用 [半色调功能的选项属性](option-attributes-for-the-halftone-feature.md) ，如下所示：

-   使用 \* rcHTPatternID、 \* HTPatternSize 和 \* HTNumPatterns 属性可以描述存储在资源 DLL 中的半色调模式。 半色调模式资源是二进制数据的三维数组，从 DWORD 地址边界开始。 可以使用以下格式指定它们：计算正确大小并提供所需的地址对齐方式：

    ```cpp
    BYTE HTPatternResource [HTNumPatterns][(HTPatternSize.y*HTPatternSize.x+3) & ~3];
    ```

    在用于创建资源 DLL 的 .rc 文件中，可以按如下所示指定模式：

    ```cpp
    1     RC_HTPATTERN LOADONCALL DISCARDABLE HALFTONE.BIN
    ```

    其中半色调. bin 是包含半色调模式的文件。

-   \*HTCallbackID 特性使你可以指示要在 [呈现插件](rendering-plug-ins.md)中实现 [**IPrintOemUni：： HalftonePattern**](/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemuni-halftonepattern)方法。 \*必须为 **IPrintOemUni：： HalftonePattern** 方法支持的每个模式提供唯一的 *_HTCallbackID_* 值。

可以提供半色调模式资源和/或 **IPrintOemUni：： HalftonePattern** 方法，如下所示：

-   如果只提供半色调模式，Unidrv 将从资源 DLL 中获取模式并将其传递给 GDI。 无法对模式进行加密。

-   如果仅提供 **IPrintOemUni：： HalftonePattern** 方法，则该方法必须生成半色调模式并将其返回给 Unidrv，并将其传递给 GDI。

-   如果要在资源 DLL 中放置加密半色调模式，还必须提供 **IPrintOemUni：： HalftonePattern** 方法以对模式进行解码并将其返回到 Unidrv，然后将其传递给 GDI。

有关半色调的详细信息，请参阅 [自定义半色调](customized-halftoning.md)。

 

