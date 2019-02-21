---
title: DeviceState
description: DeviceState
ms.assetid: 4cf650ea-cccf-411c-809f-0a01e2ceb067
keywords:
- DeviceState
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 994521158ddec6fa1af9942cfa7b81e08fb5b98c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56542373"
---
# <a name="devicestate"></a>DeviceState





**DeviceState**的成员[**设备\_功能**](https://msdn.microsoft.com/library/windows/hardware/ff543095)是一个数组[**设备\_POWER\_状态**](https://msdn.microsoft.com/library/windows/hardware/ff543160)情况下创建索引的值[**系统\_POWER\_状态**](https://msdn.microsoft.com/library/windows/hardware/ff564565)值范围从**PowerSystemWorking**到**PowerSystemShutdown**。 数组的每个元素包含设备可以支持的索引，表示的系统电源状态的最大 (highest-powered) 设备电源状态或**PowerDeviceUnspecified**如果不支持系统电源状态。

例如，在一个系统，支持 S0、 S4 和 S5[系统的电源状态](system-power-states.md)，则**DeviceState**数组支持仅 D0 和 D3 状态的设备包含下表中显示的值。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>DeviceState 元素</th>
<th>值</th>
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

 

在系统上支持所有的系统电源状态，下表列出了值的数组将包含设备 D2 中必须存在的状态或更低时系统将转到任何中间恢复睡眠状态，并处于 D3 状态时系统 hibernates。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>DeviceState 元素</th>
<th>值</th>
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

 

请注意，中的条目**DeviceState**数组表示相应的系统电源状态的设备可以支持的最高设备电源状态。 在上述示例中，设备可能处于状态 D3 的任何系统电源状态，状态系统的电源状态 D2 **PowerSystemWorking**通过**PowerSystemSleeping3**，并为系统状态声明 D1**PowerSystemWorking**。

总线驱动程序或 ACPI 筛选器设置这些值基于父设备节点的功能。

作为一般规则，更高级别的驱动程序不应更改这些值。 但是，这样的更改才在极少数情况下，驱动程序可以指定较低的 （不太支持） 状态与总线驱动程序或最初返回的 ACPI 筛选器。 例如，假定**DeviceState**\[**PowerSystemSleeping1** \]映射到**PowerDeviceD2**上, 表中。 驱动程序可以更改此值设置为**PowerDeviceD3**，而不适用于**PowerDeviceD1**或**PowerDeviceD0**。

 

 




