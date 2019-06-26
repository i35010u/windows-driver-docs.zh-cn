---
title: 不是基于 COM 的渲染插件
description: 不是基于 COM 的渲染插件
ms.assetid: 435f9754-50be-4a4b-a5b4-b2bc8d66f034
keywords:
- 非基于 COM 的呈现插件 WDK 打印
- 呈现插件 WDK 打印，非基于 COM 的
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 18835d4badc8de344162799df9ee0e5af6439783
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384520"
---
# <a name="non-com-based-rendering-plug-ins"></a>不是基于 COM 的渲染插件





打印机微型驱动程序通过实现通知其功能的核心驱动[ **OEMEnableDriver** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/printoem/nf-printoem-oemenabledriver)函数中的成员填充[ **DRVENABLEDATA** ](https://docs.microsoft.com/windows/desktop/api/winddi/ns-winddi-tagdrvenabledata)结构。 **Pdrvfn**应设置此结构的成员的数组地址[ **DRVFN** ](https://docs.microsoft.com/windows/desktop/api/winddi/ns-winddi-_drvfn)结构。 应使用一个函数的索引和的其中一个的地址初始化此数组的每个元素 **OEM * * * Xxx*实现 IHV，分别的函数。 (有关详细说明的每个 **OEM * * * Xxx*函数，请参阅[非基于 COM 的 DDI 挂钩-函数](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_print/index)。)

当应用程序调用 Microsoft Win32 GDI，又执行渲染任务，Win32 GDI 调入 Unidrv 或 Pscript5 核心驱动程序，它通常处理任务。 但是，如果打印机微型驱动程序已指明能够特定呈现的操作，挂接，核心驱动程序将呈现任务传递给 IHV 呈现插件。

例如，假设应用程序调用 Win32 **LineTo** API （Windows SDK 文档中所述）。 通常情况下，这将导致另一个调用到核心驱动[ **DrvLineTo** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvlineto) DDI 绘制直线。 如果打印机微型驱动程序已指明其意图掉此 DDI，但是，调用挂钩**DrvLineTo**立即将转发到 IHV 调用[ **OEMLineTo** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/printoem/nf-printoem-oemlineto)函数。

IHV 可以实现**OEMLineTo**，或任何其他挂钩扩展函数中所述[非基于 COM 的 DDI 挂钩-函数](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_print/index)，以便它可以完全处理呈现操作，或可以回调若要安装内核驱动程序处理该操作。

**OEMLineTo**可实现，如下面的伪代码示例中所示：

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

计算结果为核心驱动程序的地址**DrvLineTo** DDI。 (**PFN\_DrvLineTo**) 它前面的表达式将转换为适当的类型的函数指针。 在本部分中列出的挂钩扩展函数的每个都具有其自己的函数指针相关联。

请注意，当 **OEM * * * Xxx*回 Unidrv 核心驱动程序和图面 DDI 调用所涉及的是设备管理面，Unidrv 可以只需通过返回忽略调用**FALSE**。

 

 




