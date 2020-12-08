---
title: 微型驱动程序提供的半色调
description: 微型驱动程序提供的半色调
keywords:
- 微型驱动程序提供的半色调 WDK Unidrv
- 自定义半色调 WDK Unidrv
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 183fb03f55c6aabd52fc6da2d58b38c1cf271c03
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96807845"
---
# <a name="minidriver-supplied-halftoning"></a>微型驱动程序提供的半色调





如果指定的颜色格式是每个像素用于渲染图像的位数 (\* DrvBPP) 大于打印机支持的每像素位数 (\* DevBPP 乘以 \* DevNumOfPlanes) ，则必须提供自定义的半色调功能。

若要提供自定义的半色调功能，必须执行以下操作：

-   提供实现 [**IPrintOemUni：： ImageProcessing**](/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemuni-imageprocessing)方法的 [呈现插件](rendering-plug-ins.md)。

-   \*在 GPD 文件中包含半色调功能项，对于每个自定义的半色调方法，都包含一个 \* 描述半色调方法的选项项。  (不使用 [半色调功能的任何选项属性](option-attributes-for-the-halftone-feature.md)。 ) 

-   \*在 GPD 文件中包含 ColorMode 功能项。 对于每个指定的颜色格式选项， \* 如果希望 **IPrintOemUni：： ImageProcessing** 方法处理该颜色格式的半色调，则必须包含 IPCallbackID 属性。

下面的示例定义了两个颜色格式和四个半色调方法。 该示例使用 [选项约束](option-constraints.md) 来指定哪些半色调方法 Unidrv 应该允许用户为每种颜色格式选择。

```cpp
*Feature: ColorMode
{
    *Option: ColorFormat1
    {
        *Name: "Color Format 1"
        *DevBPP: 1
        *DevNumofPlanes: 4
        *ColorPlaneOrder: LIST (CYAN, MAGENTA, YELLOW, BLACK)
        *DrvBPP: 4
        *Constraints: LIST (Halftone.CustomHalftoneMethod1,
+                           Halftone.CustomHalftoneMethod2)
    }
    *Option: ColorFormat2
    {
        *Name: "Color Format 2"
        *DevBPP: 24
        *DevNumofPlanes: 1
        *DrvBPP: 8
        *IPCallbackID: 100
        *Constraints: LIST (Halftone.StandardHalftoneMethod1,
+                           Halftone.StandardHalftoneMethod2)
    }
}
*Feature: Halftone
{
    *Option: StandardHalftoneMethod1
    {
        *Name: "Standard Halftone Method 1"
    }
    *Option: StandardHalftoneMethod2
    {
        *Name: "Standard Halftone Method 2"
    }
    *Option: CustomHalftoneMethod1
    {
        *Name: "Custom Halftone Method 1"
    }
    *Option: CustomHalftoneMethod2
    {
        *Name: "Custom Halftone Method 2"
    }
}
```

在此示例中，"ColorFormat1" 和 "ColorFormat2" ColorMode 选项都表示 Unidrv 可处理的颜色格式，如 [处理颜色格式](handling-color-formats.md)中所述。 对于 ColorFormat2，指定了 \* **IPCallbackID** 属性。 如果打印机用户选择 ColorFormat2 作为颜色格式，则 Unidrv 将调用打印机的 [**IPrintOemUni：： ImageProcessing**](/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemuni-imageprocessing) COM 方法来处理半色调。 此方法的一个参数是一个指针，指向表示当前选定的半色调方法的字符串名称。

有关半色调的详细信息，请参阅 [自定义半色调](customized-halftoning.md)。

 

