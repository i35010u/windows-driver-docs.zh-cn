---
title: DeviceState
description: DeviceState
ms.assetid: 4cf650ea-cccf-411c-809f-0a01e2ceb067
keywords:
- DeviceState
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6ce651abbc1813425d239b6c34e0e7abe61d29e4
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72836922"
---
# <a name="devicestate"></a>DeviceState





[**设备\_功能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_device_capabilities)的**DeviceState**成员是一组[**设备\_电源\_状态**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ne-wdm-_device_power_state)值，这些值由[**SYSTEM\_power\_state**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ne-wdm-_system_power_state)值进行索引，范围为从**PowerSystemWorking**到**PowerSystemShutdown**。 数组中的每个元素都包含设备可为索引所表示的系统电源状态支持的最大（最高性能）设备电源状态，如果系统电源状态不受支持，则为**PowerDeviceUnspecified** 。

例如，在仅支持 S0、S4 和 S5[系统电源状态](system-power-states.md)的系统上，仅支持 D0 和 D3 状态的设备的**DeviceState**数组包含下表中显示的值。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>DeviceState 元素</th>
<th>Value</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>DeviceState</strong>[<strong>PowerSystemWorking</strong>]</p></td>
<td><p><strong>PowerDeviceD0</strong></p></td>
</tr>
<tr class="even">
<td><p><strong>DeviceState</strong>[<strong>PowerSystemSleeping1</strong>]</p></td>
<td><p><strong>PowerDeviceUnspecified</strong></p></td>
</tr>
<tr class="odd">
<td><p><strong>DeviceState</strong>[<strong>PowerSystemSleeping2</strong>]</p></td>
<td><p><strong>PowerDeviceUnspecified</strong></p></td>
</tr>
<tr class="even">
<td><p><strong>DeviceState</strong>[<strong>PowerSystemSleeping3</strong>]</p></td>
<td><p><strong>PowerDeviceUnspecified</strong></p></td>
</tr>
<tr class="odd">
<td><p><strong>DeviceState</strong>[<strong>PowerSystemHibernate</strong>]</p></td>
<td><p><strong>PowerDeviceD3</strong></p></td>
</tr>
<tr class="even">
<td><p><strong>DeviceState</strong>[<strong>PowerSystemShutdown</strong>]</p></td>
<td><p><strong>PowerDeviceD3</strong></p></td>
</tr>
</tbody>
</table>

 

在支持所有系统电源状态的系统上，下表列出了在系统 hiberna 的情况下，每次系统进入任何中间睡眠状态且在 D3 状态下，阵列将包含的设备的值tes.

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>DeviceState 元素</th>
<th>Value</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>DeviceState</strong>[<strong>PowerSystemWorking</strong>]</p></td>
<td><p><strong>PowerDeviceD0</strong></p></td>
</tr>
<tr class="even">
<td><p><strong>DeviceState</strong>[<strong>PowerSystemSleeping1</strong>]</p></td>
<td><p><strong>PowerDeviceD2</strong></p></td>
</tr>
<tr class="odd">
<td><p><strong>DeviceState</strong>[<strong>PowerSystemSleeping2</strong>]</p></td>
<td><p><strong>PowerDeviceD2</strong></p></td>
</tr>
<tr class="even">
<td><p><strong>DeviceState</strong>[<strong>PowerSystemSleeping3</strong>]</p></td>
<td><p><strong>PowerDeviceD2</strong></p></td>
</tr>
<tr class="odd">
<td><p><strong>DeviceState</strong>[<strong>PowerSystemHibernate</strong>]</p></td>
<td><p><strong>PowerDeviceD3</strong></p></td>
</tr>
<tr class="even">
<td><p><strong>DeviceState</strong>[<strong>PowerSystemShutdown</strong>]</p></td>
<td><p><strong>PowerDeviceD3</strong></p></td>
</tr>
</tbody>
</table>

 

请注意， **DeviceState**数组中的条目表示设备在相应系统电源状态下可支持的最高设备电源状态。 在前面的示例中，该设备在任何系统电源状态下可能处于 D3 状态，在系统电源状态**PowerSystemWorking**到**PowerSystemSleeping3**，状态 D1 为系统状态**PowerSystemWorking**。

总线驱动程序或 ACPI 筛选器根据父设备节点的功能设置这些值。

作为一般规则，较高级别的驱动程序不应更改这些值。 但是，在这种情况下，在这种情况下需要进行这种更改，驱动程序可以指定比最初返回的总线驱动程序或 ACPI 筛选器更低（驱动的）状态。 例如，假设**DeviceState**\[**PowerSystemSleeping1**\] 映射到**PowerDeviceD2**，如上表中所示。 驱动程序可以将此值更改为**PowerDeviceD3**，但不能更改为**PowerDeviceD1**或**PowerDeviceD0**。

 

 




