---
title: 轴选择
description: 轴选择
ms.assetid: 5ba78609-d5e7-44b1-86e8-5a677a19aadd
keywords:
- 操纵杆 WDK HID，轴
- 虚拟游戏杆驱动程序 WDK HID、轴
- VJoyD WDK HID，轴
- 轴 WDK 操纵杆
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e3901b50184e88e0b759a66a2311e32c5ac9f206
ms.sourcegitcommit: 8835925c6a88efc301dc5e8bd9bca87082416eb6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/18/2020
ms.locfileid: "90777601"
---
# <a name="axis-selection"></a>轴选择

本部分包含有关 DirectInput 如何映射轴以供 DirectInput 和 Windows 多媒体应用程序使用的信息。

## <a name="windows-2000-legacy-interfaces"></a>Windows 2000，旧版接口

在 Windows 2000 上使用 DirectX 7.0 API 时，按设备驱动程序公开轴的顺序进行轴分配，如下表所示：

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>使用情况页</th>
<th>使用情况</th>
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

SetDataFormat 使用这些 Guid 将请求的数据格式与设备对象匹配。 对于使用 DIRECTINPUT 版本0x0600 编译的应用程序 \_ &lt; ，如果数据格式在 \_ guid 滑块之前指定 guid ZAxis \_ (因为默认的操纵杆数据格式) 并在设备上找到 z 轴之前的滑块，则滑块将与 z 轴匹配。 这旨在提供与 HID 更好的兼容性。

## <a name="windows-9x-platforms"></a>Windows 9x 平台

通过 Windows 95/98/Me 上的 DirectX 7.0 接口，Winmm.dll 轴到 DirectInput 轴的映射为一维：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>Winmm.dll 轴</th>
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

Winmm.dll 轴通过 DirectX 8.0 接口以不同方式映射，如下所述。

**注意**   尽管 JoyHID 尚未映射用于方向盘、加速和刹车的车辆控制用途，但它确实会检查方向盘的使用情况，如果找到，它会将设备视为 Winmm.dll car 控制器。 而且，JoyHID 的 DirectX 8.0 版本会将任何 IHV 提供的 Winmm.dll 控制器类型标志复制 (游戏工作 \_ 流服务 \_ ISYOKE、游戏工作流服务 \_ \_ ISGAMEPAD、游戏 \_ hws \_ ISCARCTRL 或游戏工作流服务 \_ \_ ISHEADTRACKER) 和按钮计数，因此，这些类型可由 IHV 在 OEMData 注册表值中进行设置。

DirectX 8.0 接口所做的映射不同于旧接口所进行的映射。 下表描述了 DirectX 8.0 接口中的映射。

对于通过 Winmm.dll 检索到的数据，默认映射为：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>Winmm.dll 轴</th>
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

因为游戏设备上的第三个轴很少是 Z 轴，所以这些映射有助于提供与 Windows 2000、Windows XP 和 Windows 95/98/Me HID 更好的兼容性。
