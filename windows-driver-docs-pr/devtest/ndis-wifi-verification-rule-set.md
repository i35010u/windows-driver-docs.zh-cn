---
title: NDIS/WIFI 验证规则集
description: 请注意，你可以从 Windows 8.1 开始测试 NDIS/WIFI 驱动程序与这些规则。 .
ms.date: 05/21/2018
ms.localizationpriority: medium
ms.openlocfilehash: d9b79decb8c6c902ffa0e762bc6288daffc7f25e
ms.sourcegitcommit: a9fb2c30adf09ee24de8e68ac1bc6326ef3616b8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2021
ms.locfileid: "102249134"
---
# <a name="ndiswifi-verification-rule-set"></a>NDIS/WIFI 验证规则集


> [!NOTE]
> 可以从 Windows 8.1 开始测试 NDIS/WIFI 驱动程序，这些规则从开始。

 

## <a name="in-this-section"></a>在本节中


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
<td align="left"><p><a href="ndisfiltertimeddatareceive.md" data-raw-source="[&lt;strong&gt;NdisFilterTimedDataReceive&lt;/strong&gt;](ndisfiltertimeddatareceive.md)"><strong>NdisFilterTimedDataReceive</strong></a>规则验证 NDIS 筛选器驱动程序在超时前是否通过<a href="/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_receive_net_buffer_lists" data-raw-source="[&lt;em&gt;FilterReceiveNetBufferLists&lt;/em&gt;](/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_receive_net_buffer_lists)"><em>FilterReceiveNetBufferLists</em></a>函数完成了接收请求。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="ndisfiltertimeddatasend.md" data-raw-source="[&lt;strong&gt;NdisFilterTimedDataSend&lt;/strong&gt;](ndisfiltertimeddatasend.md)"><strong>NdisFilterTimedDataSend</strong></a></p></td>
<td align="left"><p><a href="ndisfiltertimeddatasend.md" data-raw-source="[&lt;strong&gt;NdisFilterTimedDataSend&lt;/strong&gt;](ndisfiltertimeddatasend.md)"><strong>NdisFilterTimedDataSend</strong></a>规则验证 NDIS 筛选器驱动程序在超时前是否通过<a href="/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_send_net_buffer_lists" data-raw-source="[&lt;em&gt;FilterSendNetBufferLists&lt;/em&gt;](/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_send_net_buffer_lists)"><em>FilterSendNetBufferLists</em></a>函数完成了发送请求。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="ndisfiltertimedpausecomplete-.md" data-raw-source="[&lt;strong&gt;NdisFilterTimedPauseComplete&lt;/strong&gt;](ndisfiltertimedpausecomplete-.md)"><strong>NdisFilterTimedPauseComplete</strong></a></p></td>
<td align="left"><p><a href="ndisfiltertimedpausecomplete-.md" data-raw-source="[&lt;strong&gt;NdisFilterTimedPauseComplete&lt;/strong&gt;](ndisfiltertimedpausecomplete-.md)"><strong>NdisFilterTimedPauseComplete</strong></a>验证三个方面：</p>
<ul>
<li><p><a href="/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_pause" data-raw-source="[&lt;em&gt;FilterPause&lt;/em&gt;](/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_pause)"><em>FilterPause</em></a>函数将在10秒或更短时间内完成。</p></li>
<li><p><a href="/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_pause" data-raw-source="[&lt;em&gt;FilterPause&lt;/em&gt;](/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_pause)"><em>FilterPause</em></a>函数不能失败。</p></li>
<li><p><a href="/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_pause" data-raw-source="[&lt;em&gt;FilterPause&lt;/em&gt;](/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_pause)"><em>FilterPause</em></a>函数不得完成两次。</p></li>
</ul></td>
</tr>
<tr class="even">
<td align="left"><p><a href="ndis-ndisoidcomplete.md" data-raw-source="[&lt;strong&gt;NdisOidComplete&lt;/strong&gt;](ndis-ndisoidcomplete.md)"><strong>NdisOidComplete</strong></a></p></td>
<td align="left"><p><a href="ndis-ndisoidcomplete.md" data-raw-source="[&lt;strong&gt;NdisOidComplete&lt;/strong&gt;](ndis-ndisoidcomplete.md)"><strong>NdisOidComplete</strong></a>规则验证 NDIS 微型端口驱动程序是否正确完成了 OID。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="ndis-ndisoiddoublecomplete.md" data-raw-source="[&lt;strong&gt;NdisOidDoubleComplete&lt;/strong&gt;](ndis-ndisoiddoublecomplete.md)"><strong>NdisOidDoubleComplete</strong></a></p></td>
<td align="left"><p><a href="ndis-ndisoiddoublecomplete.md" data-raw-source="[&lt;strong&gt;NdisOidDoubleComplete&lt;/strong&gt;](ndis-ndisoiddoublecomplete.md)"><strong>NdisOidDoubleComplete</strong></a>规则指定 NDIS 微型端口驱动程序不得为同一 OID 调用两次<a href="/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismoidrequestcomplete" data-raw-source="[&lt;strong&gt;NdisMOidRequestComplete&lt;/strong&gt;](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismoidrequestcomplete)"><strong>NdisMOidRequestComplete</strong></a>例程。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="ndis-ndisoiddoublerequest.md" data-raw-source="[&lt;strong&gt;NdisOidDoubleRequest&lt;/strong&gt;](ndis-ndisoiddoublerequest.md)"><strong>NdisOidDoubleRequest</strong></a></p></td>
<td align="left"><p>此 <a href="ndis-ndisoiddoublerequest.md" data-raw-source="[&lt;strong&gt;NdisOidDoubleRequest&lt;/strong&gt;](ndis-ndisoiddoublerequest.md)"><strong>NdisOidDoubleRequest</strong></a> 规则验证：</p>
<ul>
<li><p>Minport 驱动程序必须完成当前挂起的 <a href="/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request" data-raw-source="[&lt;strong&gt;NDIS_OID_REQUEST&lt;/strong&gt;](/windows-hardware/drivers/ddi/oidrequest/ns-oidrequest-ndis_oid_request)"><strong>NDIS_OID_REQUEST</strong></a> 。</p></li>
</ul></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="ndis-ndistimeddatahang.md" data-raw-source="[&lt;strong&gt;NdisTimedDataHang&lt;/strong&gt;](ndis-ndistimeddatahang.md)"><strong>NdisTimedDataHang</strong></a></p></td>
<td align="left"><p><a href="ndis-ndistimeddatahang.md" data-raw-source="[&lt;strong&gt;NdisTimedDataHang&lt;/strong&gt;](ndis-ndistimeddatahang.md)"><strong>NdisTimedDataHang</strong></a>规则验证 NDIS 微型端口驱动程序是否在22秒内处理<a href="/windows-hardware/drivers/ddi/nbl/ns-nbl-net_buffer_list" data-raw-source="[&lt;strong&gt;NET_BUFFER_LIST&lt;/strong&gt;](/windows-hardware/drivers/ddi/nbl/ns-nbl-net_buffer_list)"><strong>NET_BUFFER_LIST</strong></a>结构的任何挂起的发送请求。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="ndis-ndistimeddatasend.md" data-raw-source="[&lt;strong&gt;NdisTimedDataSend&lt;/strong&gt;](ndis-ndistimeddatasend.md)"><strong>NdisTimedDataSend</strong></a></p></td>
<td align="left"><p><a href="ndis-ndistimeddatasend.md" data-raw-source="[&lt;strong&gt;NdisTimedDataSend&lt;/strong&gt;](ndis-ndistimeddatasend.md)"><strong>NdisTimedDataSend</strong></a>规则验证当 NDIS 驱动程序调用<a href="/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_send_net_buffer_lists" data-raw-source="[&lt;em&gt;MiniportSendNetBufferLists&lt;/em&gt;](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_send_net_buffer_lists)"><em>MiniportSendNetBufferLists</em></a>时，微型端口驱动程序在30秒内完成了发送请求。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="ndis-ndistimedoidcomplete.md" data-raw-source="[&lt;strong&gt;NdisTimedOidComplete&lt;/strong&gt;](ndis-ndistimedoidcomplete.md)"><strong>NdisTimedOidComplete</strong></a></p></td>
<td align="left"><p><a href="ndis-ndistimedoidcomplete.md" data-raw-source="[&lt;strong&gt;NdisTimedOidComplete&lt;/strong&gt;](ndis-ndistimedoidcomplete.md)"><strong>NdisTimedOidComplete</strong></a>规则指定 NDIS 微型端口驱动程序在12秒内完成 OID 请求。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="ndis-wlanassert.md" data-raw-source="[&lt;strong&gt;WlanAssert&lt;/strong&gt;](ndis-wlanassert.md)"><strong>WlanAssert</strong></a></p></td>
<td align="left"><p><a href="ndis-wlanassert.md" data-raw-source="[&lt;strong&gt;WlanAssociation&lt;/strong&gt;](ndis-wlanassert.md)"><strong>WlanAssert</strong></a>规则包括在 WDIWIFI 驱动程序中验证的一组检查。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="ndis-wlanassociation.md" data-raw-source="[&lt;strong&gt;WlanAssociation&lt;/strong&gt;](ndis-wlanassociation.md)"><strong>WlanAssociation</strong></a></p></td>
<td align="left"><p><a href="ndis-wlanassociation.md" data-raw-source="[&lt;strong&gt;WlanAssociation&lt;/strong&gt;](ndis-wlanassociation.md)"><strong>WlanAssociation</strong></a>规则验证微型端口驱动程序是否正确地遵从了本机802.11 无线局域网 (WLAN) 关联序列。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="ndis-wlanconnectionroaming.md" data-raw-source="[&lt;strong&gt;WlanConnectionRoaming&lt;/strong&gt;](ndis-wlanconnectionroaming.md)"><strong>WlanConnectionRoaming</strong></a></p></td>
<td align="left"><p><a href="ndis-wlanconnectionroaming.md" data-raw-source="[&lt;strong&gt;WlanConnectionRoaming&lt;/strong&gt;](ndis-wlanconnectionroaming.md)"><strong>WlanConnectionRoaming</strong></a>规则验证微型端口驱动程序是否正确地遵从了本机802.11 无线局域网 (WLAN) 连接和漫游顺序。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="ndis-wlandisassociation.md" data-raw-source="[&lt;strong&gt;WlanDisassociation&lt;/strong&gt;](ndis-wlandisassociation.md)"><strong>WlanDisassociation</strong></a></p></td>
<td align="left"><p><a href="ndis-wlandisassociation.md" data-raw-source="[&lt;strong&gt;WlanDisassociation&lt;/strong&gt;](ndis-wlandisassociation.md)"><strong>WlanDisassociation</strong></a>规则验证微型端口驱动程序是否正确遵循了本机802.11 无线局域网 (WLAN) 解除相应的序列。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="ndis-wlantimedassociation.md" data-raw-source="[&lt;strong&gt;WlanTimedAssociation&lt;/strong&gt;](ndis-wlantimedassociation.md)"><strong>WlanTimedAssociation</strong></a></p></td>
<td align="left"><p><a href="ndis-wlantimedassociation.md" data-raw-source="[&lt;strong&gt;WlanTimedAssociation&lt;/strong&gt;](ndis-wlantimedassociation.md)"><strong>WlanTimedAssociation</strong></a>规则指定 NDIS 微型端口驱动程序在10秒内完成无线 LAN (WLAN) 关联操作。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="ndis-wlantimedconnectionroaming.md" data-raw-source="[&lt;strong&gt;WlanTimedConnectionRoaming&lt;/strong&gt;](ndis-wlantimedconnectionroaming.md)"><strong>WlanTimedConnectionRoaming</strong></a></p></td>
<td align="left"><p><a href="ndis-wlantimedconnectionroaming.md" data-raw-source="[&lt;strong&gt;WlanTimedConnectionRoaming&lt;/strong&gt;](ndis-wlantimedconnectionroaming.md)"><strong>WlanTimedConnectionRoaming</strong></a>规则指定 NDIS 微型端口驱动程序在10秒内完成无线 LAN (WLAN) 连接/漫游操作。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="ndis-wlantimedconnectrequest.md" data-raw-source="[&lt;strong&gt;WlanTimedConnectRequest&lt;/strong&gt;](ndis-wlantimedconnectrequest.md)"><strong>WlanTimedConnectRequest</strong></a></p></td>
<td align="left"><p><a href="ndis-wlantimedconnectrequest.md" data-raw-source="[&lt;strong&gt;WlanTimedConnectRequest&lt;/strong&gt;](ndis-wlantimedconnectrequest.md)"><strong>WlanTimedConnectRequest</strong></a>规则验证 OID_DOT11_CONNECT_REQUEST 后是否 NDIS_STATUS_DOT11_CONNECTION_START 10 秒内。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="ndis-wlantimedscan.md" data-raw-source="[&lt;strong&gt;WlanTimedScan&lt;/strong&gt;](ndis-wlantimedscan.md)"><strong>WlanTimedScan</strong></a></p></td>
<td align="left"><p><a href="ndis-wlantimedscan.md" data-raw-source="[&lt;strong&gt;WlanTimedScan&lt;/strong&gt;](ndis-wlantimedscan.md)"><strong>WlanTimedScan</strong></a>规则验证 WLAN 扫描操作是否在15秒内完成。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="ndis-wlantimedlinkquality.md" data-raw-source="[&lt;strong&gt;WlanTimedLinkQuality&lt;/strong&gt;](ndis-wlantimedlinkquality.md)"><strong>WlanTimedLinkQuality</strong></a></p></td>
<td align="left"><p><a href="ndis-wlantimedlinkquality.md" data-raw-source="[&lt;strong&gt;WlanTimedLinkQuality&lt;/strong&gt;](ndis-wlantimedlinkquality.md)"><strong>WlanTimedLinkQuality</strong></a>规则指定在成功 NDIS_STATUS_DOT11_ASSOCIATION_COMPLETION 后15秒内发出 NDIS_STATUS_DOT11_LINK_QUALITY 指示。</p></td>
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
<td align="left"><p>运行 <a href="/windows-hardware/drivers/devtest/driver-verifier" data-raw-source="[Driver Verifier](./driver-verifier.md)">驱动程序验证程序</a> ，并选择 <a href="/windows-hardware/drivers/devtest/ndis-wifi-verification" data-raw-source="[NDIS/WIFI verification](./ndis-wifi-verification.md)">NDIS/WIFI 验证</a> 选项。</p></td>
</tr>
</tbody>
</table>

 

