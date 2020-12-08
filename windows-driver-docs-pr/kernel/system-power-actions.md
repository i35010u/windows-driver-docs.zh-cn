---
title: 系统电源操作
description: 系统电源操作
keywords:
- 系统电源操作 WDK 电源管理
- 系统电源状态 WDK 内核，电源操作
- 电源操作 WDK 电源管理
- POWER_ACTION
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 77257c58035f8e31fc5c4a0bc08c99822e8edf4e
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96839229"
---
# <a name="system-power-actions"></a>系统电源操作





当电源管理器发送 IRP 来设置或查询系统电源状态时，它将指定系统电源状态以及提供有关电源状态更改信息的其他参数。 此参数传递到 **&gt; ShutdownType**，是电源 \_ 操作类型的枚举器。 枚举器反映了系统电源状态请求，如下表所示。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>POWER_ACTION 枚举器</th>
<th>请求的系统电源状态</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>PowerActionNone</strong></p></td>
<td><p>S0 或无系统电源 IRP 处于活动状态</p></td>
</tr>
<tr class="even">
<td><p><strong>PowerActionSleep</strong></p></td>
<td><p>S1、S2 或 S3</p></td>
</tr>
<tr class="odd">
<td><p><strong>PowerActionHibernate</strong></p></td>
<td><p>S4</p></td>
</tr>
<tr class="even">
<td><p>仅限 Microsoft Windows 2000 和更高版本的<strong>PowerActionShutdown</strong> () </p></td>
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

 

当驱动程序接收到用于 S5 的系统查询或设置电源 IRP 时，它可以查看 **ShutdownType** 以获取有关请求的关闭的详细信息。 当计算机重置而不是无限期关机时，驱动程序可以使用此信息优化其关闭顺序。 大多数设备的驱动程序在系统重置后仍保持开机。 但是，对于某些设备，如 (DMA) 执行直接内存访问的视频流式处理设备，驱动程序可能会选择在重置系统时关闭设备的电源，从而停止任何正在进行的 i/o。

当设备电源策略所有者将 *设备* 电源 irp 发送到其设备堆栈以响应系统电源 irp 时，驱动程序可以使用 **ShutdownType** 参数来获取有关当前 *系统* 电源 irp 的信息。 在这种情况下， **ShutdownType** 的值指示当前请求的系统电源状态，或者，如果系统请求未完成，则为 **PowerActionNone** 。 但是，如果设备 IRP 请求状态 D0，驱动程序不应依赖此信息。

在 Windows 98/Me 中，当 IRP 请求设备电源状态时，此成员始终包含 **PowerActionNone** 。

 

 




