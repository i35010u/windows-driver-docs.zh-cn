---
title: 用于指定页面的方法
description: 用于指定页面的方法
ms.assetid: 76006a2b-37b9-4490-913e-dcfc01812d43
keywords:
- 公共属性表用户界面 WDK 打印，指定页面
- CPSUI WDK 打印，指定页面
- 属性表页 WDK 打印，指定
- COMPROPSHEETUI
- PROPSHEETPAGE
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: be5aabb12302a4ba4006e17ddf77a490a8e99e41
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841645"
---
# <a name="methods-for-specifying-pages"></a>用于指定页面的方法





应用程序可以使用三种方法中的任意一种来指定要 CPSUI 的属性表页。 下面的每个方法都涉及到调用 CPSUI 的[**ComPropSheet**](https://docs.microsoft.com/windows-hardware/drivers/ddi/compstui/nc-compstui-pfncompropsheet)函数，并指定其中一个[ComPropSheet 函数代码](https://docs.microsoft.com/windows-hardware/drivers/ddi/_print/index)。

-   提供[**COMPROPSHEETUI**](https://docs.microsoft.com/windows-hardware/drivers/ddi/compstui/ns-compstui-_compropsheetui)结构

    如果应用程序通过将 COMPROPSHEETUI 结构传递到**ComPropSheet**来描述属性表页，则可以：

    -   使用[CPSUI 提供的页面和模板](cpsui-supplied-pages-and-templates.md)之一来指定打印机接口 dll 可用于打印机属性表的预定义的标准页面类型。
    -   指定将在页面上显示的一组用户可修改的[属性表选项](property-sheet-options.md)。
    -   指定在用户查看或修改页面选项时 CPSUI 将调用的[页面事件回调](page-event-callbacks.md)函数。
-   提供 PROPSHEETPAGE 结构

    如果无法使用使用 COMPROPSHEETUI 结构时可用的公用（标准）对话框构造页面，则可以使用 PROPSHEETPAGE 结构（在 Microsoft Windows SDK 文档中介绍）来描述属性表页。 打印机接口 Dll 通常不需要使用此方法。

-   提供回调函数

    应用程序可以向[**ComPropSheet**](https://docs.microsoft.com/windows-hardware/drivers/ddi/compstui/nc-compstui-pfncompropsheet)传递[**PFNPROPSHEETUI**](https://docs.microsoft.com/windows-hardware/drivers/ddi/compstui/nc-compstui-pfnpropsheetui)类型的回调函数的地址，CPSUI 会立即调用此函数。 回调函数负责调用**ComPropSheet**本身来创建属性表页。

    打印后台处理程序使用此方法来通知 CPSUI 打印机接口 DLL 的**DrvDocumentPropertySheets**和*Pscript*驱动程序使用该技术来通知 CPSUI 存在[**IPrintOemUI：:D ocumentpropertysheets**](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemui-documentpropertysheets)和[**IPrintOemUI：** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemui-devicepropertysheets)在[用户界面插件](user-interface-plug-ins.md)中:D evicepropertysheets COM 方法。

无论使用哪种方法指定新页面，都必须通过将组父句柄传递到**ComPropSheet**函数，将页面分配给[组父项](group-parent.md)。

 

 




