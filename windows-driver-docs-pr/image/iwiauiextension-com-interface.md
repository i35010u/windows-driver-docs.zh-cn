---
title: IWiaUIExtension COM 接口
description: IWiaUIExtension COM 接口
ms.assetid: 10a8e981-889a-46f0-8bf5-da75632d4d94
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 26dc6bab05a1956c6c93f310a23dd76e98d58cf6
ms.sourcegitcommit: 7500a03d1d57e95377b0b182a06f6c7dcdd4748e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "90102858"
---
# <a name="iwiauiextension-com-interface"></a>IWiaUIExtension COM 接口





如果实现了 [IWiaUIExtension 接口](/previous-versions/windows/hardware/drivers/ff545078(v=vs.85))，则可以实现 none、some 或 all **IWiaUIExtension** 方法。 如果某个特定方法返回 E \_ NOTIMPL，系统提供的替代项，而另一个可用，则改用。

**IWiaUIExtension**接口提供了以下方法：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>方法</th>
<th>说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="/previous-versions/windows/hardware/drivers/ff545069(v=vs.85)" data-raw-source="[&lt;strong&gt;IWiaUIExtension::DeviceDialog&lt;/strong&gt;](/previous-versions/windows/hardware/drivers/ff545069(v=vs.85))"><strong>IWiaUIExtension：:D eviceDialog</strong></a></p></td>
<td><p>提供用来替换默认系统用户界面的自定义用户界面。</p></td>
</tr>
<tr class="even">
<td><p><a href="/previous-versions/windows/hardware/drivers/ff545073(v=vs.85)" data-raw-source="[&lt;strong&gt;IWiaUIExtension::GetDeviceBitmapLogo&lt;/strong&gt;](/previous-versions/windows/hardware/drivers/ff545073(v=vs.85))"><strong>IWiaUIExtension::GetDeviceBitmapLogo</strong></a></p></td>
<td><p>获取设备的自定义位图徽标。</p></td>
</tr>
<tr class="odd">
<td><p><a href="/previous-versions/windows/hardware/drivers/ff545075(v=vs.85)" data-raw-source="[&lt;strong&gt;IWiaUIExtension::GetDeviceIcon&lt;/strong&gt;](/previous-versions/windows/hardware/drivers/ff545075(v=vs.85))"><strong>IWiaUIExtension::GetDeviceIcon</strong></a></p></td>
<td><p>获取自定义设备图标。</p></td>
</tr>
</tbody>
</table>

 

[**IWiaUIExtension：:D evicedialog**](/previous-versions/windows/hardware/drivers/ff545069(v=vs.85)) 接受指向 [**DEVICEDIALOGDATA**](/windows-hardware/drivers/ddi/wiadevd/ns-wiadevd-tagdevicedialogdata) *结构)  (* 的指针，该指针包含实现设备对话框所需的所有数据。

设备对话框必须作为模式 Win32 对话框实现，但要服从以下四个约束：

1.  必须使用 CoTaskMemAlloc 分配*pDeviceDialogData*ppWiaItems 中返回的项的数组 -- &gt; **ppWiaItems** ，并使用**CoTaskMemFree** (的应用程序释放这些项的数组 Microsoft Windows SDK) 文档。 **CoTaskMemAlloc**

2.  不得销毁或释放存储在*pDeviceDialogData*pIWiaItemRoot 中的根项  -- &gt; **pIWiaItemRoot**。 你还不得导致根项无效。 例如，您不能调用 WIA \_ CMD \_ 同步设备命令。

3.  返回 \_ "OK" （确定用户请求数据传输）和 "FALSE" 以 \_ 指示用户已取消传输。

4.  请注意确保此组件中不会引入内存或资源泄漏，因为它在应用程序中在进程内运行。

[**IWiaUIExtension：： GetDeviceIcon**](/previous-versions/windows/hardware/drivers/ff545075(v=vs.85)) 允许应用程序使用驱动程序指定的图标。 若要避免资源泄漏，应使用 LR 共享标志在 **LoadImage**中加载此图标 \_ (参阅 Windows SDK 文档) 。

[**IWiaUIExtension：： GetDeviceBitmapLogo**](/previous-versions/windows/hardware/drivers/ff545073(v=vs.85)) 允许应用程序根据需要提供设备和供应商徽标。 目前没有任何系统组件使用此方法。 该位图应为使用 **CreateDIBSection**的 DIB 分配的位图，或使用 LR CreateDIBSection 标志通过 **LoadImage** 进行加载 \_ (参阅 Windows SDK 文档以获取) 详细信息。 这样，应用程序便可提取任何调色板信息，并适应当前或更改的显示器颜色深度。

若要在 WIA 扫描器驱动程序中实现自定义扫描对话框，请使用 **IWiaUIExtension：:D evicedialog** 方法 (上面列出的四个约束) 创建 Win32 模式对话框，并将 DEVICEDIALOGDATA 结构作为 DialogBoxParam 传递到 LPARAM 函数的 *dwInitParam* 参数。

请记住，"设备" 对话框本身并不管理数据传输，这一点很重要。 对话框仅返回指向 **IWiaItem** 接口指针数组的指针， (将属性设置) 从驱动程序到应用程序。 然后，由应用程序来协商传输机制和格式。

