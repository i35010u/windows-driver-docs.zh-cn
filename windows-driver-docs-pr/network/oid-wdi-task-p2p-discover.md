---
title: OID_WDI_TASK_P2P_DISCOVER
description: 将 OID_WDI_TASK_P2P_DISCOVER 颁发给设备，以执行 Wi-fi 直接发现。
ms.assetid: 9425a8d1-af68-488c-8a1e-a9b759f102cc
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 OID_WDI_TASK_P2P_DISCOVER 网络驱动程序
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 7ce130c0eaba2f2ef5fce2872543f490c9e85729
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89216145"
---
# <a name="oid_wdi_task_p2p_discover"></a>OID \_ WDI \_ 任务 \_ P2P \_ 发现


已将 OID \_ WDI \_ 任务 \_ P2P \_ 发现发送到设备，以便执行 wi-fi 直接发现。

| 对象 | 支持中止                                           | 主机驱动程序策略 (默认优先级)  | 正常执行时间 (秒)  |
|--------|---------------------------------------------------------|---------------------------------------|---------------------------------|
| 端口   | 是。 中止后，端口必须处于干净状态。 | 6                                     | 15                              |

 

此命令包含一些属性，这些属性定义要搜索的一组特定 Wi-fi Direct 设备，或通配符发现。

Wi-fi 直接发现与标准 Wi-fi 扫描相互排斥。 此任务正在运行时，不应发送广播探测请求，不应使用 "DIRECT" SSID 或特定的中转 SSID。 这些探测请求还必须包含所有必需的 Wi-fi Direct。

主机可能包含未作为任务参数的一部分提供给设备的搜索条件。 如果主机已满足所需的条件，则它可能会使用任务中止机制，因此，设备可以快速中止 Wi-fi 直接发现任务，以免降低方案性能。

如果任务已完成， (正常或由于中止) ，则端口应处于良好状态，以便可以在该端口上发出另一个发现请求。

## <a name="task-parameters"></a>任务参数


