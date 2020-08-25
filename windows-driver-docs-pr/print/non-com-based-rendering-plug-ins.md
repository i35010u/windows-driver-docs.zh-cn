---
title: 不是基于 COM 的渲染插件
description: 不是基于 COM 的渲染插件
ms.assetid: 435f9754-50be-4a4b-a5b4-b2bc8d66f034
keywords:
- 非基于 COM 的呈现插件 WDK 打印
- 呈现插件 WDK 打印，基于非 COM
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 00e8cc7400f43a70dac4bb42555c8d546889dfcf
ms.sourcegitcommit: 17c1bbc5ea0bef3bbc87794b030a073f905dc942
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/25/2020
ms.locfileid: "88802717"
---
# <a name="non-com-based-rendering-plug-ins"></a>不是基于 COM 的渲染插件





打印机微型驱动程序通过实现 [**OEMEnableDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/printoem/nf-printoem-oemenabledriver) 函数通知核心驱动程序的功能，该函数将填充 [**DRVENABLEDATA**](https://docs.microsoft.com/windows/win32/api/winddi/ns-winddi-tagdrvenabledata) 结构的成员。 应通过[**DRVFN**](https://docs.microsoft.com/windows/win32/api/winddi/ns-winddi-_drvfn)结构的数组地址设置此结构的**pdrvfn**成员。 此数组的每个元素都应该使用函数索引进行初始化，并使用 IHV 实现的其中一个 **OEM**_Xxx_ 函数的地址。  (有关每个 **OEM**_Xxx_ 函数的详细说明，请参阅 [非基于 COM 的 DDI 挂钩函数](https://docs.microsoft.com/windows-hardware/drivers/ddi/_print/index)。 ) 

当应用程序调用 Microsoft Win32 GDI 来执行呈示任务时，Win32 GDI 反过来会调用 Unidrv 或 Pscript5 核心驱动程序，该驱动程序通常会处理该任务。 但是，如果打印机微型驱动程序表明它能够与特定的渲染操作挂钩，则核心驱动程序会将渲染任务传递给 IHV 呈现插件。

例如，假设有一个应用程序，该应用程序调用 Win32 **LineTo** API (Windows SDK 文档) 中所述。 通常，这会导致另一次调用核心驱动程序的 [**DrvLineTo**](https://docs.microsoft.com/windows/win32/api/winddi/nf-winddi-drvlineto) DDI 来绘制线条。 如果打印机微型驱动程序表明它打算将调用挂钩到该 DDI，则 **DrvLineTo** 会立即将调用转发到 IHV 的 [**OEMLineTo**](https://docs.microsoft.com/windows-hardware/drivers/ddi/printoem/nf-printoem-oemlineto) 函数。

IHV 可以实现 **OEMLineTo**或 [非基于 COM 的 DDI 挂钩函数](https://docs.microsoft.com/windows-hardware/drivers/ddi/_print/index)中描述的任何其他挂钩函数，使其能够完全处理呈现操作，也可以回调以使核心驱动程序处理该操作。

可以实现**OEMLineTo** ，如下面的伪代码示例所示：

```cpp
BOOL APIENTRY
  OEMLineTo(
    SURFOBJ  *pso,
    CLIPOBJ  *pco,
    BRUSHOBJ  *pbo,
    LONG  x1,
    LONG  y1,
    LONG  x2,
    LONG  y2,
    RECTL  *prclBounds,
    MIX  mix
)
{
if ( OEM intends to handle the call ) {
 code to handle the call
}
else
// OEM calls Unidrv's DrvLineTo DDI
  bRetVal = (((PFN_DrvLineTo)(poempdev->pfnUnidrv[UD_DrvLineTo])) (
 pso,
            pco,
            pbo,
            x1,
            x2,
 y1,
            y2,
            prclBounds,
            mix,));
}
```

在前面的示例中，表达式

```cpp
poempdev->pfnUnidrv[UD_DrvLineTo]
```

计算结果为核心驱动程序的 **DrvLineTo** DDI 的地址。  (** \_ DrvLineTo**) 表达式之前，它将函数指针转换为相应的类型。 本节中列出的每个挂钩函数都与其自己的函数指针相关联。

请注意，当 **OEM**_Xxx_ DDI 回拨到 Unidrv 核心驱动程序，并且所涉及的表面是设备管理的图面时，Unidrv 可以通过返回 **FALSE**来忽略调用。

 

 




