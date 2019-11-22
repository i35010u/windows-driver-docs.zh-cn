---
title: 基于 COM 的渲染插件
description: 基于 COM 的渲染插件
ms.assetid: c80d6c2b-ba4d-4bd1-bd3a-8c1b0bf29884
keywords:
- 基于 COM 的呈现插件 WDK 打印
- 呈现插件 WDK 打印，基于 COM
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 875f69820cd46736e7236ac76ae1e9dd272266dd
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842875"
---
# <a name="com-based-rendering-plug-ins"></a>基于 COM 的渲染插件





若要提供自定义挂钩函数，基于 COM 的呈现插件必须实现[**IPrintOemUni：： EnableDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemuni-enabledriver)或[**IPrintOemPS：： EnableDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemps-enabledriver)方法，该方法使用每个挂钩函数的地址填充[**DRVENABLEDATA**](https://docs.microsoft.com/windows/desktop/api/winddi/ns-winddi-tagdrvenabledata)结构。

仅当 Unidrv 或 Pscript5 驱动程序定义函数时，基于 COM 的呈现插件才能挂钩图形 DDI 函数。 有关此类函数的列表，请参阅[**IPrintOemUni：： EnableDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemuni-enabledriver)或[**IPrintOemPS：： EnableDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemps-enabledriver)。

如果提供特定的自定义挂钩函数，该函数将抢先于驱动程序的等效图形 DDI 函数。 设计自定义挂钩函数时，可以使用以下选项：

-   挂钩函数可在内部完全处理图形 DDI 操作。

-   挂钩函数可以回调到打印机驱动程序的等效图形 DDI 函数。

通过回叫驱动程序的图形 DDI 函数，挂钩函数可以执行函数参数的预处理或后处理，但仍允许驱动程序实际执行图形 DDI 操作。 呈现插件的[**IPrintOemUni：： EnablePDEV**](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemuni-enablepdev)或[**IPrintOemPS：： EnablePDEV**](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemps-enablepdev)方法的输入参数之一是[**DRVENABLEDATA**](https://docs.microsoft.com/windows/desktop/api/winddi/ns-winddi-tagdrvenabledata)结构，其中包含指向驱动程序图形 DDI 函数的指针。 如果要回调这些函数，应保存此结构的内容。

可能需要提供[自定义的 PDEV 结构](customized-pdev-structures.md)。 可以通过每个挂钩函数作为输入接收的[**SURFOBJ**](https://docs.microsoft.com/windows/desktop/api/winddi/ns-winddi-_surfobj)结构指针，从图形 DDI 挂钩函数内引用此结构。 具体而言，SURFOBJ 结构的**dhpdev**成员指向[**DEVOBJ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/printoem/ns-printoem-_devobj)结构，DEVOBJ 结构的**pdevOEM**成员指向您的自定义 PDEV 结构。

 

 




