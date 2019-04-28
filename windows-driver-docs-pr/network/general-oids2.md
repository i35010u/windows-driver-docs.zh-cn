---
title: 常规 OID
description: 常规 OID
ms.assetid: fcd0e7fe-d1ab-4ec3-9c47-0bfb0ce63572
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 48c5b2899cbc974ea0c90d65bf9c4b93ffcdad5a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63349919"
---
# <a name="general-oids"></a>常规 OID





下表列出了适用于远程 NDIS 以太网设备的常规 Oid。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">支持</th>
<th align="left">OID</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>必需</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff569642" data-raw-source="[OID_GEN_SUPPORTED_LIST](https://msdn.microsoft.com/library/windows/hardware/ff569642)">OID_GEN_SUPPORTED_LIST</a></p></td>
<td align="left"><p>受支持的 Oid 的列表。</p></td>
</tr>
<tr class="even">
<td align="left"><p>必需</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff569585" data-raw-source="[OID_GEN_HARDWARE_STATUS](https://msdn.microsoft.com/library/windows/hardware/ff569585)">OID_GEN_HARDWARE_STATUS</a></p></td>
<td align="left"><p>硬件状态。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>必需</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff569609" data-raw-source="[OID_GEN_MEDIA_SUPPORTED](https://msdn.microsoft.com/library/windows/hardware/ff569609)">OID_GEN_MEDIA_SUPPORTED</a></p></td>
<td align="left"><p>支持的媒体类型 （编码）。</p></td>
</tr>
<tr class="even">
<td align="left"><p>必需</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff569607" data-raw-source="[OID_GEN_MEDIA_IN_USE](https://msdn.microsoft.com/library/windows/hardware/ff569607)">OID_GEN_MEDIA_IN_USE</a></p></td>
<td align="left"><p>在使用 （编码） 的媒体类型。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>必需</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff569598" data-raw-source="[OID_GEN_MAXIMUM_FRAME_SIZE](https://msdn.microsoft.com/library/windows/hardware/ff569598)">OID_GEN_MAXIMUM_FRAME_SIZE</a></p></td>
<td align="left"><p>以字节为单位的最大帧大小。</p></td>
</tr>
<tr class="even">
<td align="left"><p>必需</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff569593" data-raw-source="[OID_GEN_LINK_SPEED](https://msdn.microsoft.com/library/windows/hardware/ff569593)">OID_GEN_LINK_SPEED</a></p></td>
<td align="left"><p>链接速度为 100 bps 为单位。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>必需</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff569644" data-raw-source="[OID_GEN_TRANSMIT_BLOCK_SIZE](https://msdn.microsoft.com/library/windows/hardware/ff569644)">OID_GEN_TRANSMIT_BLOCK_SIZE</a></p></td>
<td align="left"><p>最小存储，以字节为单位，单个数据包中的 NIC 的传输缓冲区空间占用量</p></td>
</tr>
<tr class="even">
<td align="left"><p>必需</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff569633" data-raw-source="[OID_GEN_RECEIVE_BLOCK_SIZE](https://msdn.microsoft.com/library/windows/hardware/ff569633)">OID_GEN_RECEIVE_BLOCK_SIZE</a></p></td>
<td align="left"><p>存储，以字节为单位，单个数据包中的 NIC 的接收缓冲区空间占用量</p></td>
</tr>
<tr class="odd">
<td align="left"><p>必需</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff569651" data-raw-source="[OID_GEN_VENDOR_ID](https://msdn.microsoft.com/library/windows/hardware/ff569651)">OID_GEN_VENDOR_ID</a></p></td>
<td align="left"><p>供应商 NIC 代码。</p></td>
</tr>
<tr class="even">
<td align="left"><p>必需</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff569649" data-raw-source="[OID_GEN_VENDOR_DESCRIPTION](https://msdn.microsoft.com/library/windows/hardware/ff569649)">OID_GEN_VENDOR_DESCRIPTION</a></p></td>
<td align="left"><p>供应商网络卡说明。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>必需</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff569650" data-raw-source="[OID_GEN_VENDOR_DRIVER_VERSION](https://msdn.microsoft.com/library/windows/hardware/ff569650)">OID_GEN_VENDOR_DRIVER_VERSION</a></p></td>
<td align="left"><p>供应商分配驱动程序的版本号。</p></td>
</tr>
<tr class="even">
<td align="left"><p>必需</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff569575" data-raw-source="[OID_GEN_CURRENT_PACKET_FILTER](https://msdn.microsoft.com/library/windows/hardware/ff569575)">OID_GEN_CURRENT_PACKET_FILTER</a></p></td>
<td align="left"><p>当前数据包筛选器 （编码）。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>必需</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff569601" data-raw-source="[OID_GEN_MAXIMUM_TOTAL_SIZE](https://msdn.microsoft.com/library/windows/hardware/ff569601)">OID_GEN_MAXIMUM_TOTAL_SIZE</a></p></td>
<td align="left"><p>以字节为单位的最大的数据包总长度。</p></td>
</tr>
<tr class="even">
<td align="left"><p>可选</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff569639" data-raw-source="[OID_GEN_RNDIS_CONFIG_PARAMETER](https://msdn.microsoft.com/library/windows/hardware/ff569639)">OID_GEN_RNDIS_CONFIG_PARAMETER</a></p></td>
<td align="left"><p>特定于设备的配置参数 （仅设置）。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>可选</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff569621" data-raw-source="[OID_GEN_PHYSICAL_MEDIUM](https://msdn.microsoft.com/library/windows/hardware/ff569621)">OID_GEN_PHYSICAL_MEDIUM</a></p></td>
<td align="left"><p>有关基础物理介质的信息。</p></td>
</tr>
<tr class="even">
<td align="left"><p>必需</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff569604" data-raw-source="[OID_GEN_MEDIA_CONNECT_STATUS](https://msdn.microsoft.com/library/windows/hardware/ff569604)">OID_GEN_MEDIA_CONNECT_STATUS</a></p></td>
<td align="left"><p>NIC 的网络连接的状态。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>可选</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff569597" data-raw-source="[OID_GEN_MAC_OPTIONS](https://msdn.microsoft.com/library/windows/hardware/ff569597)">OID_GEN_MAC_OPTIONS</a></p></td>
<td align="left"><p>指定 NIC 的可选属性的位掩码 必须仅受支持的 Nic <a href="https://msdn.microsoft.com/library/windows/hardware/ff562331" data-raw-source="[802.1p packet priority](https://msdn.microsoft.com/library/windows/hardware/ff562331)">802.1p 数据包优先级</a>。</p></td>
</tr>
</tbody>
</table>

 

 

 





