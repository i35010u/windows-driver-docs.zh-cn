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
ms.openlocfilehash: da61c06f09580ab717d81dd18cf67708b10ab083
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63343511"
---
# <a name="mapping-of-ndis-network-interfaces-to-ndis-oids"></a>将 NDIS 网络接口映射到 NDIS OID





若要响应的 NDIS 接口对象请求时，NDIS 接口提供程序可以缓存它们从基础驱动程序中获取，并还可以颁发 OID 请求以获取有关基础接口的信息的信息。

为代理接口提供程序，NDIS 通常会缓存它接收有关微型端口适配器和筛选器模块信息。 NDIS 代理接口提供程序使用缓存的信息，如果需要，对接口请求作出响应。 在某些情况下，NDIS 代理接口提供程序颁发 Oid，若要获取的接口的信息。 例如，主要的 NDIS 5 的接口信息来源。*x*早期驱动程序是通过 OID 请求。 NDIS 6.0 驱动程序中有额外的源接口的信息，如[ **NDIS\_重新启动\_特性**](https://msdn.microsoft.com/library/windows/hardware/ff567255)并[ **NDIS\_微型端口\_适配器\_常规\_特性**](https://msdn.microsoft.com/library/windows/hardware/ff565923)结构。 有关 Oid 中信息的备用源的详细信息，请参阅为每个 OID 的参考页。

NDIS 代理接口提供程序还会生成代表微型端口适配器和筛选器模块的一些接口信息。 例如，NDIS 生成接口别名 (*ifAlias*在 RFC 2863) 以响应*ifAlias*请求。 NDIS 定义其他 Oid 从 NDIS 接口提供程序获取此类信息。 例如， [OID\_代\_别名](https://msdn.microsoft.com/library/windows/hardware/ff569438)允许指定的接口提供*ifAlias*对象。 此类 Oid 是特定于接口提供程序，永远不会用于从其他的 NDIS 驱动程序中获取信息。

除了特定于接口提供程序的 Oid，接口提供程序必须支持其他 NDIS 可用于获取接口的信息的 NDIS Oid。 NDIS 可以发出这些 Oid 到提供程序和提供程序可以发出这些 Oid，如有必要，若要从基础接口收集的信息。

**请注意**  NDIS 定义不包含在 RFC 2863 的更多统计信息。 将所有的 NDIS 支持接口统计信息映射到 Oid 的列表，请参阅的成员[ **NDIS\_界面\_信息**](https://msdn.microsoft.com/library/windows/hardware/ff565736)结构。 本主题中的表定义的统计信息的读取器的尝试与的 NDIS 实现规范 RFC 2863 规范中定义的映射。

 

下表显示了从管理信息基础 (MIB) 到 NDIS 6.0 Oid 和 NDIS 可能使用 NDIS 5 中获取信息的 Oid 中定义的对象的映射。*x*和早期驱动程序。 该表还包括一些未定义为 MIB 对象的其他接口对象。 界面对象也对应中的成员[ **NDIS\_界面\_信息**](ndis-interface-information.md)与关联的结构[OID\_代\_界面\_信息](https://msdn.microsoft.com/library/windows/hardware/ff569589)OID。

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
<td align="left"><p>* <a href="https://msdn.microsoft.com/library/windows/hardware/ff569437" data-raw-source="[OID_GEN_ADMIN_STATUS](https://msdn.microsoft.com/library/windows/hardware/ff569437)">OID_GEN_ADMIN_STATUS</a></p></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><p><em>ifAlias</em></p></td>
<td align="left"><p>* <a href="https://msdn.microsoft.com/library/windows/hardware/ff569438" data-raw-source="[OID_GEN_ALIAS](https://msdn.microsoft.com/library/windows/hardware/ff569438)">OID_GEN_ALIAS</a></p></td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><p><em>ifCounterDiscontinuityTime</em></p></td>
<td align="left"><p>* <a href="https://msdn.microsoft.com/library/windows/hardware/ff569581" data-raw-source="[OID_GEN_DISCONTINUITY_TIME](https://msdn.microsoft.com/library/windows/hardware/ff569581)">OID_GEN_DISCONTINUITY_TIME</a></p></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><p><em>ifHCInBroadcastPkts</em></p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff569441" data-raw-source="[OID_GEN_BROADCAST_FRAMES_RCV](https://msdn.microsoft.com/library/windows/hardware/ff569441)">OID_GEN_BROADCAST_FRAMES_RCV</a></p></td>
<td align="left"><p>OID_GEN_BROADCAST_FRAMES_RCV</p></td>
</tr>
<tr class="odd">
<td align="left"><p><em>ifHCInMulticastPkts</em></p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff569613" data-raw-source="[OID_GEN_MULTICAST_FRAMES_RCV](https://msdn.microsoft.com/library/windows/hardware/ff569613)">OID_GEN_MULTICAST_FRAMES_RCV</a></p></td>
<td align="left"><p>OID_GEN_MULTICAST_FRAMES_RCV</p></td>
</tr>
<tr class="even">
<td align="left"><p><em>ifHCInOctets</em></p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff569443" data-raw-source="[OID_GEN_BYTES_RCV](https://msdn.microsoft.com/library/windows/hardware/ff569443)">OID_GEN_BYTES_RCV</a></p></td>
<td align="left"><p>NDIS 将结果添加从这些 Oid 来收集<em>ifHCInOctets</em>从 NDIS 5 的值。<em>x</em>驱动程序：</p>
<p><a href="https://msdn.microsoft.com/library/windows/hardware/ff569577" data-raw-source="[OID_GEN_DIRECTED_BYTES_RCV](https://msdn.microsoft.com/library/windows/hardware/ff569577)">OID_GEN_DIRECTED_BYTES_RCV</a>+</p>
<p><a href="https://msdn.microsoft.com/library/windows/hardware/ff569611" data-raw-source="[OID_GEN_MULTICAST_BYTES_RCV](https://msdn.microsoft.com/library/windows/hardware/ff569611)">OID_GEN_MULTICAST_BYTES_RCV</a>+</p>
<p><a href="https://msdn.microsoft.com/library/windows/hardware/ff569439" data-raw-source="[OID_GEN_BROADCAST_BYTES_RCV](https://msdn.microsoft.com/library/windows/hardware/ff569439)">OID_GEN_BROADCAST_BYTES_RCV</a></p>
<p>NDIS 6.0 接口提供程序还应支持这些 Oid。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><em>ifHCInUcastPkts</em></p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff569579" data-raw-source="[OID_GEN_DIRECTED_FRAMES_RCV](https://msdn.microsoft.com/library/windows/hardware/ff569579)">OID_GEN_DIRECTED_FRAMES_RCV</a></p></td>
<td align="left"><p>OID_GEN_DIRECTED_FRAMES_RCV</p></td>
</tr>
<tr class="even">
<td align="left"><p><em>ifHCOutBroadcastPkts</em></p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff569442" data-raw-source="[OID_GEN_BROADCAST_FRAMES_XMIT](https://msdn.microsoft.com/library/windows/hardware/ff569442)">OID_GEN_BROADCAST_FRAMES_XMIT</a></p></td>
<td align="left"><p>OID_GEN_BROADCAST_FRAMES_XMIT</p></td>
</tr>
<tr class="odd">
<td align="left"><p><em>ifHCOutMulticastPkts</em></p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff569614" data-raw-source="[OID_GEN_MULTICAST_FRAMES_XMIT](https://msdn.microsoft.com/library/windows/hardware/ff569614)">OID_GEN_MULTICAST_FRAMES_XMIT</a></p></td>
<td align="left"><p>OID_GEN_MULTICAST_FRAMES_XMIT</p></td>
</tr>
<tr class="even">
<td align="left"><p><em>ifHCOutOctets</em></p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff569445" data-raw-source="[OID_GEN_BYTES_XMIT](https://msdn.microsoft.com/library/windows/hardware/ff569445)">OID_GEN_BYTES_XMIT</a></p></td>
<td align="left"><p>NDIS 将结果添加从这些 Oid 来收集<em>ifHCInOctets</em>从 NDIS 5 的值。<em>x</em>驱动程序：</p>
<p><a href="https://msdn.microsoft.com/library/windows/hardware/ff569578" data-raw-source="[OID_GEN_DIRECTED_BYTES_XMIT](https://msdn.microsoft.com/library/windows/hardware/ff569578)">OID_GEN_DIRECTED_BYTES_XMIT</a>+</p>
<p><a href="https://msdn.microsoft.com/library/windows/hardware/ff569612" data-raw-source="[OID_GEN_MULTICAST_BYTES_XMIT](https://msdn.microsoft.com/library/windows/hardware/ff569612)">OID_GEN_MULTICAST_BYTES_XMIT</a>+</p>
<p><a href="https://msdn.microsoft.com/library/windows/hardware/ff569440" data-raw-source="[OID_GEN_BROADCAST_BYTES_XMIT](https://msdn.microsoft.com/library/windows/hardware/ff569440)">OID_GEN_BROADCAST_BYTES_XMIT</a></p>
<p>NDIS 6.0 接口提供程序还应支持这些 Oid。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><em>ifHCOutUCastPkts</em></p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff569580" data-raw-source="[OID_GEN_DIRECTED_FRAMES_XMIT](https://msdn.microsoft.com/library/windows/hardware/ff569580)">OID_GEN_DIRECTED_FRAMES_XMIT</a></p></td>
<td align="left"><p>OID_GEN_DIRECTED_FRAMES_XMIT</p></td>
</tr>
<tr class="even">
<td align="left"><p><em>ifHighSpeed</em></p></td>
<td align="left"><p>* <a href="https://msdn.microsoft.com/library/windows/hardware/ff569594" data-raw-source="[OID_GEN_LINK_SPEED_EX](https://msdn.microsoft.com/library/windows/hardware/ff569594)">OID_GEN_LINK_SPEED_EX</a>, * <a href="https://msdn.microsoft.com/library/windows/hardware/ff569655" data-raw-source="[OID_GEN_XMIT_LINK_SPEED](https://msdn.microsoft.com/library/windows/hardware/ff569655)">OID_GEN_XMIT_LINK_SPEED</a>, * <a href="https://msdn.microsoft.com/library/windows/hardware/ff569630" data-raw-source="[OID_GEN_RCV_LINK_SPEED](https://msdn.microsoft.com/library/windows/hardware/ff569630)">OID_GEN_RCV_LINK_SPEED</a></p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff569593" data-raw-source="[OID_GEN_LINK_SPEED](https://msdn.microsoft.com/library/windows/hardware/ff569593)">OID_GEN_LINK_SPEED</a></p></td>
</tr>
<tr class="odd">
<td align="left"><p><em>ifInDiscards</em></p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff569628" data-raw-source="[OID_GEN_RCV_DISCARDS](https://msdn.microsoft.com/library/windows/hardware/ff569628)">OID_GEN_RCV_DISCARDS</a></p></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><p><em>ifInErrors</em></p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff569629" data-raw-source="[OID_GEN_RCV_ERROR](https://msdn.microsoft.com/library/windows/hardware/ff569629)">OID_GEN_RCV_ERROR</a></p></td>
<td align="left"><p>OID_GEN_RCV_ERROR</p></td>
</tr>
<tr class="odd">
<td align="left"><p><em>ifLastChange</em></p></td>
<td align="left"><p>* <a href="https://msdn.microsoft.com/library/windows/hardware/ff569591" data-raw-source="[OID_GEN_LAST_CHANGE](https://msdn.microsoft.com/library/windows/hardware/ff569591)">OID_GEN_LAST_CHANGE</a></p></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><p><em>ifMtu</em></p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff569598" data-raw-source="[OID_GEN_MAXIMUM_FRAME_SIZE](https://msdn.microsoft.com/library/windows/hardware/ff569598)">OID_GEN_MAXIMUM_FRAME_SIZE</a></p></td>
<td align="left"><p>OID_GEN_MAXIMUM_FRAME_SIZE</p></td>
</tr>
<tr class="odd">
<td align="left"><p><em>ifOperStatus</em></p></td>
<td align="left"><p>* <a href="https://msdn.microsoft.com/library/windows/hardware/ff569619" data-raw-source="[OID_GEN_OPERATIONAL_STATUS](https://msdn.microsoft.com/library/windows/hardware/ff569619)">OID_GEN_OPERATIONAL_STATUS</a></p></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><p><em>ifOutDiscards</em></p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff569653" data-raw-source="[OID_GEN_XMIT_DISCARDS](https://msdn.microsoft.com/library/windows/hardware/ff569653)">OID_GEN_XMIT_DISCARDS</a></p></td>
<td align="left"><p>OID_GEN_XMIT_DISCARDS</p></td>
</tr>
<tr class="odd">
<td align="left"><p><em>ifOutErrors</em></p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff569654" data-raw-source="[OID_GEN_XMIT_ERROR](https://msdn.microsoft.com/library/windows/hardware/ff569654)">OID_GEN_XMIT_ERROR</a></p></td>
<td align="left"><p>OID_GEN_XMIT_ERROR</p></td>
</tr>
<tr class="even">
<td align="left"><p><em>ifPhysAddress</em></p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff569069" data-raw-source="[OID_802_3_CURRENT_ADDRESS](https://msdn.microsoft.com/library/windows/hardware/ff569069)">OID_802_3_CURRENT_ADDRESS</a></p></td>
<td align="left"><p>OID_802_3_CURRENT_ADDRESS</p></td>
</tr>
<tr class="odd">
<td align="left"><p><em>ifPromiscuousMode</em></p></td>
<td align="left"><p>* <a href="https://msdn.microsoft.com/library/windows/hardware/ff569625" data-raw-source="[OID_GEN_PROMISCUOUS_MODE](https://msdn.microsoft.com/library/windows/hardware/ff569625)">OID_GEN_PROMISCUOUS_MODE</a></p></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><p>不适用</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff569074" data-raw-source="[OID_802_3_PERMANENT_ADDRESS](https://msdn.microsoft.com/library/windows/hardware/ff569074)">OID_802_3_PERMANENT_ADDRESS</a></p></td>
<td align="left"><p>OID_802_3_PERMANENT_ADDRESS</p></td>
</tr>
<tr class="odd">
<td align="left"><p>不适用</p></td>
<td align="left"><p>* <a href="https://msdn.microsoft.com/library/windows/hardware/ff569589" data-raw-source="[OID_GEN_INTERFACE_INFO](https://msdn.microsoft.com/library/windows/hardware/ff569589)">OID_GEN_INTERFACE_INFO</a></p></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><p>不适用</p></td>
<td align="left"><p>* <a href="https://msdn.microsoft.com/library/windows/hardware/ff569605" data-raw-source="[OID_GEN_MEDIA_CONNECT_STATUS_EX](https://msdn.microsoft.com/library/windows/hardware/ff569605)">OID_GEN_MEDIA_CONNECT_STATUS_EX</a></p></td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><p>不适用</p></td>
<td align="left"><p>* <a href="https://msdn.microsoft.com/library/windows/hardware/ff569606" data-raw-source="[OID_GEN_MEDIA_DUPLEX_STATE](https://msdn.microsoft.com/library/windows/hardware/ff569606)">OID_GEN_MEDIA_DUPLEX_STATE</a></p></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><p>不适用</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff569640" data-raw-source="[OID_GEN_STATISTICS](https://msdn.microsoft.com/library/windows/hardware/ff569640)">OID_GEN_STATISTICS</a></p></td>
<td align="left"></td>
</tr>
</tbody>
</table>

 

 

 





