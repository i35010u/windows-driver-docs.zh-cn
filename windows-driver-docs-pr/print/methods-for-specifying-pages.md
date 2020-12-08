---
title: 用于指定页面的方法
description: 用于指定页面的方法
keywords:
- 公共属性表用户界面 WDK 打印，指定页面
- CPSUI WDK 打印，指定页面
- 属性表页 WDK 打印，指定
- COMPROPSHEETUI
- PROPSHEETPAGE
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 050630a2dc3dfb75996e3b537631e2655f7869ce
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96807877"
---
# <a name="methods-for-specifying-pages"></a>用于指定页面的方法





应用程序可以使用三种方法中的任意一种来指定要 CPSUI 的属性表页。 下面的每个方法都涉及到调用 CPSUI 的 [**ComPropSheet**](/windows-hardware/drivers/ddi/compstui/nc-compstui-pfncompropsheet) 函数，并指定其中一个 [ComPropSheet 函数代码](/windows-hardware/drivers/ddi/_print/index)。

-   提供 [**COMPROPSHEETUI**](/windows-hardware/drivers/ddi/compstui/ns-compstui-_compropsheetui) 结构

    如果应用程序通过将 COMPROPSHEETUI 结构传递到 **ComPropSheet** 来描述属性表页，则可以：

    -   使用 [CPSUI 提供的页面和模板](cpsui-supplied-pages-and-templates.md) 之一来指定打印机接口 dll 可用于打印机属性表的预定义的标准页面类型。
    -   指定将在页面上显示的一组用户可修改的 [属性表选项](property-sheet-options.md) 。
    -   指定在用户查看或修改页面选项时 CPSUI 将调用的 [页面事件回调](page-event-callbacks.md) 函数。
-   提供 PROPSHEETPAGE 结构

    如果无法使用使用 COMPROPSHEETUI 结构时可用的通用 (标准) 对话框构造页面，则可以使用 Microsoft Windows SDK 文档) 中介绍的 PROPSHEETPAGE (结构来描述属性表页。 打印机接口 Dll 通常不需要使用此方法。

-   提供回调函数

    应用程序可以向 [**ComPropSheet**](/windows-hardware/drivers/ddi/compstui/nc-compstui-pfncompropsheet) 传递 [**PFNPROPSHEETUI**](/windows-hardware/drivers/ddi/compstui/nc-compstui-pfnpropsheetui)类型的回调函数的地址，CPSUI 会立即调用此函数。 回调函数负责调用 **ComPropSheet** 本身来创建属性表页。

    打印后台处理程序使用此方法来通知 CPSUI 存在打印机接口 DLL 的 [**DrvDocumentPropertySheets**](/windows-hardware/drivers/ddi/winddiui/nf-winddiui-drvdocumentpropertysheets) 和 [**DrvDevicePropertySheets**](/windows-hardware/drivers/ddi/winddiui/nf-winddiui-drvdevicepropertysheets) 函数。 同样， *Unidrv* 和 *Pscript* 驱动程序使用这种方法来通知 CPSUI [用户界面插件](user-interface-plug-ins.md)中存在 [**IPrintOemUI：:D ocumentpropertysheets**](/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemui-documentpropertysheets)和 [**IPrintOemUI：:D evicepropertysheets**](/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemui-devicepropertysheets) COM 方法。

无论使用哪种方法指定新页面，都必须通过将组父句柄传递到 **ComPropSheet** 函数，将页面分配给 [组父项](group-parent.md)。

