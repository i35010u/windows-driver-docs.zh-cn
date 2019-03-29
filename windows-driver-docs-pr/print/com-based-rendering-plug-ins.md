---
title: 基于 COM 的渲染插件
description: 基于 COM 的渲染插件
ms.assetid: c80d6c2b-ba4d-4bd1-bd3a-8c1b0bf29884
keywords:
- 基于 COM 的呈现插件 WDK 打印
- 呈现插件 WDK 打印，基于 COM 的
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d1da5246b412b46034b01f9a19f55894bc1344d6
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56569004"
---
# <a name="com-based-rendering-plug-ins"></a>基于 COM 的渲染插件





若要提供自定义挂钩函数，在基于 COM 的呈现插件必须实现[ **IPrintOemUni::EnableDriver** ](https://msdn.microsoft.com/library/windows/hardware/ff554248)或[ **IPrintOemPS::EnableDriver** ](https://msdn.microsoft.com/library/windows/hardware/ff553212)填充的方法[ **DRVENABLEDATA** ](https://msdn.microsoft.com/library/windows/hardware/ff556206)具有每个挂钩函数的地址结构。

基于 COM 的呈现插件可以挂接图形 DDI 函数中，仅当 Unidrv 或 Pscript5 驱动程序定义的函数。 此类函数的列表，请参阅[ **IPrintOemUni::EnableDriver** ](https://msdn.microsoft.com/library/windows/hardware/ff554248)或[ **IPrintOemPS::EnableDriver**](https://msdn.microsoft.com/library/windows/hardware/ff553212)。

如果您提供特定自定义挂钩函数，该函数会抢占驱动程序的等效图形 DDI 函数。 在设计自定义的挂钩函数时，你具有以下选项：

-   挂钩函数可以完全在内部处理图形 DDI 操作。

-   挂钩函数可以返回到打印机驱动程序的等效图形 DDI 函数调用。

通过调用返回到驱动程序的图形 DDI 函数，挂钩函数可以执行预处理或后续处理的函数自变量，但仍允许驱动程序来实际执行图形 DDI 操作。 呈现插件的输入参数之一[ **IPrintOemUni::EnablePDEV** ](https://msdn.microsoft.com/library/windows/hardware/ff554249)或[ **IPrintOemPS::EnablePDEV** ](https://msdn.microsoft.com/library/windows/hardware/ff553215)方法[ **DRVENABLEDATA** ](https://msdn.microsoft.com/library/windows/hardware/ff556206)结构，其中包含指向驱动程序的图形 DDI 函数的指针。 如果你想要对这些函数回调，则应保存此结构的内容。

可能有必要为您提供[自定义 PDEV 结构](customized-pdev-structures.md)。 可以通过引用内的图形 DDI 挂钩函数，此结构中从[ **SURFOBJ** ](https://msdn.microsoft.com/library/windows/hardware/ff569901)结构指针作为输入接收的每个挂钩函数。 具体而言，该 SURFOBJ 结构的**dhpdev**成员将指向[ **DEVOBJ** ](https://msdn.microsoft.com/library/windows/hardware/ff547573)结构和 DEVOBJ 结构**pdevOEM**成员将指向您的自定义 PDEV 结构。

 

 




