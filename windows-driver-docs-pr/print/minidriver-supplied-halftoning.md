---
title: 微型驱动程序提供的半色调
description: 微型驱动程序提供的半色调
ms.assetid: 15af499a-c541-4d61-ace3-5a211574674c
keywords:
- 微型驱动程序提供的半色调 WDK Unidrv
- 自定义半色调 WDK Unidrv
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1fc1828e70d99dba4bd7a077798e4963e32c7051
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72824268"
---
# <a name="minidriver-supplied-halftoning"></a>微型驱动程序提供的半色调





如果指定的颜色格式是指用于渲染图像的每像素位数（\*DrvBPP）大于打印机支持的每像素位数（\*DevBPP 乘以 \*DevNumOfPlanes），则必须提供自定义半色调功能。

若要提供自定义的半色调功能，必须执行以下操作：

-   提供实现[**IPrintOemUni：： ImageProcessing**](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemuni-imageprocessing)方法的[呈现插件](rendering-plug-ins.md)。

-   在 GPD 文件中包含半色调\*功能项，对于每个自定义的半色调方法，都包含一个说明半色调方法的 \*选项条目。 （不要将任何[选项属性用于半色调功能](option-attributes-for-the-halftone-feature.md)。）

-   在 GPD 文件中包含 ColorMode \*功能项。 对于每个指定的颜色格式选项，如果希望**IPrintOemUni：： ImageProcessing**方法为该颜色格式处理半色调，则必须包含 \*IPCallbackID 属性。

下面的示例定义了两个颜色格式和四个半色调方法。 该示例使用[选项约束](option-constraints.md)来指定哪些半色调方法 Unidrv 应该允许用户为每种颜色格式选择。

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

在此示例中，"ColorFormat1" 和 "ColorFormat2" ColorMode 选项都表示 Unidrv 可处理的颜色格式，如[处理颜色格式](handling-color-formats.md)中所述。 对于 ColorFormat2，指定了一个 \***IPCallbackID**特性。 如果打印机用户选择 ColorFormat2 作为颜色格式，则 Unidrv 将调用打印机的[**IPrintOemUni：： ImageProcessing**](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemuni-imageprocessing) COM 方法来处理半色调。 此方法的一个参数是一个指针，指向表示当前选定的半色调方法的字符串名称。

有关半色调的详细信息，请参阅[自定义半色调](customized-halftoning.md)。

 

 




