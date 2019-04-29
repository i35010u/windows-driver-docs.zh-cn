---
title: 轴选择
description: 轴选择
ms.assetid: 5ba78609-d5e7-44b1-86e8-5a677a19aadd
keywords:
- 游戏杆 WDK HID，轴
- 虚拟游戏杆驱动程序 WDK HID，轴
- VJoyD WDK HID 轴
- 轴 WDK 游戏杆
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ec3007bcf34e6737329a3020ff6566ff42f7fc37
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63390371"
---
# <a name="axis-selection"></a>轴选择





本部分包含有关如何 DirectInput 由 DirectInput 和 Windows 多媒体应用程序映射使用的轴信息。

本部分包括：

[轴选择重写](axis-selection-overrides.md)

[特殊大小写映射](special-case-mappings.md)

### <a name="windows-2000-legacy-interfaces"></a>Windows 2000 中，旧接口

在 Windows 2000 上使用 DirectX 7.0 API 时，设备驱动程序下, 表中所示公开轴的顺序进行轴分配：

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>使用情况页面</th>
<th>用法</th>
<th>DirectInput 轴</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>HID_USAGE_PAGE_GENERIC</p></td>
<td><p>HID_USAGE_GENERIC_X</p></td>
<td><p>GUID_XAxis</p></td>
</tr>
<tr class="even">
<td><p>HID_USAGE_PAGE_GENERIC</p></td>
<td><p>HID_USAGE_GENERIC_Y</p></td>
<td><p>GUID_YAxis</p></td>
</tr>
<tr class="odd">
<td><p>HID_USAGE_PAGE_GENERIC</p></td>
<td><p>HID_USAGE_GENERIC_Z</p></td>
<td><p>GUID_ZAxis</p></td>
</tr>
<tr class="even">
<td><p>HID_USAGE_PAGE_GENERIC</p></td>
<td><p>HID_USAGE_GENERIC_WHEEL</p></td>
<td><p>GUID_ZAxis</p></td>
</tr>
<tr class="odd">
<td><p>HID_USAGE_PAGE_GENERIC</p></td>
<td><p>HID_USAGE_GENERIC_RX</p></td>
<td><p>GUID_RxAxis</p></td>
</tr>
<tr class="even">
<td><p>HID_USAGE_PAGE_GENERIC</p></td>
<td><p>HID_USAGE_GENERIC_RY</p></td>
<td><p>GUID_RyAxis</p></td>
</tr>
<tr class="odd">
<td><p>HID_USAGE_PAGE_GENERIC</p></td>
<td><p>HID_USAGE_GENERIC_RZ</p></td>
<td><p>GUID_RzAxis</p></td>
</tr>
<tr class="even">
<td><p>HID_USAGE_PAGE_GENERIC</p></td>
<td><p>HID_USAGE_GENERIC_HATSWITCH</p></td>
<td><p>GUID_POV</p></td>
</tr>
<tr class="odd">
<td><p>HID_USAGE_PAGE_GENERIC</p></td>
<td><p>HID_USAGE_GENERIC_SLIDER</p></td>
<td><p>GUID_Slider</p></td>
</tr>
<tr class="even">
<td><p>HID_USAGE_PAGE_GENERIC</p></td>
<td><p>HID_USAGE_GENERIC_DIAL</p></td>
<td><p>GUID_Slider</p></td>
</tr>
<tr class="odd">
<td><p>HID_USAGE_PAGE_SIMULATION</p></td>
<td><p>HID_USAGE_SIMULATION_STEERING</p></td>
<td><p>GUID_XAxis</p></td>
</tr>
<tr class="even">
<td><p>HID_USAGE_PAGE_SIMULATION</p></td>
<td><p>HID_USAGE_SIMULATION_ACCELERATOR</p></td>
<td><p>GUID_YAxis</p></td>
</tr>
<tr class="odd">
<td><p>HID_USAGE_PAGE_SIMULATION</p></td>
<td><p>HID_USAGE_SIMULATION_BRAKE</p></td>
<td><p>GUID_RzAxis</p></td>
</tr>
<tr class="even">
<td><p>HID_USAGE_PAGE_SIMULATION</p></td>
<td><p>HID_USAGE_SIMULATION_RUDDER</p></td>
<td><p>GUID_RzAxis</p></td>
</tr>
<tr class="odd">
<td><p>HID_USAGE_PAGE_SIMULATION</p></td>
<td><p>HID_USAGE_SIMULATION_THROTTLE</p></td>
<td><p>GUID_Slider</p></td>
</tr>
<tr class="even">
<td><p>HID_USAGE_PAGE_GAME</p></td>
<td><p>HID_USAGE_ SIMULATION_POV</p></td>
<td><p>GUID_POV</p></td>
</tr>
</tbody>
</table>

 

