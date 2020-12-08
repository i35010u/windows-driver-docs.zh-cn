---
title: 将打印机驱动程序与 CPSUI 配合使用
description: 将打印机驱动程序与 CPSUI 配合使用
keywords:
- 公共属性表用户界面 WDK 打印，显示属性表页
- CPSUI WDK 打印，显示属性页面页面
- 属性表页 WDK 打印，显示
- 显示属性表页
- 公共属性表用户界面 WDK 打印，关于 CPSUI
- CPSUI WDK 打印，关于 CPSUI
- 属性表页 WDK 打印，关于 CPSUI 与打印机驱动程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e936592a58559456e72c2cb1a1359065ce3da67c
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96785995"
---
# <a name="using-cpsui-with-printer-drivers"></a>将打印机驱动程序与 CPSUI 配合使用





打印后台处理程序与 [打印机接口 dll](printer-interface-dll.md)一起使用 CPSUI 为打印文档和打印机设备创建属性表页。 当应用程序 (如 Microsoft Word) 显示打印文档的属性表时，将涉及以下步骤：

1.  应用程序会调用 "打印后台处理程序" 的 **DocumentProperties** 函数 (在 Microsoft Windows SDK 文档) 中说明，指定要打印文档的打印机。

2.  打印后台处理程序调用 CPSUI 的入口点函数 [**CommonPropertySheetUI**](/windows-hardware/drivers/ddi/compstui/nf-compstui-commonpropertysheetuia)，指定内部 [**PFNPROPSHEETUI**](/windows-hardware/drivers/ddi/compstui/nc-compstui-pfnpropsheetui)类型的回调函数。

3.  CPSUI 调用后台处理程序的 PFNPROPSHEETUI 类型的回调函数。

4.  后台处理程序的 PFNPROPSHEETUI 类型回调函数使用 [**CPSFUNC \_ 添加 \_ PFNPROPSHEETUI**](/previous-versions/ff546391(v=vs.85))函数代码调用 CPSUI 的 [**ComPropSheet**](/windows-hardware/drivers/ddi/compstui/nc-compstui-pfncompropsheet) (函数) ，以通知 CPSUI 适当的打印机接口 DLL [**DrvDocumentPropertySheets**](/windows-hardware/drivers/ddi/winddiui/nf-winddiui-drvdocumentpropertysheets)函数的地址。

5.  CPSUI 调用打印机接口 DLL 的 **DrvDocumentPropertySheets** 函数。

6.  打印机接口 DLL 的 **DrvDocumentPropertySheets** 函数将调用 CPSUI 的 **ComPropSheet** 函数， (通常使用 [**CPSFUNC \_ ADD \_ PCOMPROPSHEETUI**](/previous-versions/ff546388(v=vs.85)) 函数代码) 来提供具有属性表页面说明和 [页面事件回调](page-event-callbacks.md)的 CPSUI。

7.  CPSUI 的 **ComPropSheet** 函数调用 Windows SDK 文档) 中所述的 **CreatePropertySheetPage** (来创建打印机接口 DLL 指定的属性表页。 然后，CPSUI 调用 Windows SDK 文档) 中所述的 **属性表** (来显示属性表页。

下图演示了这些步骤。

![说明显示属性表所涉及的模块的关系图](images/usecpsui.png)

当应用程序用户遍历属性表页面并修改选项值时，操作系统会通知 CPSUI 页面事件和 CPSUI，进而调用由打印机接口 DLL 提供的页面事件回叫。 页面事件回调根据需要处理页面事件并在内部存储新选择的选项值。

当用户通过单击 **"确定" 或 "** **取消** " 按钮来关闭属性表时，CPSUI 会销毁页面，并导致 **CommonPropertySheetUI** 函数返回到打印后台处理程序，然后将控制权返回给应用程序。

当应用程序为打印机设备（而不是打印文档）显示属性表时，将遵循相同的步骤，不同的是，应用程序会调用后台处理程序的 **PrinterProperties** 函数，并且后台处理程序将打印机接口 DLL 的 [**DrvDevicePropertySheets**](/windows-hardware/drivers/ddi/winddiui/nf-winddiui-drvdevicepropertysheets) 函数的地址传递到 CPSUI。

 

