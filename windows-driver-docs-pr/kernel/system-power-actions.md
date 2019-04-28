---
title: 系统电源操作
description: 系统电源操作
ms.assetid: e8ab99d4-c18d-4ba8-bfe8-8eebb881c384
keywords:
- 系统电源操作 WDK 电源管理
- 系统电源状态 WDK 内核，电源操作
- 电源操作 WDK 电源管理
- POWER_ACTION
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: cea2bcdfd67fe50f4a505e3cb23622b72d6a5eec
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63345431"
---
# <a name="system-power-actions"></a>系统电源操作





电源管理器发送 IRP 来设置或查询的系统电源状态，它指定以及一个附加参数，它提供了有关电源状态更改信息的系统电源状态。 在此参数传递**Irp-&gt;Parameters.Power.ShutdownType**，是一个枚举器的强大功能\_操作类型。 下表中所示的枚举器特点是系统电源状态请求。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>POWER_ACTION 枚举器</th>
<th>所请求的系统电源状态</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>PowerActionNone</strong></p></td>
<td><p>S0 或没有系统电源 IRP 活动</p></td>
</tr>
<tr class="even">
<td><p><strong>PowerActionSleep</strong></p></td>
<td><p>S1、 S2 或 S3</p></td>
</tr>
<tr class="odd">
<td><p><strong>PowerActionHibernate</strong></p></td>
<td><p>S4</p></td>
</tr>
<tr class="even">
<td><p><strong>PowerActionShutdown</strong> （Microsoft Windows 2000 和更高的系统）</p></td>
<td><p>S5</p></td>
</tr>
<tr class="odd">
<td><p><strong>PowerActionShutdownReset</strong></p></td>
<td><p>S5</p></td>
</tr>
<tr class="even">
<td><p><strong>PowerActionShutdownOff</strong></p></td>
<td><p>S5</p></td>
</tr>
</tbody>
</table>

 

当驱动程序收到的 S5 系统查询或集 power IRP 时，它可以检查**ShutdownType**请求关闭有关详细信息。 驱动程序可以使用此信息时在计算机正在重置而不无限期地关闭电源优化其关闭序列。 系统将重置时，大多数设备的驱动程序将保留 power。 但是，对于某些设备，如视频流执行直接内存访问 (DMA) 的设备驱动程序可能会选择关闭其设备的电源系统重置时，因此停止任何正在运行的 I/O。

当设备电源策略所有者发送*设备*IRP 的 power 为响应系统电源 IRP 其设备堆栈，驱动程序可以使用**ShutdownType**参数，以获取有关当前信息*系统*power IRP。 在本示例中的值**ShutdownType**指示当前请求的系统电源状态，或者它是**PowerActionNone**如果系统请求不是未完成。 驱动程序不应，但是，依赖此信息如果设备 IRP 请求状态 D0。

在 Windows 98 / 我来说，此成员始终包含**PowerActionNone** IRP 当请求设备电源状态。

 

 




