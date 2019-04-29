---
title: 轴选择重写
description: 轴选择重写
ms.assetid: 151c3d19-2f80-4d71-a004-10c16c691fb9
keywords:
- 游戏杆 WDK HID，轴
- 虚拟游戏杆驱动程序 WDK HID，轴
- VJoyD WDK HID 轴
- 轴 WDK 游戏杆
- 重写轴选择 WDK 游戏杆
- 使用情况页面 WDK HID
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 7e9a71b9b80628ad79a6b560ab9afd01bd12ae18
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63390400"
---
# <a name="axis-selection-overrides"></a>轴选择重写





DirectX 8.0 版本引入了一种新机制为硬件供应商提供修改 DirectInput 如何分配适用于符合 hid 标准的设备的轴的能力有限。 通过在设备上使用轴实例的 HID 用法页/使用情况对之间的关联进行初始轴选择。 轴实例在下一个可选的注册表子项中所述**轴**设备类型项的子项。 (请注意，**轴**子项也是在设备类型的密钥下的可选密钥。)内**轴**子项，属性值将存储 DIOBJECTATTRIBUTES 结构。 之前 DirectX 8.0 **wUsagePage**并**wUsage** DIOBJECTATTRIBUTES 结构中的字段赋予非 HID 设备上的对象的 HID 用法页和使用情况。 这些成员已忽略符合 hid 标准的设备。

DirectX 8.0 的版本中，这些成员成为了符合 hid 标准的设备也与相关。 它们描述的 HID 用法页和 DirectInput 应引用的游戏杆数据格式中查找特定 DirectInput 轴的匹配项的使用情况。 硬件供应商可以利用这些字段，对施加 DirectInput 如何映射不同的 Windows 操作系统上的轴中更好的一致性。 但是，这些不是重新映射轴的首选的机制。

**请注意**  轴映射是静态的因此该行为不确定，如果设备正在使用中更改这些值。 如果不能进行轴将建议的匹配，就好像没有映射曾建议继续进行处理。

 

例如，假设游戏杆设备设计为与 HID 的完整实现的平台上使用\_使用情况\_页\_游戏控件。 此类设备可以描述在 HID 作为其 X 和 Y 轴：

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th>Axis</th>
<th>使用情况页面</th>
<th>用法</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>X</p></td>
<td><p>5</p></td>
<td><p>24</p></td>
<td><p>游戏页，向左/向右移动</p></td>
</tr>
<tr class="even">
<td><p>Y</p></td>
<td><p>5</p></td>
<td><p>25</p></td>
<td><p>游戏页，将向前/向后移动</p></td>
</tr>
</tbody>
</table>

 

这些方案不直接识别由 DirectInput （或 JoyHID），因此它们不是对游戏非常有用。 若要获取其识别为 X 和 Y 轴 DirectInput，无法添加以下注册表项：

```cpp
[DIRECT_INPUT_TYPES\ VID_vvvv&PID_pppp)\Axes\0]
     Binary Attributes = 00 00 00 00 05 00 24 00

[DIRECT_INPUT_TYPES\ VID_vvvv&PID_pppp)\Axes\1]
     Binary Attributes = 00 00 00 00 05 00 25 00

Where "DIRECT_INPUT_TYPES" is a token for the following root key:
HKLM\SYSTEM\CurrentControlSet\Control\MediaProperties\PrivateProperties\Joystick\OEM
```

在 DirectInput 7.0 及更低接口、 DirectInput 8.0 接口，以及 JoyHID.Vxd，VJoyD 微型驱动程序用于 WinMM 支持已实现此机制。

在 Windows 95/98/我来说，有三个可能的数据路径 USB 游戏控制器：

-   IHV 可以提供 VJoyD 微型驱动程序报告在相同的数据的 VxD 这样，对于任何其他 VJoyD does 微型驱动程序。 在这种情况下，轴选择完全由 IHV 的控件。

-   DirectInput 可以使用随操作系统一起提供的 HID 实现以与设备通信。 在这种情况下，根据设备固件或注册表标志 （如前面所述） 进行轴选择。

-   可以使用系统默认 HID VJoyD 驱动程序 (JoyHID.VxD)。

