---
title: 将 UI 添加到 WIA 微型驱动程序
description: 将 UI 添加到 WIA 微型驱动程序
ms.assetid: 70440de2-0554-4f5b-9ce4-fe060d3077a4
ms.date: 07/18/2018
ms.localizationpriority: medium
ms.openlocfilehash: 3a010fe08a18d18d9e98c3d7f3c0c7b1821b5b70
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56544704"
---
# <a name="adding-ui-to-a-wia-minidriver"></a>将 UI 添加到 WIA 微型驱动程序

可以添加扩展的 UI 或通过使用 WIA 微型驱动程序安装单独的 DLL 替换为 WIA 微型驱动程序的 UI 组件。 与 TWAIN 驱动程序，不同 WIA 驱动程序的 UI 组件是独立于实际 WIA 微型驱动程序。 UI 组件应用程序的进程中运行，而在 WIA 服务的进程中运行 WIA 微型驱动程序。 因此，WIA 驱动程序可能会不直接显示 UI;仅 WIA UI 扩展模块的驱动程序可能会显示 UI。

WIA，可将属性页添加到系统提供的对话框中，提供自定义图标的图像，或完全替换系统提供的对话框。 属性页扩展机制为基础的 shell 定义**IShellPropSheetExt** COM 接口 （Microsoft Windows SDK 文档中所述）。 这种机制注册在属性表处理程序下 (**HKCR\\Clsid\\**&lt;*设备 UI 的 Clsid* &gt;  **\\shellex\\PropertySheetHandlers**)。

所有设备对话框框中的扩展，除属性页中，都需要[IWiaUIExtension 接口](https://msdn.microsoft.com/library/windows/hardware/ff545078)实现。

如果你实现了**IWiaUIExtension**接口，并不想要替换系统用户界面，您必须返回 E\_为 NOTIMPL [ **IWiaUIExtension::DeviceDialog** ](https://msdn.microsoft.com/library/windows/hardware/ff545069)方法。 任何其他返回值将禁止显示设备的设备对话框。

设备对话框必须实现为在进程内 COM 服务器，并传递一个模式对话框*pDeviceDialogData* -&gt;*hwndParent* 到父**DialogBoxParam**函数 （Windows SDK 文档中所述）。 设备对话框必须返回 S\_确定获取成功，S\_FALSE，如果用户取消了对话框中或 COM 错误 HRESULT 的其他错误。

[ **DEVICEDIALOGDATA** ](https://msdn.microsoft.com/library/windows/hardware/ff540560)结构包含的所有实现一个自定义设备对话框所需数据。

若要为设备提供自定义图标，实现[ **IWiaUIExtension::GetDeviceIcon** ](https://msdn.microsoft.com/library/windows/hardware/ff545075)方法。 由调用方使用销毁图标**DestroyIcon** （Windows SDK 文档中所述）。

**请注意**   WIA 具有非常有限的脚本支持。 因此，虽然可能替换 UI，但不能只是在脚本中取消它。

本部分的其余部分包括：

[创建"Hello World"WIA 微型驱动程序用户界面扩展](creating-a--hello-world--wia-minidriver-ui-extension.md)，如何实现自定义 UI 的完整示例。
