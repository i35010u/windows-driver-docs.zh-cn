---
title: OID_WDI_TASK_P2P_DISCOVER
description: OID_WDI_TASK_P2P_DISCOVER 颁发给设备执行 Wi-Fi Direct 发现。
ms.assetid: 9425a8d1-af68-488c-8a1e-a9b759f102cc
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 OID_WDI_TASK_P2P_DISCOVER 网络驱动程序
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 1252f2fa12cd227c3c860ced7444488f4af9ee4b
ms.sourcegitcommit: d17b4c61af620694ffa1c70a2dc9d308fd7e5b2e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/22/2019
ms.locfileid: "59902377"
---
# <a name="oidwditaskp2pdiscover"></a>OID\_WDI\_TASK\_P2P\_DISCOVER


OID\_WDI\_任务\_P2P\_发现颁发给设备执行 Wi-Fi Direct 发现。

| Object | 中止支持                                           | 默认优先级 （主机驱动程序策略） | 正常执行时间 （秒） |
|--------|---------------------------------------------------------|---------------------------------------|---------------------------------|
| 端口   | 是。 端口必须保持干净状态后中止。 | 6                                     | 15                              |

 

该命令包含属性的定义是一组特定的 Wi-Fi Direct 设备要搜索或通配符发现。

Wi-Fi Direct 发现是从标准的 Wi-fi 扫描互相排斥。 运行此任务时，应不会无需"直接-"SSID 或特定的转 SSID 发送广播的探测请求。 这些探测请求还必须包括所有必要 Wi-Fi Direct 导致浏览器。

主机可能有不到设备的任务参数的一部分提供的搜索条件。 主机可能会使用任务中止机制，它具有与所需的条件相匹配，因此很重要，设备可以快速中止 Wi-Fi Direct 发现任务以免降低方案的性能。

