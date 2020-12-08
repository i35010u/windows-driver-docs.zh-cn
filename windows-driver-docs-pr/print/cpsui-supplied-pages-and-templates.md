---
title: CPSUI 提供的页面和模板
description: CPSUI 提供的页面和模板
keywords:
- 通用属性表用户界面 WDK 打印，模板
- CPSUI WDK 打印，模板
- 属性表页 WDK 打印，模板
- 公共属性表用户界面 WDK 打印，预定义页面
- CPSUI WDK 打印，预定义页面
- 属性表页 WDK 打印，预定义页面
- 预定义的属性表页 WDK CPSUI
- 模板 WDK CPSUI
- treeview 页面 WDK CPSUI
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 715c31cf64ff64712fac830db4479d83d3be2fb2
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96797471"
---
# <a name="cpsui-supplied-pages-and-templates"></a>CPSUI 提供的页面和模板





CPSUI 提供一组预定义的属性表页和三个页面模板。 预定义的属性表页包括：

-   一组三页，其中包含 **布局**、 **纸张/质量** 和 **高级** 选项卡标题。 这些页面旨在包含打印机的文档属性，可用于从打印机接口 DLL 的 [**DrvDocumentPropertySheets**](/windows-hardware/drivers/ddi/winddiui/nf-winddiui-drvdocumentpropertysheets) 函数中创建属性表。

-   单个页面，选项卡标题为 " **高级**"。 同样，页面旨在包含打印机的文档属性，可用于从打印机接口 DLL 的 [**DrvDocumentPropertySheets**](/windows-hardware/drivers/ddi/winddiui/nf-winddiui-drvdocumentpropertysheets) 函数中创建属性表。

-   单个页面，带有 " **设备设置**" 选项卡的标题。 此页面旨在包含打印机属性，可用于从打印机接口 DLL 的 [**DrvDevicePropertySheets**](/windows-hardware/drivers/ddi/winddiui/nf-winddiui-drvdevicepropertysheets) 函数中创建属性表。

-   不带预定义标题的单个通用 treeview 页面。 任何 CPSUI 应用程序都可以使用此页面。

若要使用预定义的页，应用程序必须使用 [**COMPROPSHEETUI**](/windows-hardware/drivers/ddi/compstui/ns-compstui-_compropsheetui)结构的 **pDlgPage** 成员来识别它。

CPSUI 还提供三个预定义的页面模板。 CPSUI 使用这些模板来创建其预定义页面。 应用程序还可以使用它们。 这些模板包括以下各项：

-   Treeview 页面模板，CPSUI 使用该模板创建预定义的 **高级** 和 **设备设置** 页面。 此模板包含一个 treeview 控件，该控件包含每个 [属性表选项](property-sheet-options.md)的节点。 上下文菜单与树的每个节点关联。 每个节点的上下文菜单都提供用户可用于修改选项值的方法。 CPSUI 为此模板提供一个对话框过程，该过程为所有 [CPSUI 支持的窗口控件](cpsui-supported-window-controls.md)处理 Windows 消息。

-   两个多控件模板，CPSUI 使用它创建预定义的 **布局** 和 **纸张/质量** 页面。 CPSUI 为此模板提供一个对话框过程，该过程为所有 CPSUI 支持的窗口控件处理 Windows 消息。

若要使用预定义的页面模板，应用程序必须使用 [**DLGPAGE**](/windows-hardware/drivers/ddi/compstui/ns-compstui-_dlgpage)结构的 **DlgTemplateID** 成员来识别它。

 

