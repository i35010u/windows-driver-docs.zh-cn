---
title: CPSUI 提供的页面和模板
description: CPSUI 提供的页面和模板
ms.assetid: de33cb29-3941-4232-bd61-d36fb04d69d3
keywords:
- 常用属性页用户界面 WDK 打印模板
- CPSUI WDK 打印，模板
- 属性表页 WDK 打印模板
- 常见的属性页用户界面 WDK 打印、 预定义页面
- CPSUI WDK 打印，预定义的页面
- 属性表页 WDK 打印，预定义的页面
- 预定义的属性表页 WDK CPSUI
- 模板 WDK CPSUI
- 树视图页 WDK CPSUI
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 937d7192ced24d4bd33c22a52f37868197ea9536
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67372450"
---
# <a name="cpsui-supplied-pages-and-templates"></a>CPSUI 提供的页面和模板





CPSUI 提供了一组预定义的属性表页，以及三个页面模板。 预定义的属性表页如下所示：

-   一组三个页面，使用的选项卡标题**布局**，**纸张/质量**，并**高级**。 这些网页应包含对于打印机，文档属性，并可用于创建从打印机界面内 DLL 的属性表[ **DrvDocumentPropertySheets** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/winddiui/nf-winddiui-drvdocumentpropertysheets)函数。

-   单个页面，选项卡标题**高级**。 同样，页应包含对于打印机，文档属性和可用于创建从打印机界面内 DLL 的属性表[ **DrvDocumentPropertySheets** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/winddiui/nf-winddiui-drvdocumentpropertysheets)函数。

-   单个页面，选项卡标题**设备设置**。 此页应包含打印机属性，并可用于创建从打印机界面内 DLL 的属性表[ **DrvDevicePropertySheets** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/winddiui/nf-winddiui-drvdevicepropertysheets)函数。

-   一个单一的通用 treeview 的页面没有预定义的标题。 任何 CPSUI 应用程序可以使用此页。

若要使用预定义的页面，应用程序必须标识它使用**pDlgPage**的成员[ **COMPROPSHEETUI** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/compstui/ns-compstui-_compropsheetui)结构。

CPSUI 还提供了三个预定义的页面模板。 CPSUI 使用这些模板来创建其预定义的页。 应用程序还可以使用它们。 模板由以下内容组成：

-   树视图页面模板，用于创建预定义 CPSUI**高级**并**设备设置**页。 此模板中包含的每个包含一个节点的树视图控件[属性表选项](property-sheet-options.md)。 上下文菜单是树的每个节点与相关联。 每个节点的上下文菜单提供了用户可以修改选项的值的方式。 CPSUI 提供有关此模板，为所有处理 Windows 消息对话框过程[CPSUI 支持窗口控件](cpsui-supported-window-controls.md)。

-   两个多个控件模板，用于创建预定义 CPSUI**布局**并**纸张/质量**页。 CPSUI 提供了有关处理 Windows 消息的所有 CPSUI 支持窗口控件的模板，对话框过程。

若要使用预定义的页面模板，应用程序必须标识它使用**DlgTemplateID**的成员[ **DLGPAGE** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/compstui/ns-compstui-_dlgpage)结构。

 

 




