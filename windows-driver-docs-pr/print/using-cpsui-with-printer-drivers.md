---
title: 将打印机驱动程序与 CPSUI 配合使用
description: 将打印机驱动程序与 CPSUI 配合使用
ms.assetid: 898a855d-6a9a-4f98-9ee4-bad439427326
keywords:
- 常用属性页用户界面 WDK 打印，显示属性表页
- CPSUI WDK 打印、 显示属性表页
- 属性表页 WDK 打印显示
- 显示属性表页
- 常见属性页用户界面 WDK 打印，有关 CPSUI
- 打印有关 CPSUI CPSUI WDK
- 属性表页 WDK 打印有关 CPSUI 与打印机驱动程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cf4ae849bf9db95797a2bc59d8f051c6a4f28a5b
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384172"
---
# <a name="using-cpsui-with-printer-drivers"></a>将打印机驱动程序与 CPSUI 配合使用





打印后台处理程序，结合[打印机接口 Dll](printer-interface-dll.md)，使用 CPSUI 创建属性表页打印的文档和打印机设备。 应用程序 （如 Microsoft Word) 显示打印文档的属性表时，会涉及以下步骤：

1.  在应用程序调用打印后台处理程序的**DocumentProperties**函数 （Microsoft Windows SDK 文档中所述），并指定该文档是要打印的打印机。

2.  打印后台处理程序调用 CPSUI 的入口点函数， [ **CommonPropertySheetUI**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/compstui/nf-compstui-commonpropertysheetuia)，指定一个内部[ **PFNPROPSHEETUI**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/compstui/nc-compstui-pfnpropsheetui)-类型化的回调函数。

3.  CPSUI 调用后台处理程序的 PFNPROPSHEETUI 类型的回调函数。

4.  后台处理程序的类型化 PFNPROPSHEETUI 回调函数将调用 CPSUI 的[ **ComPropSheet** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/compstui/nc-compstui-pfncompropsheet)函数 (与[ **CPSFUNC\_添加\_PFNPROPSHEETUI** ](https://docs.microsoft.com/previous-versions/ff546391(v=vs.85))函数代码) 通知相应的打印机接口的 DLL 的地址 CPSUI [ **DrvDocumentPropertySheets** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/winddiui/nf-winddiui-drvdocumentpropertysheets)函数。

5.  CPSUI 调用的打印机接口 DLL **DrvDocumentPropertySheets**函数。

6.  打印机接口 DLL 的**DrvDocumentPropertySheets**函数将调用 CPSUI 的**ComPropSheet**函数 (通常与[ **CPSFUNC\_添加\_PCOMPROPSHEETUI** ](https://docs.microsoft.com/previous-versions/ff546388(v=vs.85))函数代码) 来提供与属性表页说明 CPSUI 和[页上的事件的回调](page-event-callbacks.md)。

7.  CPSUI 的**ComPropSheet**函数调用**CreatePropertySheetPage** （Windows SDK 文档中所述） 来创建由打印机接口 DLL 指定了属性表页。 然后调用 CPSUI**属性表**（Windows SDK 文档中所述） 以显示属性表页。

下图说明了这些步骤。

![说明在显示属性表中所涉及的模块的关系图](images/usecpsui.png)

当应用程序用户遍历属性表页和修改选项值，操作系统会通知 CPSUI 页面事件并 CPSUI，又调用由打印机接口 DLL 提供的页面事件回调。 页面事件回调处理页面事件，并存储新选择了选项值在内部，根据需要。

当用户通过单击关闭属性表**确定**或**取消**按钮，CPSUI 销毁页，并会导致**CommonPropertySheetUI**函数返回到打印后台处理程序，这再将控制权返回给应用程序。

当应用程序显示而不是打印文档的打印机设备的属性表时，将遵循相同的步骤，不同之处在于应用程序调用的后台处理程序**PrinterProperties**函数和后台处理程序传递打印机接口的 DLL 的地址[ **DrvDevicePropertySheets** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/winddiui/nf-winddiui-drvdevicepropertysheets) CPSUI 的函数。

 

 




