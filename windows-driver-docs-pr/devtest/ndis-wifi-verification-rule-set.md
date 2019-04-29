---
title: NDIS/WIFI 验证规则集
description: 请注意可以使用这些规则从 Windows 8.1 开始测试 NDIS/WIFI 驱动程序。 .
ms.assetid: B856F42E-E4AD-4178-AF71-3E68A23209C9
ms.date: 05/21/2018
ms.localizationpriority: medium
ms.openlocfilehash: 99842313e9f8432af57ef009df1648ad8aaac86e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63374680"
---
# <a name="ndiswifi-verification-rule-set"></a>NDIS/WIFI 验证规则集


> [!NOTE]
> 可以使用这些规则从 Windows 8.1 开始测试 NDIS/WIFI 驱动程序。

 

## <a name="in-this-section"></a>本节内容


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">主题</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="ndisfiltertimeddatareceive.md" data-raw-source="[&lt;strong&gt;NdisFilterTimedDataReceive&lt;/strong&gt;](ndisfiltertimeddatareceive.md)"><strong>NdisFilterTimedDataReceive</strong></a></p></td>
<td align="left"><p><a href="ndisfiltertimeddatareceive.md" data-raw-source="[&lt;strong&gt;NdisFilterTimedDataReceive&lt;/strong&gt;](ndisfiltertimeddatareceive.md)"> <strong>NdisFilterTimedDataReceive</strong> </a>规则验证 NDIS 筛选器驱动程序完成的接收请求<a href="https://msdn.microsoft.com/library/windows/hardware/ff549960" data-raw-source="[&lt;em&gt;FilterReceiveNetBufferLists&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549960)"> <em>FilterReceiveNetBufferLists</em></a>超时前的函数。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="ndisfiltertimeddatasend.md" data-raw-source="[&lt;strong&gt;NdisFilterTimedDataSend&lt;/strong&gt;](ndisfiltertimeddatasend.md)"><strong>NdisFilterTimedDataSend</strong></a></p></td>
<td align="left"><p><a href="ndisfiltertimeddatasend.md" data-raw-source="[&lt;strong&gt;NdisFilterTimedDataSend&lt;/strong&gt;](ndisfiltertimeddatasend.md)"> <strong>NdisFilterTimedDataSend</strong> </a>规则验证 NDIS 筛选器驱动程序完成发送请求<a href="https://msdn.microsoft.com/library/windows/hardware/ff549966" data-raw-source="[&lt;em&gt;FilterSendNetBufferLists&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549966)"> <em>FilterSendNetBufferLists</em> </a>超时前的函数。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="ndisfiltertimedpausecomplete-.md" data-raw-source="[&lt;strong&gt;NdisFilterTimedPauseComplete&lt;/strong&gt;](ndisfiltertimedpausecomplete-.md)"><strong>NdisFilterTimedPauseComplete</strong></a></p></td>
<td align="left"><p><a href="ndisfiltertimedpausecomplete-.md" data-raw-source="[&lt;strong&gt;NdisFilterTimedPauseComplete&lt;/strong&gt;](ndisfiltertimedpausecomplete-.md)"> <strong>NdisFilterTimedPauseComplete</strong> </a>验证三件事：</p>
<ul>
<li><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff549957" data-raw-source="[&lt;em&gt;FilterPause&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549957)"> <em>FilterPause</em> </a>函数将为已完成在 10 秒或更小。</p></li>
<li><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff549957" data-raw-source="[&lt;em&gt;FilterPause&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549957)"> <em>FilterPause</em> </a>函数必须不会失败。</p></li>
<li><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff549957" data-raw-source="[&lt;em&gt;FilterPause&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549957)"> <em>FilterPause</em> </a>函数必须完成两次。</p></li>
</ul></td>
</tr>
<tr class="even">
<td align="left"><p><a href="ndis-ndisoidcomplete.md" data-raw-source="[&lt;strong&gt;NdisOidComplete&lt;/strong&gt;](ndis-ndisoidcomplete.md)"><strong>NdisOidComplete</strong></a></p></td>
<td align="left"><p><a href="ndis-ndisoidcomplete.md" data-raw-source="[&lt;strong&gt;NdisOidComplete&lt;/strong&gt;](ndis-ndisoidcomplete.md)"> <strong>NdisOidComplete</strong> </a>规则验证 NDIS 微型端口驱动程序正确完成 OID。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="ndis-ndisoiddoublecomplete.md" data-raw-source="[&lt;strong&gt;NdisOidDoubleComplete&lt;/strong&gt;](ndis-ndisoiddoublecomplete.md)"><strong>NdisOidDoubleComplete</strong></a></p></td>
<td align="left"><p><a href="ndis-ndisoiddoublecomplete.md" data-raw-source="[&lt;strong&gt;NdisOidDoubleComplete&lt;/strong&gt;](ndis-ndisoiddoublecomplete.md)"> <strong>NdisOidDoubleComplete</strong> </a>规则指定 NDIS 微型端口驱动程序必须调用<a href="https://msdn.microsoft.com/library/windows/hardware/ff563622" data-raw-source="[&lt;strong&gt;NdisMOidRequestComplete&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff563622)"> <strong>NdisMOidRequestComplete</strong> </a>两次以相同的 OID 的例程。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="ndis-ndisoiddoublerequest.md" data-raw-source="[&lt;strong&gt;NdisOidDoubleRequest&lt;/strong&gt;](ndis-ndisoiddoublerequest.md)"><strong>NdisOidDoubleRequest</strong></a></p></td>
<td align="left"><p>这<a href="ndis-ndisoiddoublerequest.md" data-raw-source="[&lt;strong&gt;NdisOidDoubleRequest&lt;/strong&gt;](ndis-ndisoiddoublerequest.md)"> <strong>NdisOidDoubleRequest</strong> </a>规则验证：</p>
<ul>
<li><p>微型端口驱动程序必须完成<a href="https://msdn.microsoft.com/library/windows/hardware/ff566710" data-raw-source="[&lt;strong&gt;NDIS_OID_REQUEST&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566710)"> <strong>NDIS_OID_REQUEST</strong> </a>这是当前处于挂起状态。</p></li>
</ul></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="ndis-ndistimeddatahang.md" data-raw-source="[&lt;strong&gt;NdisTimedDataHang&lt;/strong&gt;](ndis-ndistimeddatahang.md)"><strong>NdisTimedDataHang</strong></a></p></td>
<td align="left"><p><a href="ndis-ndistimeddatahang.md" data-raw-source="[&lt;strong&gt;NdisTimedDataHang&lt;/strong&gt;](ndis-ndistimeddatahang.md)"> <strong>NdisTimedDataHang</strong> </a>规则验证 NDIS 微型端口驱动程序处理的任何挂起的发送请求<a href="https://msdn.microsoft.com/library/windows/hardware/ff568388" data-raw-source="[&lt;strong&gt;NET_BUFFER_LIST&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff568388)"> <strong>NET_BUFFER_LIST</strong> </a>22 秒内的结构。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="ndis-ndistimeddatasend.md" data-raw-source="[&lt;strong&gt;NdisTimedDataSend&lt;/strong&gt;](ndis-ndistimeddatasend.md)"><strong>NdisTimedDataSend</strong></a></p></td>
<td align="left"><p><a href="ndis-ndistimeddatasend.md" data-raw-source="[&lt;strong&gt;NdisTimedDataSend&lt;/strong&gt;](ndis-ndistimeddatasend.md)"> <strong>NdisTimedDataSend</strong> </a>规则验证时的 NDIS 驱动程序调用<a href="https://msdn.microsoft.com/library/windows/hardware/ff559440" data-raw-source="[&lt;em&gt;MiniportSendNetBufferLists&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff559440)"> <em>MiniportSendNetBufferLists</em></a>，微型端口驱动程序在 30 秒内完成发送请求。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="ndis-ndistimedoidcomplete.md" data-raw-source="[&lt;strong&gt;NdisTimedOidComplete&lt;/strong&gt;](ndis-ndistimedoidcomplete.md)"><strong>NdisTimedOidComplete</strong></a></p></td>
<td align="left"><p><a href="ndis-ndistimedoidcomplete.md" data-raw-source="[&lt;strong&gt;NdisTimedOidComplete&lt;/strong&gt;](ndis-ndistimedoidcomplete.md)"> <strong>NdisTimedOidComplete</strong> </a>规则指定 NDIS 微型端口驱动程序在 12 秒内完成的 OID 请求。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="ndis-wlanassociation.md" data-raw-source="[&lt;strong&gt;WlanAssociation&lt;/strong&gt;](ndis-wlanassociation.md)"><strong>WlanAssociation</strong></a></p></td>
<td align="left"><p><a href="ndis-wlanassociation.md" data-raw-source="[&lt;strong&gt;WlanAssociation&lt;/strong&gt;](ndis-wlanassociation.md)"> <strong>WlanAssociation</strong> </a>规则验证微型端口驱动程序正确地遵循本机 802.11 无线 LAN (WLAN) 关联序列。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="ndis-wlanconnectionroaming.md" data-raw-source="[&lt;strong&gt;WlanConnectionRoaming&lt;/strong&gt;](ndis-wlanconnectionroaming.md)"><strong>WlanConnectionRoaming</strong></a></p></td>
<td align="left"><p><a href="ndis-wlanconnectionroaming.md" data-raw-source="[&lt;strong&gt;WlanConnectionRoaming&lt;/strong&gt;](ndis-wlanconnectionroaming.md)"> <strong>WlanConnectionRoaming</strong> </a>规则验证微型端口驱动程序正确地遵循本机 802.11 无线 LAN (WLAN) 连接和漫游序列。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="ndis-wlandisassociation.md" data-raw-source="[&lt;strong&gt;WlanDisassociation&lt;/strong&gt;](ndis-wlandisassociation.md)"><strong>WlanDisassociation</strong></a></p></td>
<td align="left"><p><a href="ndis-wlandisassociation.md" data-raw-source="[&lt;strong&gt;WlanDisassociation&lt;/strong&gt;](ndis-wlandisassociation.md)"> <strong>WlanDisassociation</strong> </a>规则验证微型端口驱动程序正确地遵循本机 802.11 无线 LAN (WLAN) 解除关联序列。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="ndis-wlantimedassociation.md" data-raw-source="[&lt;strong&gt;WlanTimedAssociation&lt;/strong&gt;](ndis-wlantimedassociation.md)"><strong>WlanTimedAssociation</strong></a></p></td>
<td align="left"><p><a href="ndis-wlantimedassociation.md" data-raw-source="[&lt;strong&gt;WlanTimedAssociation&lt;/strong&gt;](ndis-wlantimedassociation.md)"> <strong>WlanTimedAssociation</strong> </a>规则指定 NDIS 微型端口驱动程序完成在 10 秒的无线 LAN (WLAN) 关联操作。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="ndis-wlantimedconnectionroaming.md" data-raw-source="[&lt;strong&gt;WlanTimedConnectionRoaming&lt;/strong&gt;](ndis-wlantimedconnectionroaming.md)"><strong>WlanTimedConnectionRoaming</strong></a></p></td>
<td align="left"><p><a href="ndis-wlantimedconnectionroaming.md" data-raw-source="[&lt;strong&gt;WlanTimedConnectionRoaming&lt;/strong&gt;](ndis-wlantimedconnectionroaming.md)"> <strong>WlanTimedConnectionRoaming</strong> </a>规则指定 NDIS 微型端口驱动程序在 10 秒内完成无线 LAN (WLAN) 漫游连接/操作。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="ndis-wlantimedconnectrequest.md" data-raw-source="[&lt;strong&gt;WlanTimedConnectRequest&lt;/strong&gt;](ndis-wlantimedconnectrequest.md)"><strong>WlanTimedConnectRequest</strong></a></p></td>
<td align="left"><p><a href="ndis-wlantimedconnectrequest.md" data-raw-source="[&lt;strong&gt;WlanTimedConnectRequest&lt;/strong&gt;](ndis-wlantimedconnectrequest.md)"> <strong>WlanTimedConnectRequest</strong> </a>规则验证，OID_DOT11_CONNECT_REQUEST 后跟 NDIS_STATUS_DOT11_CONNECTION_START 在 10 秒内。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="ndis-wlantimedscan.md" data-raw-source="[&lt;strong&gt;WlanTimedScan&lt;/strong&gt;](ndis-wlantimedscan.md)"><strong>WlanTimedScan</strong></a></p></td>
<td align="left"><p><a href="ndis-wlantimedscan.md" data-raw-source="[&lt;strong&gt;WlanTimedScan&lt;/strong&gt;](ndis-wlantimedscan.md)"> <strong>WlanTimedScan</strong> </a>规则验证 WLAN 扫描操作 15 秒内完成。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="ndis-wlantimedlinkquality.md" data-raw-source="[&lt;strong&gt;WlanTimedLinkQuality&lt;/strong&gt;](ndis-wlantimedlinkquality.md)"><strong>WlanTimedLinkQuality</strong></a></p></td>
<td align="left"><p><a href="ndis-wlantimedlinkquality.md" data-raw-source="[&lt;strong&gt;WlanTimedLinkQuality&lt;/strong&gt;](ndis-wlantimedlinkquality.md)"> <strong>WlanTimedLinkQuality</strong> </a>规则指定 NDIS_STATUS_DOT11_LINK_QUALITY 指示在 15 秒内成功 NDIS_STATUS_DOT11_ASSOCIATION_COMPLETION 之后进行。</p></td>
</tr>
</tbody>
</table>

 

<a name="how-to-test"></a>如何测试
-----------

<table>
<colgroup>
<col width="100%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">在运行时</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>运行<a href="https://msdn.microsoft.com/library/windows/hardware/ff545448" data-raw-source="[Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff545448)">Driver Verifier</a> ，然后选择<a href="https://msdn.microsoft.com/library/windows/hardware/dn312128" data-raw-source="[NDIS/WIFI verification](https://msdn.microsoft.com/library/windows/hardware/dn312128)">NDIS/WIFI 验证</a>选项。</p></td>
</tr>
</tbody>
</table>

 

 

 





