---
title: WDI_TLV_PM_CAPABILITIES (0x42)
description: WDI_TLV_PM_CAPABILITIES 是包含电源管理功能 TLV。
ms.assetid: DE8A5333-BE2B-4CBB-8C75-45ABBE35A635
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_PM_CAPABILITIES (0x42) 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: a7653b1d697a67f5ce28ed4243ee8de286139d1f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63379801"
---
# <a name="wditlvpmcapabilities-0x42"></a>WDI\_TLV\_PM\_功能 (0x42)


WDI\_TLV\_PM\_功能是包含电源管理功能 TLV。

## <a name="tlv-type"></a>TLV 类型


0x42

## <a name="length"></a>长度


所有包含的元素的大小的总和 （以字节为单位）。

## <a name="values"></a>值


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>在任务栏的搜索框中键入</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>UINT32</td>
<td>指定的电源管理支持标志。
<p>是有效的标志：</p>
<ul>
<li>NDIS_PM_WAKE_PACKET_INDICATION_SUPPORTED</li>
<li>NDIS_PM_SELECTIVE_SUSPEND_SUPPORTED (0x00000002)</li>
</ul></td>
</tr>
<tr class="even">
<td>UINT32</td>
<td>指定受支持的 LAN 唤醒模式。
<p>有效的模式包括：</p>
<ul>
<li>NDIS_PM_WOL_BITMAP_PATTERN_SUPPORTED (0x00000001)</li>
<li>NDIS_PM_WOL_MAGIC_PACKET_SUPPORTED (0x00000002)</li>
<li>NDIS_PM_WOL_IPV4_TCP_SYN_SUPPORTED (0x00000004)</li>
<li>NDIS_PM_WOL_IPV6_TCP_SYN_SUPPORTED (0x00000008)</li>
<li>NDIS_PM_WOL_IPV4_DEST_ADDR_WILDCARD_SUPPORTED (0x00000200)</li>
<li>NDIS_PM_WOL_IPV6_DEST_ADDR_WILDCARD_SUPPORTED (0x00000800)</li>
<li>NDIS_PM_WOL_EAPOL_REQUEST_ID_MESSAGE_SUPPORTED (0x00010000)</li>
</ul></td>
</tr>
<tr class="odd">
<td>UINT32</td>
<td>指定在 LAN 模式的总数。</td>
</tr>
<tr class="even">
<td>UINT32</td>
<td>指定的最大的 LAN 唤醒模式大小。</td>
</tr>
<tr class="odd">
<td>UINT32</td>
<td>指定的最大的 LAN 唤醒模式的偏移量。</td>
</tr>
<tr class="even">
<td>UINT32</td>
<td>指定保存缓冲区的最大 LAN 唤醒数据包。</td>
</tr>
<tr class="odd">
<td>UINT32</td>
<td>指定支持的协议卸载。
<p>是有效的卸载：</p>
<ul>
<li>NDIS_PM_PROTOCOL_OFFLOAD_ARP_SUPPORTED (0X00000001)</li>
<li>NDIS_PM_PROTOCOL_OFFLOAD_NS_SUPPORTED (0X00000002)</li>
<li>NDIS_PM_PROTOCOL_OFFLOAD_80211_RSN_REKEY_SUPPORTED (0x00000080)</li>
</ul></td>
</tr>
<tr class="even">
<td>UINT32</td>
<td>指定卸载 ARP 的数的 IPv4 地址。</td>
</tr>
<tr class="odd">
<td>UINT32</td>
<td>指定卸载 NS 的数的 IPv6 地址。</td>
</tr>
<tr class="even">
<td><a href="https://msdn.microsoft.com/library/windows/hardware/gg602135" data-raw-source="[&lt;strong&gt;NDIS_DEVICE_POWER_STATE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/gg602135)"><strong>NDIS_DEVICE_POWER_STATE</strong></a></td>
<td>指定最小的幻数据包唤醒。</td>
</tr>
<tr class="odd">
<td><a href="https://msdn.microsoft.com/library/windows/hardware/gg602135" data-raw-source="[&lt;strong&gt;NDIS_DEVICE_POWER_STATE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/gg602135)"><strong>NDIS_DEVICE_POWER_STATE</strong></a></td>
<td>指定最小模式唤醒。</td>
</tr>
<tr class="even">
<td><a href="https://msdn.microsoft.com/library/windows/hardware/gg602135" data-raw-source="[&lt;strong&gt;NDIS_DEVICE_POWER_STATE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/gg602135)"><strong>NDIS_DEVICE_POWER_STATE</strong></a></td>
<td>指定最小的链接更改唤醒。</td>
</tr>
<tr class="odd">
<td>UINT32</td>
<td>指定的受支持的唤醒事件。
<p>有效事件是：</p>
<ul>
<li>NDIS_PM_WAKE_ON_MEDIA_CONNECT_SUPPORTED (0x00000001)</li>
<li>NDIS_PM_WAKE_ON_MEDIA_DISCONNECT_SUPPORTED (0x00000002)</li>
</ul></td>
</tr>
<tr class="even">
<td>UINT32</td>
<td>指定特定于媒体的唤醒事件。
<p>有效事件是：</p>
<ul>
<li>NDIS_WLAN_WAKE_ON_NLO_DISCOVERY_SUPPORTED (0X00000001)</li>
<li>NDIS_WLAN_WAKE_ON_AP_ASSOCIATION_LOST_SUPPORTED (0X00000002)</li>
<li>NDIS_WLAN_WAKE_ON_GTK_HANDSHAKE_ERROR_SUPPORTED (0x00000004)</li>
<li>NDIS_WLAN_WAKE_ON_4WAY_HANDSHAKE_REQUEST_SUPPORTED (0x00000008)</li>
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
<td><p>Header</p></td>
<td>Wditypes.hpp</td>
</tr>
</tbody>
</table>

 

 




