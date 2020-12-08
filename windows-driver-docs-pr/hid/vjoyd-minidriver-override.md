---
title: VJoyD 微型驱动程序重写
description: VJoyD 微型驱动程序重写
keywords:
- 操纵杆 WDK HID，替代
- 虚拟游戏杆驱动程序 WDK HID，替代
- VJoyD WDK HID，替代
- 覆盖 virtual 微型驱动程序 WDK 操纵杆
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f0675113299d8775ce1548be6a818307cf9dec82
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96794971"
---
# <a name="vjoyd-minidriver-override"></a>VJoyD 微型驱动程序重写





如果 USB/HID 设备未加载 JoyHID 设备驱动程序，则在与其他 USB/HID 设备一起使用时，有时会显示 "游戏选项" 控制面板中存在的重复设备条目。 当 JoyHID 兼容设备与非 JoyHID 设备同时连接到系统时，会发生这种情况。

如果设备使用的是 VJoyD 微型驱动程序而不是 JoyHID （由设备制造商或关联开发），则可以通过在注册表中正确设置设备类型密钥和相关的命名值来防止这些问题。 本主题中所述的功能仅适用于类型密钥格式为 "VID \_ *VVVV*&PID \_ *pppp*" 的设备，其中字母 *v* 和 *p* 为零填充的供应商和产品的产品 ID 值。

给定格式正确的类型键后，以下步骤会阻止 JoyHID 尝试从设备检索数据或在 "控制面板/添加列表" 中显示不必要的设备条目。

-   将 OEMData 设置为 "乐趣 \_ HWS \_ AUTOLOAD"。 这会阻止设备名称显示在设备的 "添加" 列表中。

-   将 OEMCallout 设置为应为设备加载的驱动程序。 这会阻止为设备加载 JoyHID。

-   将 OEMName 设置为适用于设备的名称。

如果需要，可以将注册表值设置为任意值，以防止 JoyHID 从设备读取数据。 例如，你可以使用以下值：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>“属性”</th>
<th>“值”</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>OEMName</p></td>
<td><p>"不使用 IHV 设备 X 的条目，请不要删除"</p></td>
</tr>
<tr class="even">
<td><p>OEMData</p></td>
<td><p>OEMData 是包含两个 Dword 的二进制注册表字段。 第一个是一组 JOY_HWS_ * 标志，第二个是设备上的按钮数。 标志 JOY_HWS_AUTOLOAD 的值在 dinput 中定义为0x10000000。 由于这种情况下的按钮数量无关，因此八个字节 (十六进制) 应为00、00、00、10、00、00、00、00。</p></td>
</tr>
<tr class="odd">
<td><p>OEMCallout</p></td>
<td><p>用</p></td>
</tr>
</tbody>
</table>

 

请注意，这些值仅阻止 JoyHID 尝试从设备读取数据。 如果设备使用的是 VJoyD 微型驱动程序，则应设置前面的值，以正确反映要加载的设备名称和驱动程序。

 

 




