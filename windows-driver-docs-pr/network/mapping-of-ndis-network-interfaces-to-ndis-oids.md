---
title: 将 NDIS 网络接口映射到 NDIS OID
description: 将 NDIS 网络接口映射到 NDIS OID
ms.assetid: 117f94fd-829d-4ad8-be25-a6a90a8d4c50
keywords:
- NDIS 网络接口 WDK 和映射
- 网络接口 WDK 和映射
- Oid WDK 网络，网络接口
- OID 请求 WDK 网络
- 代理接口提供程序 WDK 网络
- NDIS 代理接口提供程序 WDK
- NDIS 网络接口
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3889228d9d5f13372f2443661bcccec210c0d977
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67387293"
---
# <a name="mapping-of-ndis-network-interfaces-to-ndis-oids"></a>将 NDIS 网络接口映射到 NDIS OID





若要响应的 NDIS 接口对象请求时，NDIS 接口提供程序可以缓存它们从基础驱动程序中获取，并还可以颁发 OID 请求以获取有关基础接口的信息的信息。

为代理接口提供程序，NDIS 通常会缓存它接收有关微型端口适配器和筛选器模块信息。 NDIS 代理接口提供程序使用缓存的信息，如果需要，对接口请求作出响应。 在某些情况下，NDIS 代理接口提供程序颁发 Oid，若要获取的接口的信息。 例如，主要的 NDIS 5 的接口信息来源。*x*早期驱动程序是通过 OID 请求。 NDIS 6.0 驱动程序中有额外的源接口的信息，如[ **NDIS\_重新启动\_特性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_restart_attributes)并[ **NDIS\_微型端口\_适配器\_常规\_特性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_miniport_adapter_general_attributes)结构。 有关 Oid 中信息的备用源的详细信息，请参阅为每个 OID 的参考页。

NDIS 代理接口提供程序还会生成代表微型端口适配器和筛选器模块的一些接口信息。 例如，NDIS 生成接口别名 (*ifAlias*在 RFC 2863) 以响应*ifAlias*请求。 NDIS 定义其他 Oid 从 NDIS 接口提供程序获取此类信息。 例如， [OID\_代\_别名](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-alias)允许指定的接口提供*ifAlias*对象。 此类 Oid 是特定于接口提供程序，永远不会用于从其他的 NDIS 驱动程序中获取信息。

除了特定于接口提供程序的 Oid，接口提供程序必须支持其他 NDIS 可用于获取接口的信息的 NDIS Oid。 NDIS 可以发出这些 Oid 到提供程序和提供程序可以发出这些 Oid，如有必要，若要从基础接口收集的信息。

