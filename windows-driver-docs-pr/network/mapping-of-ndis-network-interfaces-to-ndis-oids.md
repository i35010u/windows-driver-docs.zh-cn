---
title: 将 NDIS 网络接口映射到 NDIS OID
description: 将 NDIS 网络接口映射到 NDIS OID
ms.assetid: 117f94fd-829d-4ad8-be25-a6a90a8d4c50
keywords:
- NDIS 网络接口 WDK，映射
- 网络接口 WDK，映射
- Oid WDK 网络，网络接口
- OID 请求 WDK 网络
- 代理接口提供程序 WDK 网络
- NDIS 代理接口提供程序 WDK
- NDIS 网络接口
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 820928352b02693048ceef855bead5826abb5e21
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89215582"
---
# <a name="mapping-of-ndis-network-interfaces-to-ndis-oids"></a>将 NDIS 网络接口映射到 NDIS OID





为了响应 NDIS 接口对象请求，NDIS 接口提供程序可以缓存从基础驱动程序获取的信息，还可以发出 OID 请求以获取有关基础接口的信息。

作为代理接口提供程序，NDIS 通常会缓存它收到的有关微型端口适配器和筛选器模块的信息。 NDIS 代理接口提供程序使用缓存的信息来响应接口请求。 在某些情况下，NDIS 代理接口提供程序会发出 Oid 以获取接口的信息。 例如，NDIS 5 的接口信息的主要来源。*x* 及更早版本的驱动程序通过 OID 请求。 在 NDIS 6.0 驱动程序中，还有其他接口信息源，如 [**ndis \_ 重启 \_ 属性**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_restart_attributes) 和 [**ndis \_ 微型端口 \_ 适配器 \_ 常规 \_ 属性**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_adapter_general_attributes) 结构。 有关 Oid 中信息的替代源的详细信息，请参阅每个 OID 的参考页。

NDIS 代理接口提供程序还代表小型端口适配器和筛选器模块生成一些接口信息。 例如，NDIS (在 RFC 2863 *) 中生成* 一个接口别名，以响应 *ifAlias* 请求。 NDIS 定义了其他 Oid 来从 NDIS 接口提供程序获取此类信息。 例如， [OID \_ GEN \_ ALIAS](./oid-gen-alias.md) 允许接口提供程序指定 *ifAlias* 对象。 此类 Oid 特定于接口提供程序，从不用于从其他 NDIS 驱动程序获取信息。

除了特定于接口提供程序的 Oid 以外，接口提供程序还必须支持 NDIS 可用于获取接口信息的其他 NDIS Oid。 NDIS 可以向提供程序颁发这些 Oid，提供程序可以颁发这些 Oid （如有必要）从基础接口中收集信息。

**注意**   NDIS 定义 RFC 2863 中未包含的其他统计信息。 有关将 NDIS 支持的所有接口统计信息映射到 Oid 的列表，请参阅 [**NDIS \_ 接口 \_ 信息**](/windows/desktop/api/ifdef/ns-ifdef-_ndis_interface_information) 结构的成员。 本主题中的表为尝试将规范与 NDIS 实现相关的读取器定义为 RFC 2863 规范中定义的统计信息进行了映射。

 

下表显示了从管理信息库 (MIB) 中定义的对象到 NDIS 6.0 Oid 的映射，以及 NDIS 可能用于从 NDIS 5 获取信息的 Oid。*x* 及更早版本的驱动程序。 该表还包括一些未定义为 MIB 对象的其他接口对象。 接口对象还对应于与[OID \_ GEN \_ 接口 \_ ](./oid-gen-interface-info.md)信息 OID 关联的[**NDIS \_ 接口 \_ 信息**](ndis-interface-information.md)结构中的成员。

