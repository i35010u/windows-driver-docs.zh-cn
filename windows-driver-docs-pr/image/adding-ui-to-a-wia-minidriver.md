---
title: 将 UI 添加到 WIA 微型驱动程序
description: 将 UI 添加到 WIA 微型驱动程序
ms.assetid: 70440de2-0554-4f5b-9ce4-fe060d3077a4
ms.date: 07/18/2018
ms.localizationpriority: medium
ms.openlocfilehash: 0cf90abf8311914176a5fca780a4c27c0682a16a
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89192095"
---
# <a name="adding-ui-to-a-wia-minidriver"></a>将 UI 添加到 WIA 微型驱动程序

可以通过使用 WIA 微型驱动程序安装单独的 DLL，为 WIA 微型驱动程序添加扩展的 UI 或替换 UI 组件。 与 TWAIN 驱动程序不同，WIA 驱动程序的 UI 组件与实际的 WIA 微型驱动程序不同。 UI 组件在应用程序的进程中运行，而 WIA 微型驱动程序在 WIA 服务的进程中运行。 因此，WIA 驱动程序可能不会直接显示 UI;只有驱动程序的 WIA UI 扩展插件模块可以显示 UI。

WIA 允许您向系统提供的对话框添加属性页、提供自定义图标图像或完全替换系统提供的对话框。 属性页扩展机制基于 Microsoft Windows SDK 文档)  (所述的 **IShellPropSheetExt** COM 接口的 shell 定义。 此机制在属性表处理程序下注册 (** \\ \\ ** &lt; *设备 UI* &gt; ** \\ shellex \\ PropertySheetHandlers**) 的 HKCR clsid clsid。

除属性页外，所有设备对话框扩展都需要实现 [IWiaUIExtension 接口](/previous-versions/windows/hardware/drivers/ff545078(v=vs.85)) 。

如果实现了 **IWiaUIExtension** 接口，并且不希望替换系统 UI，则必须 \_ 为 [**IWiaUIExtension：:D evicedialog**](/previous-versions/windows/hardware/drivers/ff545069(v=vs.85)) 方法返回 E NOTIMPL。 任何其他返回值都禁止设备的设备对话框。

必须在进程内 COM 服务器中将 "设备" 对话框作为模式对话框实现，将父级的*pDeviceDialogData*  - &gt; *hwndParent*传递给**DialogBoxParam**函数 (在 Windows SDK 文档) 中进行了介绍。 "设备" 对话框必须返回 \_ "正常"， \_ 如果用户取消对话框，则返回 FALSE; 对于其他错误，则为 FALSE。

[**DEVICEDIALOGDATA**](/windows-hardware/drivers/ddi/wiadevd/ns-wiadevd-tagdevicedialogdata)结构包含实现自定义设备对话框所需的所有数据。

若要为设备提供自定义图标，请实现 [**IWiaUIExtension：： GetDeviceIcon**](/previous-versions/windows/hardware/drivers/ff545075(v=vs.85)) 方法。 此图标由调用方使用 Windows SDK 文档) 中所述的 **DestroyIcon** (进行销毁。

**注意**   WIA 的脚本支持非常有限。 因此，尽管可以替换 UI，但不能仅在脚本中将其取消。

本部分的其余部分包括：

[创建 "Hello World" WIA 微型驱动程序 UI 扩展](creating-a--hello-world--wia-minidriver-ui-extension.md)，这是如何实现您自己的自定义 UI 的完整示例。