<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th>TLV</th>
<th>允许多个 TLV 实例</th>
<th>可选</th>
<th>说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><a href="https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-p2p-discover-mode" data-raw-source="[&lt;strong&gt;WDI_TLV_P2P_DISCOVER_MODE&lt;/strong&gt;](./wdi-tlv-p2p-discover-mode.md)"><strong>WDI_TLV_P2P_DISCOVER_MODE</strong></a></td>
<td></td>
<td></td>
<td>发现模式信息，如扫描类型、计数和扫描之间的时间。</td>
</tr>
<tr class="even">
<td><a href="https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-scan-dwell-time" data-raw-source="[&lt;strong&gt;WDI_TLV_SCAN_DWELL_TIME&lt;/strong&gt;](./wdi-tlv-scan-dwell-time.md)"><strong>WDI_TLV_SCAN_DWELL_TIME</strong></a></td>
<td></td>
<td></td>
<td>正在扫描停留时间设置。</td>
</tr>
<tr class="odd">
<td><a href="https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-p2p-discovery-channel-settings" data-raw-source="[&lt;strong&gt;WDI_TLV_P2P_DISCOVERY _CHANNEL_SETTINGS&lt;/strong&gt;](./wdi-tlv-p2p-discovery-channel-settings.md)"><strong>WDI_TLV_P2P_DISCOVERY _CHANNEL_SETTINGS</strong></a></td>
<td>X</td>
<td>X</td>
<td>扫描持续时间和要扫描的频道列表。 指定时，侦听设置将覆盖 WDI_TLV_SCAN_DWELL_TIME 中指定的设置。 如果此列表为空，则端口必须扫描所有支持的通道，并使用 WDI_TLV_SCAN_DWELL_TIME 中的 "侦听" 设置。</td>
</tr>
<tr class="even">
<td><a href="https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-ssid" data-raw-source="[&lt;strong&gt;WDI_TLV_SSID&lt;/strong&gt;](./wdi-tlv-ssid.md)"><strong>WDI_TLV_SSID</strong></a></td>
<td>X</td>
<td>X</td>
<td>端口应扫描的 Ssid 列表。 此列表中可以有多个 Ssid，其中一个可以是通配符。 在通道上执行活动扫描时，端口必须为列表中的每个 SSID 发送探测请求。 如果此列表为空，则该端口必须扫描所有 Ssid。</td>
</tr>
<tr class="odd">
<td><a href="https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-p2p-service-name-hash" data-raw-source="[&lt;strong&gt;WDI_TLV_P2P_SERVICE_NAME_HASH&lt;/strong&gt;](./wdi-tlv-p2p-service-name-hash.md)"><strong>WDI_TLV_P2P_SERVICE_NAME_HASH</strong></a></td>
<td>X</td>
<td>X</td>
<td>要查询的服务哈希名称的列表。 如果指定 WDI_P2P_SERVICE_DISCOVERY_TYPE_SERVICE_NAME_ONLY 或 WDI_P2P_SERVICE_DISCOVERY_TYPE_ASP2_SERVICE_NAME_ONLY，则为必需。</td>
</tr>
<tr class="even">
<td><a href="https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-vendor-specific-ie" data-raw-source="[&lt;strong&gt;WDI_TLV_VENDOR_SPECIFIC_IE&lt;/strong&gt;](./wdi-tlv-vendor-specific-ie.md)"><strong>WDI_TLV_VENDOR_SPECIFIC_IE</strong></a></td>
<td></td>
<td>X</td>
<td>必须包含在端口发送的探测请求中的一个或多个传入。 它们不用于被动扫描。</td>
</tr>
<tr class="odd">
<td><a href="https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-p2p-service-information-discovery-entry" data-raw-source="[&lt;strong&gt;WDI_TLV_P2P_SERVICE_INFORMATION_DISCOVERY_ENTRY&lt;/strong&gt;](./wdi-tlv-p2p-service-information-discovery-entry.md)"><strong>WDI_TLV_P2P_SERVICE_INFORMATION_DISCOVERY_ENTRY</strong></a></td>
<td>X</td>
<td>X</td>
<td>要查询的服务信息发现条目的可选列表。 如果指定 WDI_P2P_SERVICE_DISCOVERY_TYPE_SERVICE_INFORMATION，则这是必需的。 驱动程序应使用服务名称哈希通过探测请求/响应来执行 P2P 服务发现。 对于包含服务信息的每个服务项，驱动程序应执行 ANQP 查询请求/响应来查询服务信息。</td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-p2p-asp2-service-information-discovery-entry" data-raw-source="[&lt;strong&gt;WDI_TLV_P2P_ASP2_SERVICE_INFORMATION_DISCOVERY_ENTRY&lt;/strong&gt;](./wdi-tlv-p2p-asp2-service-information-discovery-entry.md)"><strong>WDI_TLV_P2P_ASP2_SERVICE_INFORMATION_DISCOVERY_ENTRY</strong></a></p></td>
<td>X</td>
<td><p>X</p></td>
<td><p>已在 Windows 10 版本1607、WDI 版本1.0.21 中添加。</p>
<p>要查询的 ASP2 服务信息发现条目的可选列表。 如果指定 WDI_P2P_SERVICE_DISCOVERY_TYPE_ASP2_SERVICE_INFORMATION，则这是必需的。 驱动程序应使用服务名称哈希通过探测请求/响应来执行 P2P 服务发现。 对于包含服务信息的每个服务项，驱动程序应执行 ANQP 查询请求/响应来查询服务信息。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-p2p-include-listen-channel" data-raw-source="[&lt;strong&gt;WDI_TLV_P2P_INCLUDE_LISTEN_CHANNEL&lt;/strong&gt;](./wdi-tlv-p2p-include-listen-channel.md)"><strong>WDI_TLV_P2P_INCLUDE_LISTEN_CHANNEL</strong></a></p></td>
<td></td>
<td><p>X</p></td>
<td><p>已在 Windows 10 版本1607、WDI 版本1.0.21 中添加。</p>
<p>指定在发现过程中，探测请求是否应包括侦听通道属性。</p></td>
</tr>
</tbody>
</table>

 

## <a name="task-completion-indication"></a>任务完成指示


[NDIS \_ 状态 \_ WDI \_ 指示 \_ P2P \_ 发现 \_ 完成](ndis-status-wdi-indication-p2p-discovery-complete.md)
## <a name="unsolicited-indication"></a>未经请求的指示


[NDIS \_ 状态 \_ WDI \_ 指示 \_ BSS \_ 条目 \_ 列表](ndis-status-wdi-indication-bss-entry-list.md)

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
<td><p>标头</p></td>
<td>Dot11wdi</td>
</tr>
</tbody>
</table>

 