这些 Guid 是 SetDataFormat 用于匹配的设备对象的请求的数据格式。 对于使用 DIRECTINPUT 编译的应用程序\_版本&lt;0x0600，如果数据格式指定的 GUID\_ZAxis 之前 GUID\_（作为数据格式 does 默认游戏杆） 滑块和滑块上找到设备，才能 z 轴，则滑块将匹配作为 z 轴。 这旨在提供更好地 HID 兼容。

### <a name="windows-9x-platforms"></a>Windows 9x 平台

通过在 Windows 95/98/我的 DirectX 7.0 接口，是一维到 DirectInput 轴 WinMM 轴的映射：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>WinMM Axis</th>
<th>DirectInput 分配</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>X</p></td>
<td><p>GUID_XAxis</p></td>
</tr>
<tr class="even">
<td><p>Y</p></td>
<td><p>GUID_YAxis</p></td>
</tr>
<tr class="odd">
<td><p>Z</p></td>
<td><p>GUID_ZAxis</p></td>
</tr>
<tr class="even">
<td><p>R</p></td>
<td><p>GUID_RzAxis</p></td>
</tr>
<tr class="odd">
<td><p>U</p></td>
<td><p>GUID_Slider</p></td>
</tr>
<tr class="even">
<td><p>V</p></td>
<td><p>GUID_Slider</p></td>
</tr>
</tbody>
</table>

 

WinMM 轴映射以不同的方式通过 DirectX 8.0 的接口，如下所述。

**请注意**  尽管 JoyHID.VxD 不尚未映射控制的车辆控制使用情况、 加速，刹车，它会检查控制的使用情况并如果它找到一个将设备视为 WinMM 汽车控制器。 此外，JoyHID.VxD 的 DirectX 8.0 版本将复制任何 IHV 提供 WinMM 控制器类型标志 (JOY\_工作流服务\_ISYOKE，乐趣\_工作流服务\_ISGAMEPAD，乐趣\_工作流服务\_ISCARCTRL 或乐趣\_工作流服务\_ISHEADTRACKER) 和按钮计数，因此这些类型可以由 IHV OEMData 注册表值中设置。

 

通过 DirectX 8.0 接口所做的映射与所做的旧式界面不同。 下表描述了 DirectX 8.0 接口中的映射。

对于通过 WinMM 检索的数据，默认值映射为：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>WinMM Axis</th>
<th>DirectInput 分配</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>X</p></td>
<td><p>GUID_XAxis</p></td>
</tr>
<tr class="even">
<td><p>Y</p></td>
<td><p>GUID_YAxis</p></td>
</tr>
<tr class="odd">
<td><p>Z</p></td>
<td><p>GUID_Slider</p></td>
</tr>
<tr class="even">
<td><p>R</p></td>
<td><p>GUID_RzAxis</p></td>
</tr>
<tr class="odd">
<td><p>U</p></td>
<td><p>GUID_Slider</p></td>
</tr>
<tr class="even">
<td><p>V</p></td>
<td><p>GUID_Slider</p></td>
</tr>
</tbody>
</table>

 

由于游戏设备上的第三个轴很少是 z 轴，这些映射帮助提供更好地与 Windows 2000，Windows XP 和 Windows 95/98/我 HID 的兼容性。

 

 




