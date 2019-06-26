---
title: 基于 COM 的渲染插件
description: 基于 COM 的渲染插件
ms.assetid: c80d6c2b-ba4d-4bd1-bd3a-8c1b0bf29884
keywords:
- 基于 COM 的呈现插件 WDK 打印
- 呈现插件 WDK 打印，基于 COM 的
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 306c004a28766a0d35f0244454715077256fd303
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67369613"
---
# <a name="com-based-rendering-plug-ins"></a>基于 COM 的渲染插件





若要提供自定义挂钩函数，在基于 COM 的呈现插件必须实现[ **IPrintOemUni::EnableDriver** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintoemuni-enabledriver)或[ **IPrintOemPS::EnableDriver** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintoemps-enabledriver)填充的方法[ **DRVENABLEDATA** ](https://docs.microsoft.com/windows/desktop/api/winddi/ns-winddi-tagdrvenabledata)具有每个挂钩函数的地址结构。

基于 COM 的呈现插件可以挂接图形 DDI 函数中，仅当 Unidrv 或 Pscript5 驱动程序定义的函数。 此类函数的列表，请参阅[ **IPrintOemUni::EnableDriver** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintoemuni-enabledriver)或[ **IPrintOemPS::EnableDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintoemps-enabledriver)。

如果您提供特定自定义挂钩函数，该函数会抢占驱动程序的等效图形 DDI 函数。 在设计自定义的挂钩函数时，你具有以下选项：

-   挂钩函数可以完全在内部处理图形 DDI 操作。

-   挂钩函数可以返回到打印机驱动程序的等效图形 DDI 函数调用。

通过调用返回到驱动程序的图形 DDI 函数，挂钩函数可以执行预处理或后续处理的函数自变量，但仍允许驱动程序来实际执行图形 DDI 操作。 呈现插件的输入参数之一[ **IPrintOemUni::EnablePDEV** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintoemuni-enablepdev)或[ **IPrintOemPS::EnablePDEV** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintoemps-enablepdev)方法[ **DRVENABLEDATA** ](https://docs.microsoft.com/windows/desktop/api/winddi/ns-winddi-tagdrvenabledata)结构，其中包含指向驱动程序的图形 DDI 函数的指针。 如果你想要对这些函数回调，则应保存此结构的内容。

可能有必要为您提供[自定义 PDEV 结构](customized-pdev-structures.md)。 可以通过引用内的图形 DDI 挂钩函数，此结构中从[ **SURFOBJ** ](https://docs.microsoft.com/windows/desktop/api/winddi/ns-winddi-_surfobj)结构指针作为输入接收的每个挂钩函数。 具体而言，该 SURFOBJ 结构的**dhpdev**成员将指向[ **DEVOBJ** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/printoem/ns-printoem-_devobj)结构和 DEVOBJ 结构**pdevOEM**成员将指向您的自定义 PDEV 结构。

 

 




