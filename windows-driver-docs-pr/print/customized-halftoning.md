---
title: 自定义的半色调
description: 自定义的半色调
ms.assetid: cc14ff92-743b-42ca-b70f-0df768762f01
keywords:
- Unidrv，半色调
- 半色调 WDK Unidrv
- 自定义半色调 WDK Unidrv
- Unidrv WDK 打印
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4555984f5d15bebd98353c4f3c944785aa57974c
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837975"
---
# <a name="customized-halftoning"></a>自定义的半色调





Unidrv 允许使用 GDI、打印机设备或自定义驱动程序代码执行半色调操作。 本部分介绍如何在自定义驱动程序代码中执行半色调运算。

提供两种类型的自定义项：

-   自定义半色调模式

-   自定义半色调方法

### <a href="" id="ddk-customized-halftone-patterns-gg"></a>自定义半色调模式

可以在资源 DLL 中指定半色调模式，也可以通过实现[**IPrintOemUni：： HalftonePattern**](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemuni-halftonepattern)方法的呈现插件生成它们。 此方法的参考页提供了如何生成半色调模式的示例。

如果满足以下任一条件，则应实现[**IPrintOemUni：： HalftonePattern**](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemuni-halftonepattern) ：

-   自定义模式在资源 DLL 中提供，并对模式进行了加密。

-   资源 DLL 中不提供自定义模式。 相反，它们是通过[**IPrintOemUni：： HalftonePattern**](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemuni-halftonepattern)生成的。

[**IPrintOemUni：： HalftonePattern**](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemuni-halftonepattern)方法的用途是将可用半色调模式返回到 Unidrv，后者又将其传递到 GDI。 方法可以将存储在资源 DLL 中的模式解码为加密格式，也可以在执行期间生成模式。

如果实现**IPrintOemUni：： HalftonePattern**文件必须在每个半色调 \*Option 项中包含一个 \*HTCallbackID 属性，该属性指定使用自定义模式的半色调方法。

有关此属性的详细信息，请参阅[半色调功能的选项属性](option-attributes-for-the-halftone-feature.md)。

### <a href="" id="ddk-customized-halftoning-methods-gg"></a>自定义半色调方法

对于使用 Unidrv 的打印机，提供实现自定义半色调方法的代码的步骤如下所示：

1.  提供实现[**IPrintOemUni：： ImageProcessing**](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemuni-imageprocessing)方法的呈现插件。

2.  在打印机的 GPD 文件中包含半色调 \*功能项，其中每个都包含表示半色调方法 \*选项项。 （标准和自定义半色调方法可以同时包含在内。）

[**IPrintOemUni：： ImageProcessing**](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemuni-imageprocessing)方法接收 GDI 位图作为输入。 方法必须基于当前所选的半色调方法执行半色调运算，并将生成的位图返回到 Unidrv。

如果呈现插件实现[**IPrintOemUni：： ImageProcessing**](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemuni-imageprocessing)，它还可以实现[**IPrintOemUni：： MemoryUsage**](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemuni-memoryusage)。

有关半色调的详细信息，请参阅[Unidrv 的半色调](halftoning-with-unidrv.md)。

 

 