当完成任务后 （通常情况下或者由于中止） 时，该端口应为处于良好状态，这样，可以在该端口上发出另一个发现请求。

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
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><a href="https://msdn.microsoft.com/library/windows/hardware/dn897878" data-raw-source="[&lt;strong&gt;WDI_TLV_P2P_DISCOVER_MODE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/dn897878)"><strong>WDI_TLV_P2P_DISCOVER_MODE</strong></a></td>
<td></td>
<td></td>
<td>发现模式的信息，例如扫描类型、 计数和扫描之间的时间。</td>
</tr>
<tr class="even">
<td><a href="https://msdn.microsoft.com/library/windows/hardware/dn898051" data-raw-source="[&lt;strong&gt;WDI_TLV_SCAN_DWELL_TIME&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/dn898051)"><strong>WDI_TLV_SCAN_DWELL_TIME</strong></a></td>
<td></td>
<td></td>
<td>正在扫描停留时间设置。</td>
</tr>
<tr class="odd">
<td><a href="https://msdn.microsoft.com/library/windows/hardware/dn897877" data-raw-source="[&lt;strong&gt;WDI_TLV_P2P_DISCOVERY _CHANNEL_SETTINGS&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/dn897877)"><strong>WDI_TLV_P2P_DISCOVERY _CHANNEL_SETTINGS</strong></a></td>
<td>X</td>
<td>X</td>
<td>扫描持续时间和要扫描的频道的列表。 如果指定，侦听设置重写 WDI_TLV_SCAN_DWELL_TIME 中指定的。 如果此列表为空，该端口必须扫描所有受支持的通道，并使用 WDI_TLV_SCAN_DWELL_TIME 中的侦听设置。</td>
</tr>
<tr class="even">
<td><a href="https://msdn.microsoft.com/library/windows/hardware/dn898064" data-raw-source="[&lt;strong&gt;WDI_TLV_SSID&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/dn898064)"><strong>WDI_TLV_SSID</strong></a></td>
<td>X</td>
<td>X</td>
<td>端口应扫描的 Ssid 列表。 此列表中可以有多个 Ssid 和其中一个可以是通配符。 执行操作时的通道上的 active 扫描，端口必须为列表中每个 SSID 发送探测请求。 如果此列表为空，该端口必须扫描的所有 Ssid。</td>
</tr>
<tr class="odd">
<td><a href="https://msdn.microsoft.com/library/windows/hardware/dn898009" data-raw-source="[&lt;strong&gt;WDI_TLV_P2P_SERVICE_NAME_HASH&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/dn898009)"><strong>WDI_TLV_P2P_SERVICE_NAME_HASH</strong></a></td>
<td>X</td>
<td>X</td>
<td>要查询的服务哈希名称的列表。 如果指定 WDI_P2P_SERVICE_DISCOVERY_TYPE_SERVICE_NAME_ONLY 或 WDI_P2P_SERVICE_DISCOVERY_TYPE_ASP2_SERVICE_NAME_ONLY 被必需。</td>
</tr>
<tr class="even">
<td><a href="https://msdn.microsoft.com/library/windows/hardware/dn898076" data-raw-source="[&lt;strong&gt;WDI_TLV_VENDOR_SPECIFIC_IE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/dn898076)"><strong>WDI_TLV_VENDOR_SPECIFIC_IE</strong></a></td>
<td></td>
<td>X</td>
<td>必须包括在由端口发送的探测请求的一个或多个 Ie。 这些导致浏览器不用于被动扫描。</td>
</tr>
<tr class="odd">
<td><a href="https://msdn.microsoft.com/library/windows/hardware/mt269140" data-raw-source="[&lt;strong&gt;WDI_TLV_P2P_SERVICE_INFORMATION_DISCOVERY_ENTRY&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/mt269140)"><strong>WDI_TLV_P2P_SERVICE_INFORMATION_DISCOVERY_ENTRY</strong></a></td>
<td>X</td>
<td>X</td>
<td>服务信息发现项要查询的可选列表。 如果指定 WDI_P2P_SERVICE_DISCOVERY_TYPE_SERVICE_INFORMATION，这是必需的。 该驱动程序应通过使用服务名称哈希的探测请求/响应执行 P2P 服务发现。 对于每个包含服务的信息的服务条目，该驱动程序应执行 ANQP 查询请求/响应来查询服务的信息。</td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/mt769912" data-raw-source="[&lt;strong&gt;WDI_TLV_P2P_ASP2_SERVICE_INFORMATION_DISCOVERY_ENTRY&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/mt769912)"><strong>WDI_TLV_P2P_ASP2_SERVICE_INFORMATION_DISCOVERY_ENTRY</strong></a></p></td>
<td>X</td>
<td><p>X</p></td>
<td><p>在 Windows 10，版本 1607，WDI 版本 1.0.21 中添加。</p>
<p>ASP2 服务信息发现项要查询的可选列表。 如果指定 WDI_P2P_SERVICE_DISCOVERY_TYPE_ASP2_SERVICE_INFORMATION，这是必需的。 该驱动程序应通过使用服务名称哈希的探测请求/响应执行 P2P 服务发现。 对于每个包含服务的信息的服务条目，该驱动程序应执行 ANQP 查询请求/响应来查询服务的信息。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/mt769913" data-raw-source="[&lt;strong&gt;WDI_TLV_P2P_INCLUDE_LISTEN_CHANNEL&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/mt769913)"><strong>WDI_TLV_P2P_INCLUDE_LISTEN_CHANNEL</strong></a></p></td>
<td></td>
<td><p>X</p></td>
<td><p>在 Windows 10，版本 1607，WDI 版本 1.0.21 中添加。</p>
<p>指定的探测请求是否应包含在发现期间的侦听通道属性。</p></td>
</tr>
</tbody>
</table>

 

## <a name="task-completion-indication"></a>指示任务完成


[NDIS\_状态\_WDI\_指示\_P2P\_发现\_完成](ndis-status-wdi-indication-p2p-discovery-complete.md)
## <a name="unsolicited-indication"></a>未经请求的指示


[NDIS\_状态\_WDI\_指示\_BSS\_条目\_列表](ndis-status-wdi-indication-bss-entry-list.md)

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

 

 




