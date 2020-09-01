---
title: 常规 OID
description: 常规 OID
ms.assetid: fcd0e7fe-d1ab-4ec3-9c47-0bfb0ce63572
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c9db27f697ebe1bfb1269aacf24a71c66f7c067e
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89212459"
---
# <a name="general-oids"></a>常规 OID





下表列出了远程 NDIS 以太网设备的常规 Oid。

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
<th align="left">说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>必须</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-supported-list" data-raw-source="[OID_GEN_SUPPORTED_LIST](./oid-gen-supported-list.md)">OID_GEN_SUPPORTED_LIST</a></p></td>
<td align="left"><p>支持的 Oid 列表。</p></td>
</tr>
<tr class="even">
<td align="left"><p>必须</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-hardware-status" data-raw-source="[OID_GEN_HARDWARE_STATUS](./oid-gen-hardware-status.md)">OID_GEN_HARDWARE_STATUS</a></p></td>
<td align="left"><p>硬件状态。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>必须</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-media-supported" data-raw-source="[OID_GEN_MEDIA_SUPPORTED](./oid-gen-media-supported.md)">OID_GEN_MEDIA_SUPPORTED</a></p></td>
<td align="left"><p>支持 (编码) 的媒体类型。</p></td>
</tr>
<tr class="even">
<td align="left"><p>必须</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-media-in-use" data-raw-source="[OID_GEN_MEDIA_IN_USE](./oid-gen-media-in-use.md)">OID_GEN_MEDIA_IN_USE</a></p></td>
<td align="left"><p> (编码) 使用的媒体类型。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>必须</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-maximum-frame-size" data-raw-source="[OID_GEN_MAXIMUM_FRAME_SIZE](./oid-gen-maximum-frame-size.md)">OID_GEN_MAXIMUM_FRAME_SIZE</a></p></td>
<td align="left"><p>帧大小的最大值（字节）。</p></td>
</tr>
<tr class="even">
<td align="left"><p>必须</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-link-speed" data-raw-source="[OID_GEN_LINK_SPEED](./oid-gen-link-speed.md)">OID_GEN_LINK_SPEED</a></p></td>
<td align="left"><p>以 100 bps 为单位的链接速度。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>必须</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-transmit-block-size" data-raw-source="[OID_GEN_TRANSMIT_BLOCK_SIZE](./oid-gen-transmit-block-size.md)">OID_GEN_TRANSMIT_BLOCK_SIZE</a></p></td>
<td align="left"><p>单个数据包在 NIC 的传输缓冲区空间中占据的最小存储量（以字节为单位）。</p></td>
</tr>
<tr class="even">
<td align="left"><p>必须</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-receive-block-size" data-raw-source="[OID_GEN_RECEIVE_BLOCK_SIZE](./oid-gen-receive-block-size.md)">OID_GEN_RECEIVE_BLOCK_SIZE</a></p></td>
<td align="left"><p>单个数据包在 NIC 的接收缓冲区空间中占据的存储量（以字节为单位）。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>必须</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-vendor-id" data-raw-source="[OID_GEN_VENDOR_ID](./oid-gen-vendor-id.md)">OID_GEN_VENDOR_ID</a></p></td>
<td align="left"><p>供应商 NIC 代码。</p></td>
</tr>
<tr class="even">
<td align="left"><p>必须</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-vendor-description" data-raw-source="[OID_GEN_VENDOR_DESCRIPTION](./oid-gen-vendor-description.md)">OID_GEN_VENDOR_DESCRIPTION</a></p></td>
<td align="left"><p>供应商网卡说明。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>必须</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-vendor-driver-version" data-raw-source="[OID_GEN_VENDOR_DRIVER_VERSION](./oid-gen-vendor-driver-version.md)">OID_GEN_VENDOR_DRIVER_VERSION</a></p></td>
<td align="left"><p>供应商分配的驱动程序的版本号。</p></td>
</tr>
<tr class="even">
<td align="left"><p>必须</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-current-packet-filter" data-raw-source="[OID_GEN_CURRENT_PACKET_FILTER](./oid-gen-current-packet-filter.md)">OID_GEN_CURRENT_PACKET_FILTER</a></p></td>
<td align="left"><p>当前数据包筛选器 (编码) 。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>必须</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-maximum-total-size" data-raw-source="[OID_GEN_MAXIMUM_TOTAL_SIZE](./oid-gen-maximum-total-size.md)">OID_GEN_MAXIMUM_TOTAL_SIZE</a></p></td>
<td align="left"><p>最大数据包总长度（以字节为单位）。</p></td>
</tr>
<tr class="even">
<td align="left"><p>可选</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-rndis-config-parameter" data-raw-source="[OID_GEN_RNDIS_CONFIG_PARAMETER](./oid-gen-rndis-config-parameter.md)">OID_GEN_RNDIS_CONFIG_PARAMETER</a></p></td>
<td align="left"><p>设备特定的配置参数 (仅) 设置。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>可选</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-physical-medium" data-raw-source="[OID_GEN_PHYSICAL_MEDIUM](./oid-gen-physical-medium.md)">OID_GEN_PHYSICAL_MEDIUM</a></p></td>
<td align="left"><p>有关基础物理介质的信息。</p></td>
</tr>
<tr class="even">
<td align="left"><p>必须</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-media-connect-status" data-raw-source="[OID_GEN_MEDIA_CONNECT_STATUS](./oid-gen-media-connect-status.md)">OID_GEN_MEDIA_CONNECT_STATUS</a></p></td>
<td align="left"><p>NIC 网络连接的状态。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>可选</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-mac-options" data-raw-source="[OID_GEN_MAC_OPTIONS](./oid-gen-mac-options.md)">OID_GEN_MAC_OPTIONS</a></p></td>
<td align="left"><p>指定 NIC 的可选属性的位掩码。 必须仅支持支持 <a href="https://docs.microsoft.com/previous-versions/windows/hardware/network/ff562331(v=vs.85)" data-raw-source="[802.1p packet priority](/previous-versions/windows/hardware/network/ff562331(v=vs.85))">802.1 p 数据包优先级</a>的 nic。</p></td>
</tr>
</tbody>
</table>

 

 