**请注意**  NDIS 定义不包含在 RFC 2863 的更多统计信息。 将所有的 NDIS 支持接口统计信息映射到 Oid 的列表，请参阅的成员[ **NDIS\_界面\_信息**](https://docs.microsoft.com/windows/desktop/api/ifdef/ns-ifdef-_ndis_interface_information)结构。 本主题中的表定义的统计信息的读取器的尝试与的 NDIS 实现规范 RFC 2863 规范中定义的映射。

 

下表显示了从管理信息基础 (MIB) 到 NDIS 6.0 Oid 和 NDIS 可能使用 NDIS 5 中获取信息的 Oid 中定义的对象的映射。*x*和早期驱动程序。 该表还包括一些未定义为 MIB 对象的其他接口对象。 界面对象也对应中的成员[ **NDIS\_界面\_信息**](ndis-interface-information.md)与关联的结构[OID\_代\_界面\_信息](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-interface-info)OID。

**请注意**  NDIS 6.0 Oid 表中以星号标记 (\*) 前缀是特定于接口提供程序。 其他 NDIS 6.0 Oid 可以颁发给接口提供程序和其他 NDIS 驱动程序。

 

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">接口的 MIB 值</th>
<th align="left">NDIS 6.0 Oid</th>
<th align="left">NDIS 5.x 和早期的 Oid</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><em>ifAdminStatus</em></p></td>
<td align="left"><p>* <a href="https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-admin-status" data-raw-source="[OID_GEN_ADMIN_STATUS](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-admin-status)">OID_GEN_ADMIN_STATUS</a></p></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><p><em>ifAlias</em></p></td>
<td align="left"><p>* <a href="https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-alias" data-raw-source="[OID_GEN_ALIAS](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-alias)">OID_GEN_ALIAS</a></p></td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><p><em>ifCounterDiscontinuityTime</em></p></td>
<td align="left"><p>* <a href="https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-discontinuity-time" data-raw-source="[OID_GEN_DISCONTINUITY_TIME](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-discontinuity-time)">OID_GEN_DISCONTINUITY_TIME</a></p></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><p><em>ifHCInBroadcastPkts</em></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-broadcast-frames-rcv" data-raw-source="[OID_GEN_BROADCAST_FRAMES_RCV](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-broadcast-frames-rcv)">OID_GEN_BROADCAST_FRAMES_RCV</a></p></td>
<td align="left"><p>OID_GEN_BROADCAST_FRAMES_RCV</p></td>
</tr>
<tr class="odd">
<td align="left"><p><em>ifHCInMulticastPkts</em></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-multicast-frames-rcv" data-raw-source="[OID_GEN_MULTICAST_FRAMES_RCV](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-multicast-frames-rcv)">OID_GEN_MULTICAST_FRAMES_RCV</a></p></td>
<td align="left"><p>OID_GEN_MULTICAST_FRAMES_RCV</p></td>
</tr>
<tr class="even">
<td align="left"><p><em>ifHCInOctets</em></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-bytes-rcv" data-raw-source="[OID_GEN_BYTES_RCV](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-bytes-rcv)">OID_GEN_BYTES_RCV</a></p></td>
<td align="left"><p>NDIS 将结果添加从这些 Oid 来收集<em>ifHCInOctets</em>从 NDIS 5 的值。<em>x</em>驱动程序：</p>
<p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-directed-bytes-rcv" data-raw-source="[OID_GEN_DIRECTED_BYTES_RCV](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-directed-bytes-rcv)">OID_GEN_DIRECTED_BYTES_RCV</a>+</p>
<p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-multicast-bytes-rcv" data-raw-source="[OID_GEN_MULTICAST_BYTES_RCV](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-multicast-bytes-rcv)">OID_GEN_MULTICAST_BYTES_RCV</a>+</p>
<p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-broadcast-bytes-rcv" data-raw-source="[OID_GEN_BROADCAST_BYTES_RCV](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-broadcast-bytes-rcv)">OID_GEN_BROADCAST_BYTES_RCV</a></p>
<p>NDIS 6.0 接口提供程序还应支持这些 Oid。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><em>ifHCInUcastPkts</em></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-directed-frames-rcv" data-raw-source="[OID_GEN_DIRECTED_FRAMES_RCV](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-directed-frames-rcv)">OID_GEN_DIRECTED_FRAMES_RCV</a></p></td>
<td align="left"><p>OID_GEN_DIRECTED_FRAMES_RCV</p></td>
</tr>
<tr class="even">
<td align="left"><p><em>ifHCOutBroadcastPkts</em></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-broadcast-frames-xmit" data-raw-source="[OID_GEN_BROADCAST_FRAMES_XMIT](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-broadcast-frames-xmit)">OID_GEN_BROADCAST_FRAMES_XMIT</a></p></td>
<td align="left"><p>OID_GEN_BROADCAST_FRAMES_XMIT</p></td>
</tr>
<tr class="odd">
<td align="left"><p><em>ifHCOutMulticastPkts</em></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-multicast-frames-xmit" data-raw-source="[OID_GEN_MULTICAST_FRAMES_XMIT](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-multicast-frames-xmit)">OID_GEN_MULTICAST_FRAMES_XMIT</a></p></td>
<td align="left"><p>OID_GEN_MULTICAST_FRAMES_XMIT</p></td>
</tr>
<tr class="even">
<td align="left"><p><em>ifHCOutOctets</em></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-bytes-xmit" data-raw-source="[OID_GEN_BYTES_XMIT](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-bytes-xmit)">OID_GEN_BYTES_XMIT</a></p></td>
<td align="left"><p>NDIS 将结果添加从这些 Oid 来收集<em>ifHCInOctets</em>从 NDIS 5 的值。<em>x</em>驱动程序：</p>
<p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-directed-bytes-xmit" data-raw-source="[OID_GEN_DIRECTED_BYTES_XMIT](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-directed-bytes-xmit)">OID_GEN_DIRECTED_BYTES_XMIT</a>+</p>
<p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-multicast-bytes-xmit" data-raw-source="[OID_GEN_MULTICAST_BYTES_XMIT](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-multicast-bytes-xmit)">OID_GEN_MULTICAST_BYTES_XMIT</a>+</p>
<p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-broadcast-bytes-xmit" data-raw-source="[OID_GEN_BROADCAST_BYTES_XMIT](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-broadcast-bytes-xmit)">OID_GEN_BROADCAST_BYTES_XMIT</a></p>
<p>NDIS 6.0 接口提供程序还应支持这些 Oid。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><em>ifHCOutUCastPkts</em></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-directed-frames-xmit" data-raw-source="[OID_GEN_DIRECTED_FRAMES_XMIT](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-directed-frames-xmit)">OID_GEN_DIRECTED_FRAMES_XMIT</a></p></td>
<td align="left"><p>OID_GEN_DIRECTED_FRAMES_XMIT</p></td>
</tr>
<tr class="even">
<td align="left"><p><em>ifHighSpeed</em></p></td>
<td align="left"><p>* <a href="https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-link-speed-ex" data-raw-source="[OID_GEN_LINK_SPEED_EX](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-link-speed-ex)">OID_GEN_LINK_SPEED_EX</a>, * <a href="https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-xmit-link-speed" data-raw-source="[OID_GEN_XMIT_LINK_SPEED](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-xmit-link-speed)">OID_GEN_XMIT_LINK_SPEED</a>, * <a href="https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-rcv-link-speed" data-raw-source="[OID_GEN_RCV_LINK_SPEED](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-rcv-link-speed)">OID_GEN_RCV_LINK_SPEED</a></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-link-speed" data-raw-source="[OID_GEN_LINK_SPEED](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-link-speed)">OID_GEN_LINK_SPEED</a></p></td>
</tr>
<tr class="odd">
<td align="left"><p><em>ifInDiscards</em></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-rcv-discards" data-raw-source="[OID_GEN_RCV_DISCARDS](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-rcv-discards)">OID_GEN_RCV_DISCARDS</a></p></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><p><em>ifInErrors</em></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-rcv-error" data-raw-source="[OID_GEN_RCV_ERROR](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-rcv-error)">OID_GEN_RCV_ERROR</a></p></td>
<td align="left"><p>OID_GEN_RCV_ERROR</p></td>
</tr>
<tr class="odd">
<td align="left"><p><em>ifLastChange</em></p></td>
<td align="left"><p>* <a href="https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-last-change" data-raw-source="[OID_GEN_LAST_CHANGE](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-last-change)">OID_GEN_LAST_CHANGE</a></p></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><p><em>ifMtu</em></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-maximum-frame-size" data-raw-source="[OID_GEN_MAXIMUM_FRAME_SIZE](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-maximum-frame-size)">OID_GEN_MAXIMUM_FRAME_SIZE</a></p></td>
<td align="left"><p>OID_GEN_MAXIMUM_FRAME_SIZE</p></td>
</tr>
<tr class="odd">
<td align="left"><p><em>ifOperStatus</em></p></td>
<td align="left"><p>* <a href="https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-operational-status" data-raw-source="[OID_GEN_OPERATIONAL_STATUS](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-operational-status)">OID_GEN_OPERATIONAL_STATUS</a></p></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><p><em>ifOutDiscards</em></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-xmit-discards" data-raw-source="[OID_GEN_XMIT_DISCARDS](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-xmit-discards)">OID_GEN_XMIT_DISCARDS</a></p></td>
<td align="left"><p>OID_GEN_XMIT_DISCARDS</p></td>
</tr>
<tr class="odd">
<td align="left"><p><em>ifOutErrors</em></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-xmit-error" data-raw-source="[OID_GEN_XMIT_ERROR](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-xmit-error)">OID_GEN_XMIT_ERROR</a></p></td>
<td align="left"><p>OID_GEN_XMIT_ERROR</p></td>
</tr>
<tr class="even">
<td align="left"><p><em>ifPhysAddress</em></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/oid-802-3-current-address" data-raw-source="[OID_802_3_CURRENT_ADDRESS](https://docs.microsoft.com/windows-hardware/drivers/network/oid-802-3-current-address)">OID_802_3_CURRENT_ADDRESS</a></p></td>
<td align="left"><p>OID_802_3_CURRENT_ADDRESS</p></td>
</tr>
<tr class="odd">
<td align="left"><p><em>ifPromiscuousMode</em></p></td>
<td align="left"><p>* <a href="https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-promiscuous-mode" data-raw-source="[OID_GEN_PROMISCUOUS_MODE](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-promiscuous-mode)">OID_GEN_PROMISCUOUS_MODE</a></p></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><p>不适用</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/oid-802-3-permanent-address" data-raw-source="[OID_802_3_PERMANENT_ADDRESS](https://docs.microsoft.com/windows-hardware/drivers/network/oid-802-3-permanent-address)">OID_802_3_PERMANENT_ADDRESS</a></p></td>
<td align="left"><p>OID_802_3_PERMANENT_ADDRESS</p></td>
</tr>
<tr class="odd">
<td align="left"><p>不适用</p></td>
<td align="left"><p>* <a href="https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-interface-info" data-raw-source="[OID_GEN_INTERFACE_INFO](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-interface-info)">OID_GEN_INTERFACE_INFO</a></p></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><p>不适用</p></td>
<td align="left"><p>* <a href="https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-media-connect-status-ex" data-raw-source="[OID_GEN_MEDIA_CONNECT_STATUS_EX](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-media-connect-status-ex)">OID_GEN_MEDIA_CONNECT_STATUS_EX</a></p></td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><p>不适用</p></td>
<td align="left"><p>* <a href="https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-media-duplex-state" data-raw-source="[OID_GEN_MEDIA_DUPLEX_STATE](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-media-duplex-state)">OID_GEN_MEDIA_DUPLEX_STATE</a></p></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><p>不适用</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-statistics" data-raw-source="[OID_GEN_STATISTICS](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-statistics)">OID_GEN_STATISTICS</a></p></td>
<td align="left"></td>
</tr>
</tbody>
</table>

 

 

 





