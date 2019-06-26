---
title: 确定设备是否可以唤醒系统
description: 确定设备是否可以唤醒系统
ms.assetid: 59f23035-4169-4dd4-ac60-882c32efda2c
keywords:
- 等待/唤醒 Irp WDK 电源管理具有唤醒功能的设备
- 电源管理 WDK 内核，唤醒功能
- 外部唤醒信号 WDK
- 唤醒设备
- 唤醒功能 WDK 电源管理
- 设备唤醒 ups WDK 电源管理
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: f73513baa10a47e6bacbbd8ba5bc2e83251f696a
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67378019"
---
# <a name="determining-whether-a-device-can-wake-the-system"></a>确定设备是否可以唤醒系统





在设备进入睡眠状态中的外部信号可以响应某些设备，例如键盘、 调制解调器和网络卡。 作为其电源管理技术的一部分，操作系统提供了一种方法对于此类设备唤醒处于睡眠状态的系统，然后还原其以前的上下文。 软件唤醒机制使系统能够唤醒从 S5 以外的所有状态 (**PowerSystemShutdown**)，取决于系统和设备的硬件和 BIOS 中的支持。 处于状态 S5 必须始终重新启动系统。

尽管 operating system 旨在从任何中间睡眠状态唤醒，但确切唤醒功能在不同计算机到计算机和设备。 并非所有计算机都支持所有系统睡眠状态;因此，可以从某些状态唤醒的功能是在某些计算机上没有任何意义。

同样，大多数设备都不支持所有设备的电源状态 (通过 D3 D0)，也不都支持唤醒从所有设备电源它们都支持的状态。

睡眠状态，设备可以输入，以及从其最多可支持唤醒，描述在枚举总线驱动程序并存储在状态[**设备\_功能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_device_capabilities)结构。 下表列出了相关来等待/唤醒支持此结构的成员。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>成员</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="deviced1-and-deviced2.md" data-raw-source="[&lt;strong&gt;DeviceD1&lt;/strong&gt;](deviced1-and-deviced2.md)"><strong>DeviceD1</strong></a></p></td>
<td><p>如果设备支持 PowerDeviceD1 状态，则为 true。</p></td>
</tr>
<tr class="even">
<td><p><a href="deviced1-and-deviced2.md" data-raw-source="[&lt;strong&gt;DeviceD2&lt;/strong&gt;](deviced1-and-deviced2.md)"><strong>DeviceD2</strong></a></p></td>
<td><p>如果设备支持 PowerDeviceD2 状态，则为 true。</p></td>
</tr>
<tr class="odd">
<td><p><a href="wakefromd0--wakefromd1--wakefromd2--and-wakefromd3.md" data-raw-source="[&lt;strong&gt;WakeFromD0&lt;/strong&gt;](wakefromd0--wakefromd1--wakefromd2--and-wakefromd3.md)"><strong>WakeFromD0</strong></a></p></td>
<td><p>如果设备可以从 PowerDeviceD0 唤醒，则为 true。</p></td>
</tr>
<tr class="even">
<td><p><a href="wakefromd0--wakefromd1--wakefromd2--and-wakefromd3.md" data-raw-source="[&lt;strong&gt;WakeFromD1&lt;/strong&gt;](wakefromd0--wakefromd1--wakefromd2--and-wakefromd3.md)"><strong>WakeFromD1</strong></a></p></td>
<td><p>如果设备可以从 PowerDeviceD1 唤醒，则为 true。</p></td>
</tr>
<tr class="odd">
<td><p><a href="wakefromd0--wakefromd1--wakefromd2--and-wakefromd3.md" data-raw-source="[&lt;strong&gt;WakeFromD2&lt;/strong&gt;](wakefromd0--wakefromd1--wakefromd2--and-wakefromd3.md)"><strong>WakeFromD2</strong></a></p></td>
<td><p>如果设备可以从 PowerDeviceD2 唤醒，则为 true。</p></td>
</tr>
<tr class="even">
<td><p><a href="wakefromd0--wakefromd1--wakefromd2--and-wakefromd3.md" data-raw-source="[&lt;strong&gt;WakeFromD3&lt;/strong&gt;](wakefromd0--wakefromd1--wakefromd2--and-wakefromd3.md)"><strong>WakeFromD3</strong></a></p></td>
<td><p>如果设备可以从 PowerDeviceD3 唤醒，则为 true。</p></td>
</tr>
<tr class="odd">
<td><p><a href="devicestate.md" data-raw-source="[&lt;strong&gt;DeviceState&lt;/strong&gt;](devicestate.md)"><strong>DeviceState</strong></a> [PowerSystemMaximum]</p></td>
<td><p>指定此设备可为每个系统电源状态，从 PowerSystemUnspecified PowerSystemShutdown 到支持的最高设备电源状态。</p></td>
</tr>
<tr class="even">
<td><p><a href="systemwake.md" data-raw-source="[&lt;strong&gt;SystemWake&lt;/strong&gt;](systemwake.md)"><strong>SystemWake</strong></a></p></td>
<td><p>指定最低系统电源状态 (通过 S4 S0) 从被唤醒系统。</p></td>
</tr>
<tr class="odd">
<td><p><a href="devicewake.md" data-raw-source="[&lt;strong&gt;DeviceWake&lt;/strong&gt;](devicewake.md)"><strong>DeviceWake</strong></a></p></td>
<td><p>指定最低设备电源状态中唤醒设备可以 (通过 D3 D0)。</p></td>
</tr>
</tbody>
</table>

 

**DeviceWake**项列出了从该设备可以响应唤醒信号的最低设备电源状态。 值 PowerDeviceUnspecified 指示该设备不能将系统唤醒。 **SystemWake**项列出了可从中唤醒系统的最低系统电源状态。 这些值基于父 devnode 的功能和驱动程序不应更改它们。 有关详细信息，请参阅[报告设备电源功能](reporting-device-power-capabilities.md)。

一般情况下，设备可以将系统唤醒如果满足以下条件：

-   设备处于相同或比提供更多支持的电源状态**DeviceWake**值。

-   系统处于相同或比更驱动的电源状态**SystemWake**值。

 

 




