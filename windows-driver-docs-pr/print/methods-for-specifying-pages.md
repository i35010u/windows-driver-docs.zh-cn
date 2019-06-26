---
title: 用于指定页面的方法
description: 用于指定页面的方法
ms.assetid: 76006a2b-37b9-4490-913e-dcfc01812d43
keywords:
- 常用属性页用户界面 WDK 打印，请指定页
- CPSUI WDK 打印，请指定页
- 属性表页 WDK 打印，请指定
- COMPROPSHEETUI
- PROPSHEETPAGE
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e8ee69c614031a743cae0d2a24a3e17b8b9bc87b
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67353509"
---
# <a name="methods-for-specifying-pages"></a>用于指定页面的方法





应用程序可以使用三种方法来指定 CPSUI 到属性表页。 以下方法的每个涉及调用的 CPSUI [ **ComPropSheet** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/compstui/nc-compstui-pfncompropsheet)函数，并指定之一[ComPropSheet 函数代码](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_print/index)。

-   提供[ **COMPROPSHEETUI** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/compstui/ns-compstui-_compropsheetui)结构

    如果应用程序通过将传递到 COMPROPSHEETUI 结构描述的属性表页**ComPropSheet**，它可以：

    -   使用之一[CPSUI 提供页和模板](cpsui-supplied-pages-and-templates.md)要指定预定义的标准页键入该打印机接口 Dll 可以使用打印机属性表。
    -   指定一组的用户可修改[属性工作表选项](property-sheet-options.md)，将出现在该页。
    -   指定[页上的事件回调](page-event-callbacks.md)CPSUI 当用户查看或修改页面的选项时将调用的函数。
-   提供 PROPSHEETPAGE 结构

    可以使用 PROPSHEETPAGE 结构 （Microsoft Windows SDK 文档中所述） 来描述属性表页，如果不能构造使用 COMPROPSHEETUI 结构时使用的常见的 （标准） 对话框的页。 打印机接口 Dll 通常应该不需要使用此方法。

-   提供一个回调函数

    应用程序可以将传递[ **ComPropSheet** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/compstui/nc-compstui-pfncompropsheet)的地址[ **PFNPROPSHEETUI**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/compstui/nc-compstui-pfnpropsheetui)-类型化的回调函数，哪些 CPSUI 立即调用。 回调函数负责调用**ComPropSheet**本身创建属性表页。

    打印后台处理程序使用此方法以打印机接口 DLL 的通知是否存在 CPSUI **DrvDocumentPropertySheets**并*Pscript*驱动程序使用的技术来通知 CPSUI是否存在[**IPrintOemUI::DocumentPropertySheets** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintoemui-documentpropertysheets)并[ **IPrintOemUI::DevicePropertySheets** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintoemui-devicepropertysheets)中的 COM 方法[用户接口插件](user-interface-plug-ins.md)。

无论哪种方法用于指定新的页面，页面必须将分配给[父级组](group-parent.md)通过将组父传递的句柄**ComPropSheet**函数。

 

 




