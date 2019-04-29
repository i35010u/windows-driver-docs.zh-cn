---
title: VJoyD 微型驱动程序重写
description: VJoyD 微型驱动程序重写
ms.assetid: a77d2464-7785-44a9-b527-2224d261feac
keywords:
- 游戏杆 WDK HID，重写
- 虚拟游戏杆驱动程序 WDK HID，重写
- VJoyD WDK HID，重写
- 重写虚拟微型驱动程序 WDK 游戏杆
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7121ec7f010308e588cfed6a580301ee6f5e0de5
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63376725"
---
# <a name="vjoyd-minidriver-override"></a>VJoyD 微型驱动程序重写





不加载 JoyHID.VxD 设备驱动程序的 USB/HID 设备有时可以显示在游戏选项控件面板中，与其他 USB/HID 设备一起使用时存在重复的设备条目。 在同一时间为非 JoyHID 设备 JoyHID 兼容设备附加到系统时，将发生这种情况。

如果你的设备使用 VJoyD 微型驱动程序以外 JoyHID-可能由设备制造商或附属机构-开发可以防止这些问题，请正确设置你的设备类型项和注册表中的相关命名的值。 仅限为窗体中的类型密钥的设备提供了本主题中所述的功能"VID\_*vvvv*& PID\_*pppp*"，其中字母*v*并*p*是零填充供应商和产品的产品的 ID 值。

以下步骤提供格式正确的类型项，防止 JoyHID 从尝试从设备中检索数据或控件面板/添加列表中显示不必要的设备的条目。

-   设置为乐趣的 OEMData\_工作流服务\_自动加载。 这可以防止设备名称显示在设备的添加列表中。

-   将 OEMCallout 设置为应加载设备驱动程序。 这可以防止 JoyHID.VxD 正在加载设备。

-   设置为名称 OEMName 适合于设备。

如果需要您可以设置注册表值为任意值，以防止 JoyHID 从设备读取数据。 例如，可以使用以下值：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>名称</th>
<th>值</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>OEMName</p></td>
<td><p>"IHV 设备 X，未使用的项并删除"</p></td>
</tr>
<tr class="even">
<td><p>OEMData</p></td>
<td><p>OEMData 是包含两个 dword 值的二进制注册表字段。 第一个是一组 JOY_HWS_ * 标志，第二个是在设备上的按钮的数目。 Dinput.h 为 0x10000000 中定义的标志 JOY_HWS_AUTOLOAD 值。 由于这种情况下的按钮的数目是不相关，八个字节 （以十六进制） 应为 00,00,00,10,00,00,00,00。</p></td>
</tr>
<tr class="odd">
<td><p>OEMCallout</p></td>
<td><p>"未使用"</p></td>
</tr>
</tbody>
</table>

 

请注意，这些值只是防止 JoyHID 尝试从设备读取数据。 如果你的设备使用 VJoyD 微型驱动程序，应设置前面的值以正确反映设备名称和要加载的驱动程序。

 

 




