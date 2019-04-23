---
title: OID_WDI_TASK_SCAN
description: OID_WDI_TASK_SCAN 请求 BSS 网络的一项调查。 该端口执行扫描根据 IEEE 802.11 规范的要求。
ms.assetid: c4131010-20f2-45a4-8fb9-5a1e3e9735e5
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 OID_WDI_TASK_SCAN 网络驱动程序
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: d7bf84cda2adbec918206cee5dfb3511cac1d75a
ms.sourcegitcommit: d17b4c61af620694ffa1c70a2dc9d308fd7e5b2e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/22/2019
ms.locfileid: "59902664"
---
# <a name="oidwditaskscan"></a>OID\_WDI\_TASK\_SCAN


OID\_WDI\_任务\_扫描请求的 BSS 网络调查。 该端口执行扫描根据 IEEE 802.11 规范的要求。

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th>Object</th>
<th>中止支持</th>
<th>默认优先级 （主机驱动程序策略）</th>
<th>正常执行时间 （秒）</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>端口</td>
<td>是。 端口必须保持干净状态后中止。</td>
<td><p>6 （背景扫描）</p>
<p>5 （用户启动的扫描）</p></td>
<td>4</td>
</tr>
</tbody>
</table>

 

消息包含启动任务[ **WDI\_TLV\_状态**](https://msdn.microsoft.com/library/windows/hardware/dn898068)指示端口启动扫描，并已准备好接收其他命令之后。

端口扫描启动后通过 LiveUpdatesNeeded 启用时，必须提供增量更新 (使用未经请求的迹象[NDIS\_状态\_WDI\_指示\_BSS\_条目\_列表](ndis-status-wdi-indication-bss-entry-list.md)) 有关发现的 BSS 条目。 端口不应报告 BSS 项以前已发现但找不到由端口当前扫描中。 出于能力和性能原因，端口应限制迹象，并将更新发送到主机，仅当它所发现 3 或更多，或它已发现不超过 3 个条目，但尚未报告它们所在的主机超过 500 毫秒。 扫描完成后，如果适配器不会管理 BSS 条目后，它不需要记住它所发现的 BSS 条目。 扫描操作完成后，端口必须将任务完成通知发送到操作系统，并停止向该主机进行报告 BSS 条目。 扫描命令用于查找旧版 （Wi-Fi Direct 网络） 和端口不应包含 Wi-Fi Direct 导致浏览器的探测请求中。

如果适配器不会管理 BSS 条目，主机会记住报告的有限的一段时间内扫描中的端口的 BSS 条目。 它超时时其缓存条目，并将它们刷新。 如果适配器管理的 BSS 条目，将其缓存然后会超时。主机可能会发送[OID\_WDI\_设置\_刷新\_BSS\_条目](oid-wdi-set-flush-bss-entry.md)命令显式刷新条目。

主机跟踪使用其 BSSID BSS 条目。 如果该端口的相同 BSSID 报告两个 BSS 条目，主机将覆盖其中一个与另一个。

扫描正在进行时，该端口必须维护现有连接 （例如，基础结构或 Wi-Fi Direct）。 如果连接已存在，该端口应扫描一次和子集之间通道的子集，提供对中的其他连接访问。 扫描期间，主机可以提交到该适配器上的任何端口的数据包发送请求。

在所指示的 BSS 条目中，该端口可以包含设备特定的上下文信息。 如果端口要求连接到该 BSS 条目，此上下文信息将传递回设备。 但是，此上下文可能会由主机自动清除如果刷新 BSS 条目。

可以终止扫描命令。 在接收时中止命令，该端口应停止尝试查找新 BSS 网络并尽可能快地完成扫描任务。 当完成任务后 （通常情况下或者由于中止） 时，该端口应为处于良好状态，这样，可以在该端口上发出另一个扫描。

执行一次扫描时，适配器必须不违反法规的限制。

## <a name="task-parameters"></a>任务参数


| TLV                                                                       | 允许多个 TLV 实例 | 可选 | 描述                                                                                                                                                                                                                                                                                   |
|---------------------------------------------------------------------------|--------------------------------|----------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [**WDI\_TLV\_BSSID**](https://msdn.microsoft.com/library/windows/hardware/dn926153)                             |                                |          | 要扫描的网络的 BSSID。 如果这是广播的 MAC 地址，工作站将扫描的所有 BSSIDs。                                                                                                                                                                                     |
| [**WDI\_TLV\_SSID**](https://msdn.microsoft.com/library/windows/hardware/dn898064)                               | X                              |          | 端口应扫描的 SSID 列表的列表。 此列表中可以有多个 Ssid 和其中一个可以是通配符。 执行操作时的通道上的 active 扫描，端口必须为列表中每个 SSID 发送探测请求。 如果此列表为空，该端口必须扫描的所有 Ssid。 |
| [**WDI\_TLV\_VENDOR\_SPECIFIC\_IE**](https://msdn.microsoft.com/library/windows/hardware/dn898076) |                                | X        | 必须包括在由端口发送的探测请求的一个或多个 Ie。 这些导致浏览器不用于被动扫描。                                                                                                                                                                        |
| [**WDI\_TLV\_SCAN\_MODE**](https://msdn.microsoft.com/library/windows/hardware/dn898052)                    |                                |          | 扫描模式参数。                                                                                                                                                                                                                                                                         |
| [**WDI\_TLV\_SCAN\_DWELL\_TIME**](https://msdn.microsoft.com/library/windows/hardware/dn898051)       |                                |          | 会仔细斟酌时间参数。                                                                                                                                                                                                                                                                        |
| [**WDI\_TLV\_BAND\_CHANNEL**](https://msdn.microsoft.com/library/windows/hardware/dn926144)              | X                              | X        | 建议的通道进行扫描的列表。 适配器可以对子集或超集通道列表执行扫描，只要它满足最长扫描时间要求。 如果此列表为空，该端口必须扫描所有受支持的通道上。                                               |

 

## <a name="task-completion-indication"></a>指示任务完成


[NDIS\_状态\_WDI\_指示\_扫描\_完成](ndis-status-wdi-indication-scan-complete.md)

## <a name="unsolicited-indication"></a>未经请求的指示

[NDIS\_状态\_WDI\_指示\_BSS\_条目\_列表](ndis-status-wdi-indication-bss-entry-list.md)

此通知由设备使用，需要了解的有关 BSS 条目更新主机。 可以在任何时候发送它。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>最低受支持的客户端</p></td>
<td><p>Windows 10</p></td>
</tr>
<tr class="even">
<td><p>最低受支持的服务器</p></td>
<td><p>Windows Server 2016</p></td>
</tr>
<tr class="odd">
<td><p>Header</p></td>
<td>Dot11wdi.h</td>
</tr>
</tbody>
</table>

 

 




