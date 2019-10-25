---
title: 将打印机驱动程序与 CPSUI 配合使用
description: 将打印机驱动程序与 CPSUI 配合使用
ms.assetid: 898a855d-6a9a-4f98-9ee4-bad439427326
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
ms.openlocfilehash: d0b454eb7513502f5ba7b6a9efdf6f715d5cf939
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844202"
---
# <a name="using-cpsui-with-printer-drivers"></a>将打印机驱动程序与 CPSUI 配合使用





打印后台处理程序与[打印机接口 dll](printer-interface-dll.md)一起使用 CPSUI 为打印文档和打印机设备创建属性表页。 当应用程序（如 Microsoft Word）显示打印文档的属性表时，需要执行以下步骤：

1.  应用程序调用打印后台处理程序的**DocumentProperties**函数（在 Microsoft Windows SDK 文档中进行了描述），并指定要在其上打印文档的打印机。

2.  打印后台处理程序调用 CPSUI 的入口点函数[**CommonPropertySheetUI**](https://docs.microsoft.com/windows-hardware/drivers/ddi/compstui/nf-compstui-commonpropertysheetuia)，指定内部[**PFNPROPSHEETUI**](https://docs.microsoft.com/windows-hardware/drivers/ddi/compstui/nc-compstui-pfnpropsheetui)类型的回调函数。

3.  CPSUI 调用后台处理程序的 PFNPROPSHEETUI 类型的回调函数。

4.  后台处理程序的 PFNPROPSHEETUI 类型回调函数调用 CPSUI 的[**ComPropSheet**](https://docs.microsoft.com/windows-hardware/drivers/ddi/compstui/nc-compstui-pfncompropsheet)函数（使用[**CPSFUNC\_添加\_PFNPROPSHEETUI**](https://docs.microsoft.com/previous-versions/ff546391(v=vs.85))函数代码）来通知 CPSUI 适当的打印机接口 DLL[**的地址DrvDocumentPropertySheets**](https://docs.microsoft.com/windows-hardware/drivers/ddi/winddiui/nf-winddiui-drvdocumentpropertysheets)函数。

5.  CPSUI 调用打印机接口 DLL 的**DrvDocumentPropertySheets**函数。

6.  打印机接口 DLL 的**DrvDocumentPropertySheets**函数调用 CPSUI 的**ComPropSheet**函数（通常使用[**CPSFUNC\_添加\_PCOMPROPSHEETUI**](https://docs.microsoft.com/previous-versions/ff546388(v=vs.85))函数代码）以通过属性表页提供 CPSUI说明和[页面事件回调](page-event-callbacks.md)。

7.  CPSUI 的**ComPropSheet**函数调用**CreatePropertySheetPage** （如 Windows SDK 文档中所述）来创建打印机接口 DLL 指定的属性表页。 然后，CPSUI 调用**属性表**（在 Windows SDK 文档中进行了介绍）以显示属性表页。

下图说明了这些步骤。

![说明显示属性表所涉及的模块的关系图](images/usecpsui.png)

当应用程序用户遍历属性表页面并修改选项值时，操作系统会通知 CPSUI 页面事件和 CPSUI，进而调用由打印机接口 DLL 提供的页面事件回叫。 页面事件回调根据需要处理页面事件并在内部存储新选择的选项值。

当用户通过单击 **"确定" 或 "** **取消**" 按钮来关闭属性表时，CPSUI 会销毁页面，并导致**CommonPropertySheetUI**函数返回到打印后台处理程序，然后将控制权返回给应用程序。

当应用程序为打印机设备（而不是打印文档）显示属性表时，将遵循相同的步骤，不同的是，应用程序会调用后台处理程序的**PrinterProperties**函数，并且后台处理程序将传递打印机的地址接口 DLL 到 CPSUI 的[**DrvDevicePropertySheets**](https://docs.microsoft.com/windows-hardware/drivers/ddi/winddiui/nf-winddiui-drvdevicepropertysheets)函数。

 

 




