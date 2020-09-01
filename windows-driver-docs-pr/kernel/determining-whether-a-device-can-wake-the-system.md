---
title: 确定设备是否可以唤醒系统
description: 确定设备是否可以唤醒系统
ms.assetid: 59f23035-4169-4dd4-ac60-882c32efda2c
keywords:
- 等待/唤醒 Irp WDK 电源管理，具有唤醒功能的设备
- 电源管理 WDK 内核，唤醒功能
- 外部唤醒信号 WDK
- 唤醒设备
- 唤醒功能 WDK 电源管理
- 设备唤醒 ups WDK 电源管理
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: b1545c428dac981405d2409508abfa9ddcae09ca
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89191928"
---
# <a name="determining-whether-a-device-can-wake-the-system"></a>确定设备是否可以唤醒系统





某些设备（例如键盘、调制解调器和网卡）可以在设备睡眠状态下响应外部信号。 作为其电源管理技术的一部分，操作系统为此类设备提供了一种唤醒睡眠系统的方式，该系统可以还原其以前的上下文。 软件唤醒机制允许系统从除 S5 (**PowerSystemShutdown**) 以外的任何状态唤醒，具体取决于系统和设备硬件和 BIOS 中的支持。 处于 S5 状态的系统必须始终重启。

尽管操作系统旨在从任何中间睡眠状态唤醒，但具体的唤醒功能在不同的计算机和设备之间有所不同。 并非所有计算机都支持所有系统睡眠状态;因此，从某些状态唤醒的能力在某些计算机上无意义。

同样，大多数设备既不支持通过 D3 (D0) 的所有设备电源状态，也不支持从其支持的所有设备电源状态唤醒。

设备可以输入的睡眠状态以及它支持唤醒的状态在总线驱动程序的枚举中进行描述，并存储在 [**设备 \_ 功能**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_device_capabilities) 结构中。 下表列出了与等待/唤醒支持相关的此结构的成员。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>成员</th>
<th>说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="deviced1-and-deviced2.md" data-raw-source="[&lt;strong&gt;DeviceD1&lt;/strong&gt;](deviced1-and-deviced2.md)"><strong>DeviceD1</strong></a></p></td>
<td><p>如果设备支持状态 PowerDeviceD1，则为 True。</p></td>
</tr>
<tr class="even">
<td><p><a href="deviced1-and-deviced2.md" data-raw-source="[&lt;strong&gt;DeviceD2&lt;/strong&gt;](deviced1-and-deviced2.md)"><strong>DeviceD2</strong></a></p></td>
<td><p>如果设备支持状态 PowerDeviceD2，则为 True。</p></td>
</tr>
<tr class="odd">
<td><p><a href="wakefromd0--wakefromd1--wakefromd2--and-wakefromd3.md" data-raw-source="[&lt;strong&gt;WakeFromD0&lt;/strong&gt;](wakefromd0--wakefromd1--wakefromd2--and-wakefromd3.md)"><strong>WakeFromD0</strong></a></p></td>
<td><p>如果设备可以从 PowerDeviceD0 唤醒，则为 True。</p></td>
</tr>
<tr class="even">
<td><p><a href="wakefromd0--wakefromd1--wakefromd2--and-wakefromd3.md" data-raw-source="[&lt;strong&gt;WakeFromD1&lt;/strong&gt;](wakefromd0--wakefromd1--wakefromd2--and-wakefromd3.md)"><strong>WakeFromD1</strong></a></p></td>
<td><p>如果设备可以从 PowerDeviceD1 唤醒，则为 True。</p></td>
</tr>
<tr class="odd">
<td><p><a href="wakefromd0--wakefromd1--wakefromd2--and-wakefromd3.md" data-raw-source="[&lt;strong&gt;WakeFromD2&lt;/strong&gt;](wakefromd0--wakefromd1--wakefromd2--and-wakefromd3.md)"><strong>WakeFromD2</strong></a></p></td>
<td><p>如果设备可以从 PowerDeviceD2 唤醒，则为 True。</p></td>
</tr>
<tr class="even">
<td><p><a href="wakefromd0--wakefromd1--wakefromd2--and-wakefromd3.md" data-raw-source="[&lt;strong&gt;WakeFromD3&lt;/strong&gt;](wakefromd0--wakefromd1--wakefromd2--and-wakefromd3.md)"><strong>WakeFromD3</strong></a></p></td>
<td><p>如果设备可以从 PowerDeviceD3 唤醒，则为 True。</p></td>
</tr>
<tr class="odd">
<td><p><a href="devicestate.md" data-raw-source="[&lt;strong&gt;DeviceState&lt;/strong&gt;](devicestate.md)"><strong>DeviceState</strong></a> [PowerSystemMaximum]</p></td>
<td><p>指定此设备可支持的每个系统电源状态的最高设备电源状态，从 PowerSystemUnspecified 到 PowerSystemShutdown。</p></td>
</tr>
<tr class="even">
<td><p><a href="systemwake.md" data-raw-source="[&lt;strong&gt;SystemWake&lt;/strong&gt;](systemwake.md)"><strong>SystemWake</strong></a></p></td>
<td><p>指定最低系统电源状态 (S0 到 S4) 可以从中唤醒系统。</p></td>
</tr>
<tr class="odd">
<td><p><a href="devicewake.md" data-raw-source="[&lt;strong&gt;DeviceWake&lt;/strong&gt;](devicewake.md)"><strong>DeviceWake</strong></a></p></td>
<td><p>指定设备可唤醒的最小设备电源状态 (D0 到 D3) 。</p></td>
</tr>
</tbody>
</table>

 

**DeviceWake**条目列出了设备可用于响应唤醒信号的最小设备电源状态。 值 PowerDeviceUnspecified 指示设备无法唤醒系统。 **SystemWake**条目列出了可从中唤醒系统的最低系统电源状态。 这些值基于父 devnode 的功能，驱动程序不应更改这些值。 有关详细信息，请参阅 [报表设备功能](reporting-device-power-capabilities.md)。

通常，如果满足以下条件，设备可以唤醒系统：

-   设备处于电源状态等于或大于 **DeviceWake** 值。

-   系统处于电源状态等于或大于 **SystemWake** 值。

 