**注意**   用星号标记的表中的 NDIS 6.0 Oid (\*) 前缀特定于接口提供程序。 其他 NDIS 6.0 Oid 可以颁发给接口提供程序和其他 NDIS 驱动程序。

 

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">接口 MIB 值</th>
<th align="left">NDIS 6.0 Oid</th>
<th align="left">NDIS 1.x 和更早的 Oid</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><em>ifAdminStatus</em></p></td>
<td align="left"><p>* <a href="https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-admin-status" data-raw-source="[OID_GEN_ADMIN_STATUS](./oid-gen-admin-status.md)">OID_GEN_ADMIN_STATUS</a></p></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><p><em>ifAlias</em></p></td>
<td align="left"><p>* <a href="https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-alias" data-raw-source="[OID_GEN_ALIAS](./oid-gen-alias.md)">OID_GEN_ALIAS</a></p></td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><p><em>ifCounterDiscontinuityTime</em></p></td>
<td align="left"><p>* <a href="https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-discontinuity-time" data-raw-source="[OID_GEN_DISCONTINUITY_TIME](./oid-gen-discontinuity-time.md)">OID_GEN_DISCONTINUITY_TIME</a></p></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><p><em>ifHCInBroadcastPkts</em></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-broadcast-frames-rcv" data-raw-source="[OID_GEN_BROADCAST_FRAMES_RCV](./oid-gen-broadcast-frames-rcv.md)">OID_GEN_BROADCAST_FRAMES_RCV</a></p></td>
<td align="left"><p>OID_GEN_BROADCAST_FRAMES_RCV</p></td>
</tr>
<tr class="odd">
<td align="left"><p><em>ifHCInMulticastPkts</em></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-multicast-frames-rcv" data-raw-source="[OID_GEN_MULTICAST_FRAMES_RCV](./oid-gen-multicast-frames-rcv.md)">OID_GEN_MULTICAST_FRAMES_RCV</a></p></td>
<td align="left"><p>OID_GEN_MULTICAST_FRAMES_RCV</p></td>
</tr>
<tr class="even">
<td align="left"><p><em>ifHCInOctets</em></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-bytes-rcv" data-raw-source="[OID_GEN_BYTES_RCV](./oid-gen-bytes-rcv.md)">OID_GEN_BYTES_RCV</a></p></td>
<td align="left"><p>NDIS 添加这些 Oid 的结果，从 NDIS 5 收集 <em>ifHCInOctets</em> 值。<em>x</em> 驱动程序：</p>
<p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-directed-bytes-rcv" data-raw-source="[OID_GEN_DIRECTED_BYTES_RCV](./oid-gen-directed-bytes-rcv.md)">OID_GEN_DIRECTED_BYTES_RCV</a>+</p>
<p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-multicast-bytes-rcv" data-raw-source="[OID_GEN_MULTICAST_BYTES_RCV](./oid-gen-multicast-bytes-rcv.md)">OID_GEN_MULTICAST_BYTES_RCV</a>+</p>
<p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-broadcast-bytes-rcv" data-raw-source="[OID_GEN_BROADCAST_BYTES_RCV](./oid-gen-broadcast-bytes-rcv.md)">OID_GEN_BROADCAST_BYTES_RCV</a></p>
<p>NDIS 6.0 接口提供程序还应支持这些 Oid。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><em>ifHCInUcastPkts</em></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-directed-frames-rcv" data-raw-source="[OID_GEN_DIRECTED_FRAMES_RCV](./oid-gen-directed-frames-rcv.md)">OID_GEN_DIRECTED_FRAMES_RCV</a></p></td>
<td align="left"><p>OID_GEN_DIRECTED_FRAMES_RCV</p></td>
</tr>
<tr class="even">
<td align="left"><p><em>ifHCOutBroadcastPkts</em></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-broadcast-frames-xmit" data-raw-source="[OID_GEN_BROADCAST_FRAMES_XMIT](./oid-gen-broadcast-frames-xmit.md)">OID_GEN_BROADCAST_FRAMES_XMIT</a></p></td>
<td align="left"><p>OID_GEN_BROADCAST_FRAMES_XMIT</p></td>
</tr>
<tr class="odd">
<td align="left"><p><em>ifHCOutMulticastPkts</em></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-multicast-frames-xmit" data-raw-source="[OID_GEN_MULTICAST_FRAMES_XMIT](./oid-gen-multicast-frames-xmit.md)">OID_GEN_MULTICAST_FRAMES_XMIT</a></p></td>
<td align="left"><p>OID_GEN_MULTICAST_FRAMES_XMIT</p></td>
</tr>
<tr class="even">
<td align="left"><p><em>ifHCOutOctets</em></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-bytes-xmit" data-raw-source="[OID_GEN_BYTES_XMIT](./oid-gen-bytes-xmit.md)">OID_GEN_BYTES_XMIT</a></p></td>
<td align="left"><p>NDIS 添加这些 Oid 的结果，从 NDIS 5 收集 <em>ifHCInOctets</em> 值。<em>x</em> 驱动程序：</p>
<p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-directed-bytes-xmit" data-raw-source="[OID_GEN_DIRECTED_BYTES_XMIT](./oid-gen-directed-bytes-xmit.md)">OID_GEN_DIRECTED_BYTES_XMIT</a>+</p>
<p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-multicast-bytes-xmit" data-raw-source="[OID_GEN_MULTICAST_BYTES_XMIT](./oid-gen-multicast-bytes-xmit.md)">OID_GEN_MULTICAST_BYTES_XMIT</a>+</p>
<p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-broadcast-bytes-xmit" data-raw-source="[OID_GEN_BROADCAST_BYTES_XMIT](./oid-gen-broadcast-bytes-xmit.md)">OID_GEN_BROADCAST_BYTES_XMIT</a></p>
<p>NDIS 6.0 接口提供程序还应支持这些 Oid。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><em>ifHCOutUCastPkts</em></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-directed-frames-xmit" data-raw-source="[OID_GEN_DIRECTED_FRAMES_XMIT](./oid-gen-directed-frames-xmit.md)">OID_GEN_DIRECTED_FRAMES_XMIT</a></p></td>
<td align="left"><p>OID_GEN_DIRECTED_FRAMES_XMIT</p></td>
</tr>
<tr class="even">
<td align="left"><p><em>ifHighSpeed</em></p></td>
<td align="left"><p>* <a href="https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-link-speed-ex" data-raw-source="[OID_GEN_LINK_SPEED_EX](./oid-gen-link-speed-ex.md)">OID_GEN_LINK_SPEED_EX</a>、* <a href="https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-xmit-link-speed" data-raw-source="[OID_GEN_XMIT_LINK_SPEED](./oid-gen-xmit-link-speed.md)">OID_GEN_XMIT_LINK_SPEED</a>、* <a href="https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-rcv-link-speed" data-raw-source="[OID_GEN_RCV_LINK_SPEED](./oid-gen-rcv-link-speed.md)">OID_GEN_RCV_LINK_SPEED</a></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-link-speed" data-raw-source="[OID_GEN_LINK_SPEED](./oid-gen-link-speed.md)">OID_GEN_LINK_SPEED</a></p></td>
</tr>
<tr class="odd">
<td align="left"><p><em>ifInDiscards</em></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-rcv-discards" data-raw-source="[OID_GEN_RCV_DISCARDS](./oid-gen-rcv-discards.md)">OID_GEN_RCV_DISCARDS</a></p></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><p><em>ifInErrors</em></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-rcv-error" data-raw-source="[OID_GEN_RCV_ERROR](./oid-gen-rcv-error.md)">OID_GEN_RCV_ERROR</a></p></td>
<td align="left"><p>OID_GEN_RCV_ERROR</p></td>
</tr>
<tr class="odd">
<td align="left"><p><em>ifLastChange</em></p></td>
<td align="left"><p>* <a href="https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-last-change" data-raw-source="[OID_GEN_LAST_CHANGE](./oid-gen-last-change.md)">OID_GEN_LAST_CHANGE</a></p></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><p><em>ifMtu</em></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-maximum-frame-size" data-raw-source="[OID_GEN_MAXIMUM_FRAME_SIZE](./oid-gen-maximum-frame-size.md)">OID_GEN_MAXIMUM_FRAME_SIZE</a></p></td>
<td align="left"><p>OID_GEN_MAXIMUM_FRAME_SIZE</p></td>
</tr>
<tr class="odd">
<td align="left"><p><em>ifOperStatus</em></p></td>
<td align="left"><p>* <a href="https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-operational-status" data-raw-source="[OID_GEN_OPERATIONAL_STATUS](./oid-gen-operational-status.md)">OID_GEN_OPERATIONAL_STATUS</a></p></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><p><em>ifOutDiscards</em></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-xmit-discards" data-raw-source="[OID_GEN_XMIT_DISCARDS](./oid-gen-xmit-discards.md)">OID_GEN_XMIT_DISCARDS</a></p></td>
<td align="left"><p>OID_GEN_XMIT_DISCARDS</p></td>
</tr>
<tr class="odd">
<td align="left"><p><em>ifOutErrors</em></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-xmit-error" data-raw-source="[OID_GEN_XMIT_ERROR](./oid-gen-xmit-error.md)">OID_GEN_XMIT_ERROR</a></p></td>
<td align="left"><p>OID_GEN_XMIT_ERROR</p></td>
</tr>
<tr class="even">
<td align="left"><p><em>ifPhysAddress</em></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/oid-802-3-current-address" data-raw-source="[OID_802_3_CURRENT_ADDRESS](./oid-802-3-current-address.md)">OID_802_3_CURRENT_ADDRESS</a></p></td>
<td align="left"><p>OID_802_3_CURRENT_ADDRESS</p></td>
</tr>
<tr class="odd">
<td align="left"><p><em>ifPromiscuousMode</em></p></td>
<td align="left"><p>* <a href="https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-promiscuous-mode" data-raw-source="[OID_GEN_PROMISCUOUS_MODE](./oid-gen-promiscuous-mode.md)">OID_GEN_PROMISCUOUS_MODE</a></p></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><p>不适用</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/oid-802-3-permanent-address" data-raw-source="[OID_802_3_PERMANENT_ADDRESS](./oid-802-3-permanent-address.md)">OID_802_3_PERMANENT_ADDRESS</a></p></td>
<td align="left"><p>OID_802_3_PERMANENT_ADDRESS</p></td>
</tr>
<tr class="odd">
<td align="left"><p>不适用</p></td>
<td align="left"><p>* <a href="https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-interface-info" data-raw-source="[OID_GEN_INTERFACE_INFO](./oid-gen-interface-info.md)">OID_GEN_INTERFACE_INFO</a></p></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><p>不适用</p></td>
<td align="left"><p>* <a href="https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-media-connect-status-ex" data-raw-source="[OID_GEN_MEDIA_CONNECT_STATUS_EX](./oid-gen-media-connect-status-ex.md)">OID_GEN_MEDIA_CONNECT_STATUS_EX</a></p></td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><p>不适用</p></td>
<td align="left"><p>* <a href="https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-media-duplex-state" data-raw-source="[OID_GEN_MEDIA_DUPLEX_STATE](./oid-gen-media-duplex-state.md)">OID_GEN_MEDIA_DUPLEX_STATE</a></p></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><p>不适用</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-statistics" data-raw-source="[OID_GEN_STATISTICS](./oid-gen-statistics.md)">OID_GEN_STATISTICS</a></p></td>
<td align="left"></td>
</tr>
</tbody>
</table>

 

 

