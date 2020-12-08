---
title: 自定义的半色调
description: 自定义的半色调
keywords:
- Unidrv，半色调
- 半色调 WDK Unidrv
- 自定义半色调 WDK Unidrv
- Unidrv WDK 打印
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5ffb40534ca39d7bff034677448b756d651b4425
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96797397"
---
# <a name="customized-halftoning"></a>自定义的半色调





Unidrv 允许使用 GDI、打印机设备或自定义驱动程序代码执行半色调操作。 本部分介绍如何在自定义驱动程序代码中执行半色调运算。

提供两种类型的自定义项：

-   自定义半色调模式

-   自定义半色调方法

### <a name="customized-halftone-patterns"></a><a href="" id="ddk-customized-halftone-patterns-gg"></a>自定义半色调模式

可以在资源 DLL 中指定半色调模式，也可以通过实现 [**IPrintOemUni：： HalftonePattern**](/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemuni-halftonepattern) 方法的呈现插件生成它们。 此方法的参考页提供了如何生成半色调模式的示例。

如果满足以下任一条件，则应实现 [**IPrintOemUni：： HalftonePattern**](/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemuni-halftonepattern) ：

-   自定义模式在资源 DLL 中提供，并对模式进行了加密。

-   资源 DLL 中不提供自定义模式。 相反，它们是通过 [**IPrintOemUni：： HalftonePattern**](/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemuni-halftonepattern)生成的。

[**IPrintOemUni：： HalftonePattern**](/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemuni-halftonepattern)方法的用途是将可用半色调模式返回到 Unidrv，后者又将其传递到 GDI。 方法可以将存储在资源 DLL 中的模式解码为加密格式，也可以在执行期间生成模式。

如果实现 [**IPrintOemUni：： HalftonePattern**](/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemuni-halftonepattern) 方法，则 *GPD* 文件必须 \* 在每个半色调选项条目中包含一个 HTCallbackID 属性 \* ，该属性指定使用自定义模式的半色调方法。

有关此属性的详细信息，请参阅 [半色调功能的选项属性](option-attributes-for-the-halftone-feature.md)。

### <a name="customized-halftoning-methods"></a><a href="" id="ddk-customized-halftoning-methods-gg"></a>自定义半色调方法

对于使用 Unidrv 的打印机，提供实现自定义半色调方法的代码的步骤如下所示：

1.  提供实现 [**IPrintOemUni：： ImageProcessing**](/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemuni-imageprocessing) 方法的呈现插件。

2.  \*在打印机的 GPD 文件中包含一个半色调功能条目，其中每个包含 \* 一个表示半色调方法的选项项。 可以同时包含 (标准和自定义半色调方法。 ) 

[**IPrintOemUni：： ImageProcessing**](/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemuni-imageprocessing)方法接收 GDI 位图作为输入。 方法必须基于当前所选的半色调方法执行半色调运算，并将生成的位图返回到 Unidrv。

如果呈现插件实现 [**IPrintOemUni：： ImageProcessing**](/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemuni-imageprocessing)，它还可以实现 [**IPrintOemUni：： MemoryUsage**](/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemuni-memoryusage)。

有关半色调的详细信息，请参阅 [Unidrv 的半色调](halftoning-with-unidrv.md)。

