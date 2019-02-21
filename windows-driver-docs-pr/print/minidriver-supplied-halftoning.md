---
title: 微型驱动程序提供半色调
description: 微型驱动程序提供半色调
ms.assetid: 15af499a-c541-4d61-ace3-5a211574674c
keywords:
- 微型驱动程序提供半色调 WDK Unidrv
- 自定义半色调 WDK Unidrv
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4439ad68f41c64474c25cc4a683a1f49da921b94
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56526266"
---
# <a name="minidriver-supplied-halftoning"></a>微型驱动程序提供半色调





如果指定的颜色格式是另一个为其每像素位数用于呈现图像 (\*DrvBPP) 大于每个打印机支持的像素的位数 (\*DevBPP 乘以\*DevNumOfPlanes)，然后你必须提供自定义的半色调的功能。

若要提供自定义的半色调功能，必须执行以下操作：

-   提供[呈现插件](rendering-plug-ins.md)实现[ **IPrintOemUni::ImageProcessing** ](https://msdn.microsoft.com/library/windows/hardware/ff554261)方法。

-   包括半色调\*GPD 文件中，并为每个功能项自定义半色调方法，包括\*选项条目描述的半色调方法。 (不使用任何[选项的半色调功能特性](option-attributes-for-the-halftone-feature.md)。)

-   包括 ColorMode\*功能 GPD 文件中的条目。 对于每一个指定颜色格式设置选项，必须包括\*IPCallbackID 属性，如果您希望您**IPrintOemUni::ImageProcessing**方法以处理该颜色格式的半色调。

下面的示例定义两种颜色格式和四个半色调方法。 该示例使用[选项约束](option-constraints.md)来指定哪些半色调方法 Unidrv 应允许用户选择的每种颜色格式。

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

在示例中，ColorFormat1 和 ColorFormat2 ColorMode 选项表示可以处理 Unidrv，颜色格式，如中所述[处理颜色格式](handling-color-formats.md)。 ColorFormat2，对于\* **IPCallbackID**指定属性。 如果打印机用户选择的颜色格式作为 ColorFormat2，Unidrv 调用打印机[ **IPrintOemUni::ImageProcessing** ](https://msdn.microsoft.com/library/windows/hardware/ff554261) COM 方法以处理半色调。 该方法的参数之一是指向表示当前所选的半色调方法的字符串名称。

有关半色调的详细信息，请参阅[自定义半色调](customized-halftoning.md)。

 

 