DirectInput 使用 JoyHID.VxD （通过 VJoyD.VxD) 读取数据的应用程序指定 DIRECTINPUT\_新版小于 0x0700，或者如果 JOYTYPE\_NOHIDDIRECT 标志指定的设备。 如果直接\_INPUTVERSION 是大于或等于 0x0700，DirectInput 使用 HID 与设备进行交互。

拍摄 JoyHID/VJoyD 路径下, 表与匹配到 HID 使用情况页面/使用情况对 WinMM 轴：

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>WinMM Axis</th>
<th>使用情况页面</th>
<th>用法</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>X</p></td>
<td><p>HID_USAGE_PAGE_GENERIC</p></td>
<td><p>HID_USAGE_GENERIC_X</p></td>
</tr>
<tr class="even">
<td></td>
<td><p>HID_USAGE_PAGE_GENERIC</p></td>
<td><p>HID_USAGE_GENERIC_RY</p></td>
</tr>
<tr class="odd">
<td><p>Y</p></td>
<td><p>HID_USAGE_PAGE_GENERIC</p></td>
<td><p>HID_USAGE_GENERIC_Y</p></td>
</tr>
<tr class="even">
<td></td>
<td><p>HID_USAGE_PAGE_GENERIC</p></td>
<td><p>HID_USAGE_GENERIC_RX</p></td>
</tr>
<tr class="odd">
<td><p>Z</p></td>
<td><p>HID_USAGE_PAGE_GENERIC</p></td>
<td><p>HID_USAGE_GENERIC_Z</p></td>
</tr>
<tr class="even">
<td></td>
<td><p>HID_USAGE_PAGE_SIMULATION</p></td>
<td><p>HID_USAGE_SIMULATION_THROTTLE</p></td>
</tr>
<tr class="odd">
<td></td>
<td><p>HID_USAGE_PAGE_GENERIC</p></td>
<td><p>HID_USAGE_GENERIC_SLIDER</p></td>
</tr>
<tr class="even">
<td></td>
<td><p>HID_USAGE_PAGE_GENERIC</p></td>
<td><p>HID_USAGE_GENERIC_DIAL</p></td>
</tr>
<tr class="odd">
<td><p>R</p></td>
<td><p>HID_USAGE_PAGE_SIMULATION</p></td>
<td><p>HID_USAGE_SIMULATION_RUDDER</p></td>
</tr>
<tr class="even">
<td></td>
<td><p>HID_USAGE_PAGE_GENERIC</p></td>
<td><p>HID_USAGE_GENERIC_RZ</p></td>
</tr>
<tr class="odd">
<td><p>U</p></td>
<td><p>HID_USAGE_PAGE_SIMULATION</p></td>
<td><p>HID_USAGE_SIMULATION_THROTTLE</p></td>
</tr>
<tr class="even">
<td></td>
<td><p>HID_USAGE_PAGE_GENERIC</p></td>
<td><p>HID_USAGE_GENERIC_SLIDER</p></td>
</tr>
<tr class="odd">
<td></td>
<td><p>HID_USAGE_PAGE_GENERIC</p></td>
<td><p>HID_USAGE_GENERIC_DIAL</p></td>
</tr>
<tr class="even">
<td></td>
<td><p>HID_USAGE_PAGE_GENERIC</p></td>
<td><p>HID_USAGE_GENERIC_RY</p></td>
</tr>
<tr class="odd">
<td><p>V</p></td>
<td><p>HID_USAGE_PAGE_GENERIC</p></td>
<td><p>HID_USAGE_GENERIC_RX</p></td>
</tr>
</tbody>
</table>

 

**请注意**  R，你和 V 轴的映射贯穿到下一步轴如果找不到映射，而 X、 Y 和 Z 的映射是完全相互独立。 这是因为 VJoyD.VxD 仅支持连续组轴 （X、 Y、 Z，对于支持 R，但不是 X、 Y、 Z、 U）。 此规则的唯一例外对使用精确的组合的游戏杆 X、 Y 和 R 或 X、 Y、 Z、 R 和 V。映射此方法有助于避免 JoyHID.VxD 使轴分配 VJoyD.VxD 无法容忍不变。

 

 

 




