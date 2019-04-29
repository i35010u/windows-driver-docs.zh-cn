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
ms.openlocfilehash: 3267ce97f51253b7c18b1c09417c2e6c77be1187
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63358607"
---
# <a name="methods-for-specifying-pages"></a>用于指定页面的方法





应用程序可以使用三种方法来指定 CPSUI 到属性表页。 以下方法的每个涉及调用的 CPSUI [ **ComPropSheet** ](https://msdn.microsoft.com/library/windows/hardware/ff546207)函数，并指定之一[ComPropSheet 函数代码](https://msdn.microsoft.com/library/windows/hardware/ff546214)。

-   提供[ **COMPROPSHEETUI** ](https://msdn.microsoft.com/library/windows/hardware/ff546211)结构

    如果应用程序通过将传递到 COMPROPSHEETUI 结构描述的属性表页**ComPropSheet**，它可以：

    -   使用之一[CPSUI 提供页和模板](cpsui-supplied-pages-and-templates.md)要指定预定义的标准页键入该打印机接口 Dll 可以使用打印机属性表。
    -   指定一组的用户可修改[属性工作表选项](property-sheet-options.md)，将出现在该页。
    -   指定[页上的事件回调](page-event-callbacks.md)CPSUI 当用户查看或修改页面的选项时将调用的函数。
-   提供 PROPSHEETPAGE 结构

    可以使用 PROPSHEETPAGE 结构 （Microsoft Windows SDK 文档中所述） 来描述属性表页，如果不能构造使用 COMPROPSHEETUI 结构时使用的常见的 （标准） 对话框的页。 打印机接口 Dll 通常应该不需要使用此方法。

-   提供一个回调函数

    应用程序可以将传递[ **ComPropSheet** ](https://msdn.microsoft.com/library/windows/hardware/ff546207)的地址[ **PFNPROPSHEETUI**](https://msdn.microsoft.com/library/windows/hardware/ff559812)-类型化的回调函数，哪些 CPSUI 立即调用。 回调函数负责调用**ComPropSheet**本身创建属性表页。

    打印后台处理程序使用此方法以打印机接口 DLL 的通知是否存在 CPSUI **DrvDocumentPropertySheets**并*Pscript*驱动程序使用的技术来通知 CPSUI是否存在[**IPrintOemUI::DocumentPropertySheets** ](https://msdn.microsoft.com/library/windows/hardware/ff554173)并[ **IPrintOemUI::DevicePropertySheets** ](https://msdn.microsoft.com/library/windows/hardware/ff554165)中的 COM 方法[用户接口插件](user-interface-plug-ins.md)。

无论哪种方法用于指定新的页面，页面必须将分配给[父级组](group-parent.md)通过将组父传递的句柄**ComPropSheet**函数。

 

 




