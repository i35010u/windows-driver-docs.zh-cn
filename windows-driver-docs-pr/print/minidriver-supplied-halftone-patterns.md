---
title: 微型驱动程序提供的半色调模式
description: 微型驱动程序提供的半色调模式
ms.assetid: db2e1c5c-f337-4875-980d-a75a54a4cece
keywords:
- GDI 提供半色调 WDK Unidrv
- 微型驱动程序提供半色调 WDK Unidrv
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: de1908fd7a75188e0c9891b218d82af93fb134a1
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67382039"
---
# <a name="minidriver-supplied-halftone-patterns"></a>微型驱动程序提供的半色调模式





当使用 GDI 支持半色调方法时，GDI 将允许自定义的半色调模式的规范。 若要指定自定义的半色调模式，请使用[选项的半色调功能特性](option-attributes-for-the-halftone-feature.md)，如下所示：

-   \*RcHTPatternID， \*HTPatternSize 和\*HTNumPatterns 特性，你可以描述存储在资源 DLL 中的半色调模式。 半色调模式资源是 DWORD 地址边界上启动的二进制数据的三维数组。 可以使用正确的大小计算，并提供所需的地址对齐方式的以下格式指定它们：

    ```cpp
    BYTE HTPatternResource [HTNumPatterns][(HTPatternSize.y*HTPatternSize.x+3) & ~3];
    ```

    在.rc 文件中用于创建资源 DLL，可能会按如下所示指定的模式：

    ```cpp
    1     RC_HTPATTERN LOADONCALL DISCARDABLE HALFTONE.BIN
    ```

    其中 halftone.bin 是包含半色调模式的文件。

-   \*HTCallbackID 特性，您可以指示要实施[ **IPrintOemUni::HalftonePattern** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintoemuni-halftonepattern)中的方法[呈现插件](rendering-plug-ins.md). 一个唯一\* **HTCallbackID**值必须为每个模式提供**IPrintOemUni::HalftonePattern**方法支持。

你可以提供半色调模式资源**IPrintOemUni::HalftonePattern**方法，或两者，按如下所示：

-   如果提供只有半色调模式，Unidrv 资源 DLL 中获取模式，并将其传递给 GDI。 不能加密模式。

-   如果仅提供**IPrintOemUni::HalftonePattern**方法，该方法必须生成并返回到 Unidrv，将其传递给 GDI 的半色调模式。

-   如果你想要将加密的半色调模式放在资源 DLL，则还必须提供**IPrintOemUni::HalftonePattern**方法进行解码模式，并将其返回到 Unidrv，又将其传递给 GDI。

有关半色调的详细信息，请参阅[自定义半色调](customized-halftoning.md)。

 

 




