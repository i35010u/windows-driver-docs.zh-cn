---
title: 替换驱动程序提供的属性表页
description: 替换驱动程序提供的属性表页
ms.assetid: b7f79841-f82c-4a60-9c2f-58772a65a5eb
keywords:
- 用户界面插件 WDK 打印，属性表页
- UI 插件 WDK 打印，属性表页
- 属性表页 WDK 打印
- 替换为属性表页
- IPrintCoreUI2
- 打印文档粘滞属性 WDK
- 打印机粘滞属性 WDK 打印
- 设备粘滞属性 WDK 打印
- 粘滞属性 WDK 打印
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4d7bc30e52dcbfc099bd0ebc754cfa33c99055ed
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63382577"
---
# <a name="replacing-driver-supplied-property-sheet-pages"></a>替换驱动程序提供的属性表页





[IPrintCoreUI2 COM 接口](iprintcoreui2-com-interface.md)提供四种方法的 Pscript5 UI 插件正在运行 Windows XP 和更高版本的 Windows 操作系统上时，必须使用它想要完全替换核心驱动程序的标准 UI 页。 （术语核心驱动程序将引用的 Unidrv 或 Pscript5 打印机驱动程序。）这些方法是按如下所示：

[**IPrintCoreUI2::EnumConstrainedOptions**](https://msdn.microsoft.com/library/windows/hardware/ff553045)

[**IPrintCoreUI2::GetOptions**](https://msdn.microsoft.com/library/windows/hardware/ff553069)

[**IPrintCoreUI2::SetOptions**](https://msdn.microsoft.com/library/windows/hardware/ff553081)

[**IPrintCoreUI2::WhyConstrained**](https://msdn.microsoft.com/library/windows/hardware/ff553087)

UI 插件的程序执行期间仅支持这些方法[ **IPrintOemUI::DocumentPropertySheets** ](https://msdn.microsoft.com/library/windows/hardware/ff554173)并[ **IPrintOemUI::DevicePropertySheets**](https://msdn.microsoft.com/library/windows/hardware/ff554165)方法和它们的属性表回调例程。 插件的 UI 支持这些方法来显示其自己的用户界面。 这些方法返回时不受支持，电子\_NOTIMPL。

核心驱动程序显示其自己的属性表 UI 中两种情况下- [ **DrvDocumentPropertySheets**](https://msdn.microsoft.com/library/windows/hardware/ff548548)，并为[ **DrvDevicePropertySheets**](https://msdn.microsoft.com/library/windows/hardware/ff548542). 第一种方法显示仅适用于文档 （文档粘滞属性） 的属性，同时第二个方法会显示应用于设备 （设备或打印机粘滞属性） 的属性。

核心驱动程序会记住它处理的属性表 （以及因此，模式-文档粘性或打印机粘滞） 的类型。 核心驱动程序将该状态信息保存在一个结构 ( [ **OEMUIOBJ** ](https://msdn.microsoft.com/library/windows/hardware/ff559571)结构) 创建的 UI 实例。 当核心驱动程序调用插件的接口方法时，它将指针传递到 OEMUIOBJ 结构，以便当插件调用返回到核心驱动程序从[ **IPrintCoreUI2::EnumConstrainedOptions** ](https://msdn.microsoft.com/library/windows/hardware/ff553045)， [ **IPrintCoreUI2::GetOptions**](https://msdn.microsoft.com/library/windows/hardware/ff553069)， [ **IPrintCoreUI2::SetOptions**](https://msdn.microsoft.com/library/windows/hardware/ff553081)，或[ **IPrintCoreUI2::WhyConstrained**](https://msdn.microsoft.com/library/windows/hardware/ff553087)，这些方法将指针传递到核心驱动程序，它便能确定的模式。

有关**IPrintCoreUI2::EnumConstrainedOptions**， **IPrintCoreUI2::SetOptions**，并**IPrintCoreUI2::WhyConstrained**，仅粘滞文档功能在执行过程中支持**IPrintOemUI::DocumentPropertySheets**或其属性表回调例程和仅打印机粘滞功能支持的执行过程**IPrintOemUI::DevicePropertySheets**或其属性表回调例程。 有关**IPrintCoreUI2::SetOptions**，应忽略其粘性与当前的粘滞模式不匹配任何功能。 当任一**IPrintCoreUI2::EnumConstrainedOptions**或**IPrintCoreUI2::WhyConstrained**调用其粘性不匹配当前的粘滞模式下，该方法应返回一项功能的 E\_INVALIDARG。

有关[ **IPrintCoreUI2::GetOptions**](https://msdn.microsoft.com/library/windows/hardware/ff553069)，在文档粘滞模式下支持粘性文档和打印机粘滞功能 (即，当[ **IPrintOemUI::DocumentPropertySheets** ](https://msdn.microsoft.com/library/windows/hardware/ff554173)或其属性表回调例程正在运行)，但所支持的打印机粘滞模式仅粘滞打印机功能 (当[ **IPrintOemUI::DevicePropertySheets** ](https://msdn.microsoft.com/library/windows/hardware/ff554165)或其属性表回调例程正在运行)。

 

 




