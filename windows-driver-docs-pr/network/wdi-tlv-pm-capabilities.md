---
title: 'WDI_TLV_PM_CAPABILITIES (0x42) '
description: WDI_TLV_PM_CAPABILITIES 是包含电源管理功能的 TLV。
ms.assetid: DE8A5333-BE2B-4CBB-8C75-45ABBE35A635
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_PM_CAPABILITIES (0x42) 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: ffa71d0854dc93cf64188c0eddc0458e2e1b4067
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89217195"
---
# <a name="wdi_tlv_pm_capabilities-0x42"></a>WDI \_ TLV \_ PM \_ 功能 (0x42) 


WDI \_ tlv \_ PM \_ 功能是包含电源管理功能的 tlv。

## <a name="tlv-type"></a>TLV 类型


0x42

## <a name="length"></a>Length


Sum (所有包含的元素的大小) 。

## <a name="values"></a>值


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>类型</th>
<th>说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>UINT32</td>
<td>指定电源管理支持的标志。
<p>有效标志为：</p>
<ul>
<li>NDIS_PM_WAKE_PACKET_INDICATION_SUPPORTED</li>
<li>NDIS_PM_SELECTIVE_SUSPEND_SUPPORTED (0x00000002) </li>
</ul></td>
</tr>
<tr class="even">
<td>UINT32</td>
<td>指定受支持的 LAN 唤醒模式。
<p>有效模式为：</p>
<ul>
<li> (0x00000001) NDIS_PM_WOL_BITMAP_PATTERN_SUPPORTED</li>
<li>NDIS_PM_WOL_MAGIC_PACKET_SUPPORTED (0x00000002) </li>
<li>NDIS_PM_WOL_IPV4_TCP_SYN_SUPPORTED (0x00000004) </li>
<li>NDIS_PM_WOL_IPV6_TCP_SYN_SUPPORTED (0x00000008) </li>
<li>NDIS_PM_WOL_IPV4_DEST_ADDR_WILDCARD_SUPPORTED (0x00000200) </li>
<li>NDIS_PM_WOL_IPV6_DEST_ADDR_WILDCARD_SUPPORTED (0x00000800) </li>
<li>NDIS_PM_WOL_EAPOL_REQUEST_ID_MESSAGE_SUPPORTED (0x00010000) </li>
</ul></td>
</tr>
<tr class="odd">
<td>UINT32</td>
<td>指定 LAN 唤醒模式的总数。</td>
</tr>
<tr class="even">
<td>UINT32</td>
<td>指定最大 LAN 唤醒模式大小。</td>
</tr>
<tr class="odd">
<td>UINT32</td>
<td>指定最大 LAN 唤醒模式偏移量。</td>
</tr>
<tr class="even">
<td>UINT32</td>
<td>指定 LAN 唤醒数据包的最大保存缓冲区。</td>
</tr>
<tr class="odd">
<td>UINT32</td>
<td>指定支持的协议卸载。
<p>有效的卸载是：</p>
<ul>
<li> (0x00000001) NDIS_PM_PROTOCOL_OFFLOAD_ARP_SUPPORTED</li>
<li>NDIS_PM_PROTOCOL_OFFLOAD_NS_SUPPORTED (0x00000002) </li>
<li>NDIS_PM_PROTOCOL_OFFLOAD_80211_RSN_REKEY_SUPPORTED (0x00000080) </li>
</ul></td>
</tr>
<tr class="even">
<td>UINT32</td>
<td>指定 ARP 卸载 IPv4 地址的数目。</td>
</tr>
<tr class="odd">
<td>UINT32</td>
<td>指定 NS 卸载 IPv6 地址的数目。</td>
</tr>
<tr class="even">
<td><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ne-ntddndis-_ndis_device_power_state" data-raw-source="[&lt;strong&gt;NDIS_DEVICE_POWER_STATE&lt;/strong&gt;](/windows-hardware/drivers/ddi/ntddndis/ne-ntddndis-_ndis_device_power_state)"><strong>NDIS_DEVICE_POWER_STATE</strong></a></td>
<td>指定最小幻数据包唤醒。</td>
</tr>
<tr class="odd">
<td><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ne-ntddndis-_ndis_device_power_state" data-raw-source="[&lt;strong&gt;NDIS_DEVICE_POWER_STATE&lt;/strong&gt;](/windows-hardware/drivers/ddi/ntddndis/ne-ntddndis-_ndis_device_power_state)"><strong>NDIS_DEVICE_POWER_STATE</strong></a></td>
<td>指定最小模式唤醒。</td>
</tr>
<tr class="even">
<td><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ne-ntddndis-_ndis_device_power_state" data-raw-source="[&lt;strong&gt;NDIS_DEVICE_POWER_STATE&lt;/strong&gt;](/windows-hardware/drivers/ddi/ntddndis/ne-ntddndis-_ndis_device_power_state)"><strong>NDIS_DEVICE_POWER_STATE</strong></a></td>
<td>指定最小链接更改唤醒。</td>
</tr>
<tr class="odd">
<td>UINT32</td>
<td>指定支持的唤醒事件。
<p>有效事件包括：</p>
<ul>
<li> (0x00000001) NDIS_PM_WAKE_ON_MEDIA_CONNECT_SUPPORTED</li>
<li>NDIS_PM_WAKE_ON_MEDIA_DISCONNECT_SUPPORTED (0x00000002) </li>
</ul></td>
</tr>
<tr class="even">
<td>UINT32</td>
<td>指定特定于媒体的唤醒事件。
<p>有效事件包括：</p>
<ul>
<li> (0x00000001) NDIS_WLAN_WAKE_ON_NLO_DISCOVERY_SUPPORTED</li>
<li>NDIS_WLAN_WAKE_ON_AP_ASSOCIATION_LOST_SUPPORTED (0x00000002) </li>
<li>NDIS_WLAN_WAKE_ON_GTK_HANDSHAKE_ERROR_SUPPORTED (0x00000004) </li>
<li>NDIS_WLAN_WAKE_ON_4WAY_HANDSHAKE_REQUEST_SUPPORTED (0x00000008) </li>
</ul></td>
</tr>
</tbody>
</table>

 

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
<td>Wditypes.hpp</td>
</tr>
</tbody>
</table>

 

