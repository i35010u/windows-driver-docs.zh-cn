---
title: IWiaUIExtension COM 接口
description: IWiaUIExtension COM 接口
ms.assetid: 10a8e981-889a-46f0-8bf5-da75632d4d94
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1a66bfc6ddca796e2ff5e95a6b020be87efeaebc
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63381649"
---
# <a name="iwiauiextension-com-interface"></a>IWiaUIExtension COM 接口





如果你实现了[IWiaUIExtension 接口](https://msdn.microsoft.com/library/windows/hardware/ff545078)，可以实现无、 some 或 all **IWiaUIExtension**方法。 如果特定方法返回 E\_NOTIMPL，系统提供替代方法，另一个可用，则使用它。

**IWiaUIExtension**接口提供了以下方法：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>方法</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff545069" data-raw-source="[&lt;strong&gt;IWiaUIExtension::DeviceDialog&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff545069)"><strong>IWiaUIExtension::DeviceDialog</strong></a></p></td>
<td><p>提供替换默认系统用户界面的自定义用户界面。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff545073" data-raw-source="[&lt;strong&gt;IWiaUIExtension::GetDeviceBitmapLogo&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff545073)"><strong>IWiaUIExtension::GetDeviceBitmapLogo</strong></a></p></td>
<td><p>获取自定义位图徽标的设备。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff545075" data-raw-source="[&lt;strong&gt;IWiaUIExtension::GetDeviceIcon&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff545075)"><strong>IWiaUIExtension::GetDeviceIcon</strong></a></p></td>
<td><p>获取自定义设备图标。</p></td>
</tr>
</tbody>
</table>

 

[**IWiaUIExtension::DeviceDialog** ](https://msdn.microsoft.com/library/windows/hardware/ff545069)接受一个指向[ **DEVICEDIALOGDATA** ](https://msdn.microsoft.com/library/windows/hardware/ff540560)结构 (中声明*wiadevd.h*)，它包含实现设备对话框所需的所有数据。

设备对话框中必须实现为模式 Win32 对话框中，受的以下四个限制：

1.  数组中返回的项数*pDeviceDialogData*--&gt;**ppWiaItems**必须使用分配**CoTaskMemAlloc**，并且将释放的应用程序使用**CoTaskMemFree** （请参阅 Microsoft Windows SDK 文档的这两个函数）。

2.  您必须销毁或发布根项存储在*pDeviceDialogData* --&gt;**pIWiaItemRoot**。 你也不得导致根项变得无效。 例如，您必须调用 WIA\_CMD\_同步设备命令。

3.  返回 S\_确定以指示用户请求的数据传输和 S\_FALSE 以指示用户已取消传输。

4.  请务必确保内存或资源泄漏不中引入了此组件，因为它在进程中运行应用程序中。

[**IWiaUIExtension::GetDeviceIcon** ](https://msdn.microsoft.com/library/windows/hardware/ff545075)允许应用程序使用驱动程序指定的图标。 若要避免资源泄漏，此图标应加载与**LoadImage**，使用 LR\_共享标志 （请参阅 Windows SDK 文档）。

[**IWiaUIExtension::GetDeviceBitmapLogo** ](https://msdn.microsoft.com/library/windows/hardware/ff545073)允许应用程序提供适当的设备和供应商的徽标。 目前，没有任何系统组件使用此方法。 位图应该是 DIB 分配位图使用**CreateDIBSection**，或使用加载**LoadImage** lr\_CREATEDIBSECTION 标志 （请参阅 Windows SDK 文档的详细信息信息）。 这允许应用程序中提取任何调色板信息并适应当前或更改显示的颜色深度。

若要在 WIA 扫描程序驱动程序中实现自定义扫描对话框，使用**IWiaUIExtension::DeviceDialog** （与上面列出的四个约束） 的方法来创建 Win32 模式对话框，并传递到 DEVICEDIALOGDATA 结构*dwInitParam*作为 LPARAM DialogBoxParam 函数的参数。

请务必记住设备对话框本身不会管理数据传输。 对话框的只是返回指向数组的指针**IWiaItem**接口指针 （含有属性集） 从驱动程序对应用程序。 这样，它将应用程序负责协商的传输机制和格式。

 

 




