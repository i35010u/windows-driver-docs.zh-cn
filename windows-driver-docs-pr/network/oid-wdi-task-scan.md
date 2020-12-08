---
title: OID_WDI_TASK_SCAN
description: OID_WDI_TASK_SCAN 请求对 BSS 网络的调查。 端口根据 IEEE 802.11 规范的要求执行扫描。
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 OID_WDI_TASK_SCAN 网络驱动程序
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 41e749308dc6a4ad0b815dc4c09be0df9f8ca1aa
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96829235"
---
# <a name="oid_wdi_task_scan"></a>OID \_ WDI \_ 任务 \_ 扫描


OID \_ WDI \_ 任务 \_ 扫描请求 BSS 网络调查。 端口根据 IEEE 802.11 规范的要求执行扫描。

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th>对象</th>
<th>支持中止</th>
<th>主机驱动程序策略 (默认优先级) </th>
<th>正常执行时间 (秒) </th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>端口</td>
<td>是的。 中止后，端口必须处于干净状态。</td>
<td><p>6 (后台扫描) </p>
<p>5 (用户启动的扫描) </p></td>
<td>4</td>
</tr>
</tbody>
</table>

 

当端口开始扫描并准备好接收其他命令时，将显示包含 [**WDI \_ TLV \_ 状态**](./wdi-tlv-status.md) 的任务已启动消息。

当 LiveUpdatesNeeded 启用扫描时，此端口必须提供增量更新 (使用) 有关发现的 BSS 条目的 [NDIS \_ 状态 \_ WDI \_ 指示 \_ BSS \_ 条目 \_ 列表](ndis-status-wdi-indication-bss-entry-list.md) 的未经请求的指示。 先前已发现但未被当前扫描中的端口找到的 BSS 条目不应由端口报告。 出于电源和性能方面的原因，此端口应限制指示并仅在发现3个或更多的情况下将更新发送到主机，或在发现小于3个条目，但未将其报告给主机超过500毫秒。 扫描完成后，如果适配器不管理 BSS 条目，则不需要记住已发现的 BSS 条目。 扫描操作完成后，端口必须将任务完成通知发送到操作系统，并停止向主机报告 BSS 条目。 Scan 命令用于查找旧版 (非 Wi-fi Direct 网络) ，端口不应在探测请求中包含 Wi-Fi 直接请求。

如果适配器未管理 BSS 条目，则主机会记下由端口报告的 BSS 项，并在有限的时间段内扫描。 它会超时其缓存条目并刷新它们。 如果适配器管理 BSS 条目，则会将其缓存并超时。宿主可以发送 [OID \_ WDI \_ SET \_ FLUSH \_ BSS \_ ENTRY](oid-wdi-set-flush-bss-entry.md) 命令，以显式刷新条目。

主机使用其 BSSID 跟踪 BSS 条目。 如果端口报告相同 BSSID 的两个 BSS 条目，则主机会覆盖另一个。

当扫描正在进行时，该端口必须保持现有连接 (例如，基础结构或 Wi-Fi 直接) 。 如果连接已存在，则该端口一次应扫描一小部分的频道，在子集之间，提供对介质的其他连接。 在扫描期间，主机可以将数据包发送请求提交到适配器上的任何端口。

在指示的 BSS 条目中，端口可能包含特定于设备的上下文信息。 如果要求端口连接到该 BSS 条目，则会将此上下文信息传递回设备。 但是，如果刷新了 BSS 条目，主机可能会自动清除此上下文。

Scan 命令可以中止。 收到 abort 命令后，端口应停止尝试查找新的 BSS 网络并尽快完成扫描任务。 如果任务已完成， (正常或由于中止) ，则端口应处于良好状态，以便可以在该端口上发出其他扫描。

在执行扫描时，适配器不得违反规章限制。

## <a name="task-parameters"></a>任务参数


| TLV                                                                       | 允许多个 TLV 实例 | 可选 | 说明                                                                                                                                                                                                                                                                                   |
|---------------------------------------------------------------------------|--------------------------------|----------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [**WDI \_ TLV \_ BSSID**](./wdi-tlv-bssid.md)                             |                                |          | 要扫描的网络的 BSSID。 如果这是广播 MAC 地址，工作站将扫描所有 BSSIDs。                                                                                                                                                                                     |
| [**WDI \_ TLV \_ SSID**](./wdi-tlv-ssid.md)                               | X                              |          | 端口应扫描的 SSID 列表。 此列表中可以有多个 Ssid，其中一个可以是通配符。 在通道上执行活动扫描时，端口必须为列表中的每个 SSID 发送探测请求。 如果此列表为空，则该端口必须扫描所有 Ssid。 |
| [**WDI \_ TLV \_ 供应商 \_ 特定 \_ IE**](./wdi-tlv-vendor-specific-ie.md) |                                | X        | 必须包含在端口发送的探测请求中的一个或多个传入。 它们不用于被动扫描。                                                                                                                                                                        |
| [**WDI \_ TLV \_ 扫描 \_ 模式**](./wdi-tlv-scan-mode.md)                    |                                |          | 扫描模式参数。                                                                                                                                                                                                                                                                         |
| [**WDI \_ TLV \_ 扫描 \_ 停留 \_ 时间**](./wdi-tlv-scan-dwell-time.md)       |                                |          | 停留时间参数。                                                                                                                                                                                                                                                                        |
| [**WDI \_ TLV \_ 波段 \_ 通道**](./wdi-tlv-band-channel.md)              | X                              | X        | 要扫描的推荐通道的列表。 适配器可以在通道列表的子集或超集上执行扫描，只要它满足最长扫描时间要求。 如果此列表为空，则端口必须扫描所有支持的通道。                                               |

 

## <a name="task-completion-indication"></a>任务完成指示


[NDIS \_ 状态 \_ WDI \_ 指示 \_ 扫描 \_ 完成](ndis-status-wdi-indication-scan-complete.md)

## <a name="unsolicited-indication"></a>未经请求的指示

[NDIS \_ 状态 \_ WDI \_ 指示 \_ BSS \_ 条目 \_ 列表](ndis-status-wdi-indication-bss-entry-list.md)

设备使用此通知来告知主机有关 BSS 项的更新。 随时可以发送。

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
<td><p>Windows Server 2016</p></td>
</tr>
<tr class="odd">
<td><p>标头</p></td>
<td>Dot11wdi</td>
</tr>
</tbody>
</table>

 

