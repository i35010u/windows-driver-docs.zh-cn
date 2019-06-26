---
title: 筛选条件标志
description: 本部分介绍筛选条件标志。
ms.assetid: a2493fc5-614f-47df-a818-cdec06dc9f4a
keywords:
- 筛选条件标志网络驱动程序
ms.date: 01/07/2019
ms.localizationpriority: medium
ms.openlocfilehash: 8ddf1285144d5cedf1f2503708cd9248eb7a7768
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67353352"
---
# <a name="filtering-condition-flags"></a>筛选条件标志

每个表示位域的筛选条件标志。 这些标志定义，如下所示：

> [!NOTE]
> 本主题包含内核模式 WFP 标注驱动程序的筛选条件的标志。 有关筛选信息条件用户模式和内核模式之间共享的标志，或如果您正在寻找有关此处未列出的标志的信息，请参阅[筛选条件标志](https://docs.microsoft.com/windows/desktop/FWP/filtering-condition-flags-)Windows SDK 中的主题文档。

<table>
<tr>
<th>筛选条件标志</th>
<th>描述</th>
</tr>
<tr>
<td>
<p>FWP_CONDITION_FLAG_IS_LOOPBACK</p>
<p>0x00000001</p>
</td>
<td>
<p>指示网络流量是环回流量。</p>
<p>此标志是适用于以下筛选层：<dl>
<dd>FWPM_LAYER_INBOUND_IPPACKET_V4</dd>
<dd>FWPM_LAYER_INBOUND_IPPACKET_V6</dd>
<dd>FWPM_LAYER_INBOUND_IPPACKET_V4_DISCARD</dd>
<dd>FWPM_LAYER_INBOUND_IPPACKET_V6_DISCARD</dd>
<dd>FWPM_LAYER_OUTBOUND_IPPACKET_V4</dd>
<dd>FWPM_LAYER_OUTBOUND_IPPACKET_V6</dd>
<dd>FWPM_LAYER_OUTBOUND_IPPACKET_V4_DISCARD</dd>
<dd>FWPM_LAYER_OUTBOUND_IPPACKET_V6_DISCARD</dd>
<dd>FWPM_LAYER_INBOUND_TRANSPORT_V4</dd>
<dd>FWPM_LAYER_INBOUND_TRANSPORT_V6</dd>
<dd>FWPM_LAYER_INBOUND_TRANSPORT_V4_DISCARD</dd>
<dd>FWPM_LAYER_INBOUND_TRANSPORT_V6_DISCARD</dd>
<dd>FWPM_LAYER_OUTBOUND_TRANSPORT_V4</dd>
<dd>FWPM_LAYER_OUTBOUND_TRANSPORT_V6</dd>
<dd>FWPM_LAYER_OUTBOUND_TRANSPORT_V4_DISCARD</dd>
<dd>FWPM_LAYER_OUTBOUND_TRANSPORT_V6_DISCARD</dd>
<dd>FWPM_LAYER_DATAGRAM_DATA_V4</dd>
<dd>FWPM_LAYER_DATAGRAM_DATA_V6</dd>
<dd>FWPM_LAYER_DATAGRAM_DATA_V4_DISCARD</dd>
<dd>FWPM_LAYER_DATAGRAM_DATA_V6_DISCARD</dd>
<dd>FWPM_LAYER_INBOUND_ICMP_ERROR_V4</dd>
<dd>FWPM_LAYER_INBOUND_ICMP_ERROR_V6</dd>
<dd>FWPM_LAYER_INBOUND_ICMP_ERROR_V4_DISCARD</dd>
<dd>FWPM_LAYER_INBOUND_ICMP_ERROR_V6_DISCARD</dd>
<dd>FWPM_LAYER_OUTBOUND_ICMP_ERROR_V4</dd>
<dd>FWPM_LAYER_OUTBOUND_ICMP_ERROR_V6</dd>
<dd>FWPM_LAYER_OUTBOUND_ICMP_ERROR_V4_DISCARD</dd>
<dd>FWPM_LAYER_OUTBOUND_ICMP_ERROR_V6_DISCARD</dd>
<dd>FWPM_LAYER_ALE_AUTH_RECV_ACCEPT_V4</dd>
<dd>FWPM_LAYER_ALE_AUTH_RECV_ACCEPT_V6</dd>
<dd>FWPM_LAYER_ALE_AUTH_RECV_ACCEPT_V4_DISCARD</dd>
<dd>FWPM_LAYER_ALE_AUTH_RECV_ACCEPT_V6_DISCARD</dd>
<dd>FWPM_LAYER_ALE_FLOW_ESTABLISHED_V4</dd>
<dd>FWPM_LAYER_ALE_FLOW_ESTABLISHED_V6</dd>
<dd>FWPM_LAYER_ALE_FLOW_ESTABLISHED_V4_DISCARD</dd>
<dd>FWPM_LAYER_ALE_FLOW_ESTABLISHED_V6_DISCARD</dd>
</dl>
</p>
</td>
</tr>
<tr>
<td>
<p>FWP_CONDITION_FLAG_IS_IPSEC_SECURED</p>
<p>0x00000002</p>
</td>
<td>
<p>指示由 IPsec 保护的网络流量。</p>
<p>此标志是适用于以下筛选层：<dl>
<dd>FWPM_LAYER_INBOUND_TRANSPORT_V4</dd>
<dd>FWPM_LAYER_INBOUND_TRANSPORT_V6</dd>
<dd>FWPM_LAYER_INBOUND_TRANSPORT_V4_DISCARD</dd>
<dd>FWPM_LAYER_INBOUND_TRANSPORT_V6_DISCARD</dd>
<dd>FWPM_LAYER_ALE_FLOW_ESTABLISHED_V4</dd>
<dd>FWPM_LAYER_ALE_FLOW_ESTABLISHED_V6</dd>
<dd>FWPM_LAYER_ALE_FLOW_ESTABLISHED_V4_DISCARD</dd>
<dd>FWPM_LAYER_ALE_FLOW_ESTABLISHED_V6_DISCARD</dd>
</dl>
</p>
</td>
</tr>
<tr>
<td>
<p>FWP_CONDITION_FLAG_IS_REAUTHORIZE</p>
<p>0x00000004</p>
</td>
<td>
<p>指示策略更改 （而不是新的连接）。</p>
<p>此标志是适用于以下筛选层：<dl>
<dd>FWPM_LAYER_ALE_AUTH_RECV_ACCEPT_V4</dd>
<dd>FWPM_LAYER_ALE_AUTH_RECV_ACCEPT_V6</dd>
<dd>FWPM_LAYER_ALE_AUTH_RECV_ACCEPT_V4_DISCARD</dd>
<dd>FWPM_LAYER_ALE_AUTH_RECV_ACCEPT_V6_DISCARD</dd>
<dd>FWPM_LAYER_ALE_AUTH_CONNECT_V4</dd>
<dd>FWPM_LAYER_ALE_AUTH_CONNECT_V6</dd>
<dd>FWPM_LAYER_ALE_AUTH_CONNECT_V4_DISCARD</dd>
<dd>FWPM_LAYER_ALE_AUTH_CONNECT_V6_DISCARD</dd>
</dl>
</p>
<p>此标志，还适用于 Windows Server 2008 R2、 Windows 7 和更高版本的 Windows 中的以下筛选层：<dl>
<dd>FWPM_LAYER_ALE_BIND_REDIRECT_V4</dd>
<dd>FWPM_LAYER_ALE_BIND_REDIRECT_V6</dd>
</dl>
</p>
</td>
</tr>
<tr>
<td>
<p>FWP_CONDITION_FLAG_IS_WILDCARD_BIND</p>
<p>0x00000008</p>
</td>
<td>
<p>指示应用程序绑定到本地网络地址时指定的通配符地址。</p>
<p>此标志是适用于以下筛选层：<dl>
<dd>FWPM_LAYER_ALE_RESOURCE_ASSIGNMENT_V4</dd>
<dd>FWPM_LAYER_ALE_RESOURCE_ASSIGNMENT_V6</dd>
<dd>FWPM_LAYER_ALE_RESOURCE_ASSIGNMENT_V4_DISCARD</dd>
<dd>FWPM_LAYER_ALE_RESOURCE_ASSIGNMENT_V6_DISCARD</dd>
</dl>
</p>
</td>
</tr>
<tr>
<td>
<p>FWP_CONDITION_FLAG_IS_RAW_ENDPOINT</p>
<p>0x00000010</p>
</td>
<td>
<p>指示是发送和接收流量的本地终结点的原始终结点。</p>
<p>此标志是适用于以下筛选层：<dl>
<dd>FWPM_LAYER_INBOUND_TRANSPORT_V4</dd>
<dd>FWPM_LAYER_INBOUND_TRANSPORT_V6</dd>
<dd>FWPM_LAYER_INBOUND_TRANSPORT_V4_DISCARD</dd>
<dd>FWPM_LAYER_INBOUND_TRANSPORT_V6_DISCARD</dd>
<dd>FWPM_LAYER_OUTBOUND_TRANSPORT_V4</dd>
<dd>FWPM_LAYER_OUTBOUND_TRANSPORT_V6</dd>
<dd>FWPM_LAYER_OUTBOUND_TRANSPORT_V4_DISCARD</dd>
<dd>FWPM_LAYER_OUTBOUND_TRANSPORT_V6_DISCARD</dd>
<dd>FWPM_LAYER_DATAGRAM_DATA_V4</dd>
<dd>FWPM_LAYER_DATAGRAM_DATA_V6</dd>
<dd>FWPM_LAYER_DATAGRAM_DATA_V4_DISCARD</dd>
<dd>FWPM_LAYER_DATAGRAM_DATA_V6_DISCARD</dd>
<dd>FWPM_LAYER_INBOUND_ICMP_ERROR_V4</dd>
<dd>FWPM_LAYER_INBOUND_ICMP_ERROR_V6</dd>
<dd>FWPM_LAYER_INBOUND_ICMP_ERROR_V4_DISCARD</dd>
<dd>FWPM_LAYER_INBOUND_ICMP_ERROR_V6_DISCARD</dd>
<dd>FWPM_LAYER_ALE_AUTH_RECV_ACCEPT_V4</dd>
<dd>FWPM_LAYER_ALE_AUTH_RECV_ACCEPT_V6</dd>
<dd>FWPM_LAYER_ALE_AUTH_RECV_ACCEPT_V4_DISCARD</dd>
<dd>FWPM_LAYER_ALE_AUTH_RECV_ACCEPT_V6_DISCARD</dd>
<dd>FWPM_LAYER_ALE_AUTH_CONNECT_V4</dd>
<dd>FWPM_LAYER_ALE_AUTH_CONNECT_V6</dd>
<dd>FWPM_LAYER_ALE_AUTH_CONNECT_V4_DISCARD</dd>
<dd>FWPM_LAYER_ALE_AUTH_CONNECT_V6_DISCARD</dd>
</dl>
</p>
<p>此标志是适用于 Windows Server 2008 R2、 Windows 7 和更高版本的 Windows 中的以下筛选层：<dl>
<dd>FWPM_LAYER_ALE_CONNECT_REDIRECT_V4</dd>
<dd>FWPM_LAYER_ALE_CONNECT_REDIRECT_V6</dd>
<dd>FWPM_LAYER_ALE_BIND_REDIRECT_V4</dd>
<dd>FWPM_LAYER_ALE_BIND_REDIRECT_V6</dd>
</dl>
</p>
</td>
</tr>
<tr>
<td>
<p>FWP_CONDITION_FLAG_IS_FRAGMENT</p>
<p>0x00000020</p>
</td>
<td>
<p>指示<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list"> <b>NET_BUFFER_LIST</b> </a>结构传递给标注驱动程序是 IP 数据包片段。</p>
<p>此标志是适用于以下筛选层：<dl>
<dd>FWPM_LAYER_INBOUND_IPPACKET_V4</dd>
<dd>FWPM_LAYER_INBOUND_IPPACKET_V6</dd>
<dd>FWPM_LAYER_INBOUND_IPPACKET_V4_DISCARD</dd>
<dd>FWPM_LAYER_INBOUND_IPPACKET_V6_DISCARD</dd>
</dl>
</p>
</td>
</tr>
<tr>
<td>
<p>FWP_CONDITION_FLAG_IS_FRAGMENT_GROUP</p>
<p>0x00000040</p>
</td>
<td>
<p>指示<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list"> <b>NET_BUFFER_LIST</b> </a>结构传递给标注驱动程序描述数据包片段的链接的列表。</p>
<p>此标志是适用于以下筛选层：<dl>
<dd>FWPM_LAYER_INBOUND_IPPACKET_V4</dd>
<dd>FWPM_LAYER_INBOUND_IPPACKET_V6</dd>
<dd>FWPM_LAYER_INBOUND_IPPACKET_V4_DISCARD</dd>
<dd>FWPM_LAYER_INBOUND_IPPACKET_V6_DISCARD</dd>
</dl>
</p>
</td>
</tr>
<tr>
<td>
<p>FWP_CONDITION_FLAG_IS_IPSEC_NATT_RECLASSIFY</p>
<p>0x00000080</p>
</td>
<td>
<p>所指示的 NAT 遍历 （UDP 端口 4500） 数据包时设置此标志。  一旦解封发生，标志设置为使用封装的数据包中的信息重新分类。</p>
<p>此标志是适用于以下筛选层：<dl>
<dd>FWPM_LAYER_INBOUND_TRANSPORT_V4</dd>
<dd>FWPM_LAYER_INBOUND_TRANSPORT_V6</dd>
<dd>FWPM_LAYER_INBOUND_TRANSPORT_V4_DISCARD</dd>
<dd>FWPM_LAYER_INBOUND_TRANSPORT_V6_DISCARD</dd>
<dd>FWPM_LAYER_OUTBOUND_TRANSPORT_V4</dd>
<dd>FWPM_LAYER_OUTBOUND_TRANSPORT_V6</dd>
<dd>FWPM_LAYER_OUTBOUND_TRANSPORT_V4_DISCARD</dd>
<dd>FWPM_LAYER_OUTBOUND_TRANSPORT_V6_DISCARD</dd>
</dl>
</p>
</td>
</tr>
<tr>
<td>
<p>FWP_CONDITION_FLAG_REQUIRES_ALE_CLASSIFY</p>
<p>0x00000100</p>
</td>
<td>
<p>指示该数据包已尚未到达的 ALE 接收/接受的层 （FWPM_LAYER_ALE_AUTH_RECV_ACCEPT_V4 或 FWPM_LAYER_ALE_AUTH_RECV_ACCEPT_V6），将在其中跟踪其连接状态。</p>
<p>此标志是适用于以下筛选层：<dl>
<dd>FWPM_LAYER_INBOUND_TRANSPORT_V4</dd>
<dd>FWPM_LAYER_INBOUND_TRANSPORT_V6</dd>
<dd>FWPM_LAYER_INBOUND_TRANSPORT_V4_DISCARD</dd>
<dd>FWPM_LAYER_INBOUND_TRANSPORT_V6_DISCARD</dd>
</dl>
</p>
</td>
</tr>
<tr>
<td>
<p>FWP_CONDITION_FLAG_IS_IMPLICIT_BIND</p>
<p>0x00000200</p>
</td>
<td>
<p>指示套接字不显式绑定。 如果发件人调用发送不第一次调用绑定的情况下，Windows 套接字执行隐式绑定。<div class="alert"><b>请注意</b>  仅在 Windows Server 2008 和 Windows Vista 中支持此标志。 它在更高版本的 Windows 版本中已弃用。</div>
<div> </div>
</p>
<p>此标志是适用于以下筛选层：<dl>
<dd>FWPM_LAYER_ALE_RESOURCE_ASSIGNMENT_V4</dd>
<dd>FWPM_LAYER_ALE_RESOURCE_ASSIGNMENT_V6</dd>
<dd>FWPM_LAYER_ALE_RESOURCE_ASSIGNMENT_V4_DISCARD</dd>
<dd>FWPM_LAYER_ALE_RESOURCE_ASSIGNMENT_V6_DISCARD</dd>
</dl>
</p>
</td>
</tr>
<tr>
<td>
<p>FWP_CONDITION_FLAG_IS_REASSEMBLED</p>
<p>0x00000400</p>
</td>
<td>
<p>指示已重新数据包组合片段的组中。</p>
<p>此标志是适用于 Windows Server 2008、 Windows Vista Service Pack 1 (SP1) 和更高版本的 Windows 中的以下筛选层：<dl>
<dd>FWPM_LAYER_INBOUND_IPPACKET_V4</dd>
<dd>FWPM_LAYER_INBOUND_IPPACKET_V6</dd>
<dd>FWPM_LAYER_INBOUND_IPPACKET_V4_DISCARD</dd>
<dd>FWPM_LAYER_INBOUND_IPPACKET_V6_DISCARD</dd>
</dl>
</p>
</td>
</tr>
<tr>
<td>
<p>FWP_CONDITION_FLAG_IS_NAME_APP_SPECIFIED</p>
<p>0x00004000</p>
</td>
<td>
<p>指示已通过调用一个函数，如获得的应用程序需要连接到的对等机的名称<a href="https://docs.microsoft.com/windows/desktop/api/ws2tcpip/nf-ws2tcpip-wsasetsocketpeertargetname"> <b>WSASetSocketPeerTargetName</b> </a>而不是使用缓存试探法。</p>
<p>此标志是适用于 Windows Server 2008 R2、 Windows 7 和更高版本的 Windows 中的以下筛选层：<dl>
<dd>FWPM_LAYER_ALE_AUTH_CONNECT_V4</dd>
<dd>FWPM_LAYER_ALE_AUTH_CONNECT_V6</dd>
<dd>FWPM_LAYER_ALE_AUTH_CONNECT_V4_DISCARD</dd>
<dd>FWPM_LAYER_ALE_AUTH_CONNECT_V6_DISCARD</dd>
</dl>
</p>
</td>
</tr>
<tr>
<td>
<p>FWP_CONDITION_FLAG_IS_PROMISCUOUS</p>
<p>0x00008000</p>
</td>
<td>
<p>保留供将来使用。</p>
</td>
</tr>
<tr>
<td>
<p>FWP_CONDITION_FLAG_IS_AUTH_FW</p>
<p>0x00010000</p>
</td>
<td>
<p>指示数据包与经过身份验证的防火墙策略相匹配。 只有匹配的"允许连接，如果它是安全的"防火墙规则选项的连接会设置此标志。 有关详细信息，请参阅<a href="https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc753463(v=ws.10)">如何启用身份验证的防火墙旁路</a>。</p>
<p>此标志，还适用于 Windows Server 2008、 Windows Vista SP1 和更高版本的 Windows 中的以下筛选层：<dl>
<dd>FWPM_LAYER_ALE_FLOW_ESTABLISHED_V4</dd>
<dd>FWPM_LAYER_ALE_FLOW_ESTABLISHED_V6</dd>
<dd>FWPM_LAYER_ALE_FLOW_ESTABLISHED_V4_DISCARD</dd>
<dd>FWPM_LAYER_ALE_FLOW_ESTABLISHED_V6_DISCARD</dd>
</dl>
</p>
<p>此标志，还适用于 Windows Server 2008 R2、 Windows 7 和更高版本的 Windows 中的以下筛选层：<dl>
<dd>FWPM_LAYER_ALE_AUTH_CONNECT_V4</dd>
<dd>FWPM_LAYER_ALE_AUTH_CONNECT_V6</dd>
<dd>FWPM_LAYER_ALE_AUTH_CONNECT_V4_DISCARD</dd>
<dd>FWPM_LAYER_ALE_AUTH_CONNECT_V6_DISCARD</dd>
<dd>FWPM_LAYER_ALE_AUTH_RECV_ACCEPT_V4</dd>
<dd>FWPM_LAYER_ALE_AUTH_RECV_ACCEPT_V6</dd>
<dd>FWPM_LAYER_ALE_AUTH_RECV_ACCEPT_V4_DISCARD</dd>
<dd>FWPM_LAYER_ALE_AUTH_RECV_ACCEPT_V6_DISCARD</dd>
</dl>
</p>
</td>
</tr>
<tr>
<td>
<p>FWP_CONDITION_FLAG_IS_RECLASSIFY</p>
<p>0x00020000</p>
</td>
<td>
<p>当设置此标志<a href="https://docs.microsoft.com/windows/desktop/WinSock/ipv6-protection-level">IPV6_PROTECTION_LEVEL</a>此前获得授权的套接字上设置套接字选项。</p>
<p>此标志是适用于以下筛选层：<dl>
<dd>FWPM_LAYER_ALE_RESOURCE_ASSIGNMENT_V6</dd>
<dd>FWPM_LAYER_ALE_RESOURCE_ASSIGNMENT_V6_DISCARD</dd>
<dd>FWPM_LAYER_ALE_AUTH_LISTEN_V6</dd>
<dd>FWPM_LAYER_ALE_AUTH_LISTEN_V6_DISCARD</dd>
</dl>
</p>
</td>
</tr>
<tr>
<td>
<p>FWP_CONDITION_FLAG_IS_OUTBOUND_PASS_THRU</p>
<p>0x00040000</p>
</td>
<td>
<p>指示数据包是弱主机发送，这意味着它不离开此网络接口，因此必须转发到另一个接口。</p>
<p>此标志是适用于 Windows Server 2008 R2、 Windows 7 和更高版本的 Windows 中的以下筛选层：<dl>
<dd>FWPM_LAYER_IPFORWARD_V4</dd>
<dd>FWPM_LAYER_IPFORWARD_V6</dd>
<dd>FWPM_LAYER_IPFORWARD_V4_DISCARD</dd>
<dd>FWPM_LAYER_IPFORWARD_V6_DISCARD</dd>
</dl>
</p>
</td>
</tr>
<tr>
<td>
<p>FWP_CONDITION_FLAG_IS_INBOUND_PASS_THRU</p>
<p>0x00080000</p>
</td>
<td>
<p>指示数据包是弱主机接收，这意味着它不去往接收的网络接口，因此必须转发到另一个接口。</p>
<p>此标志是适用于 Windows Server 2008 R2、 Windows 7 和更高版本的 Windows 中的以下筛选层：<dl>
<dd>FWPM_LAYER_IPFORWARD_V4</dd>
<dd>FWPM_LAYER_IPFORWARD_V6</dd>
<dd>FWPM_LAYER_IPFORWARD_V4_DISCARD</dd>
<dd>FWPM_LAYER_IPFORWARD_V6_DISCARD</dd>
</dl>
</p>
</td>
</tr>
<tr>
<td>
<p>FWP_CONDITION_FLAG_IS_CONNECTION_REDIRECTED</p>
<p>0x00100000</p>
</td>
<td>
<p>指示 ALE_CONNECT_REDIRECT 标注函数进行了重定向连接。</p>
<p>此标志是适用于 Windows Server 2008 R2、 Windows 7 和更高版本的 Windows 中的以下筛选层：<dl>
<dd>FWPM_LAYER_ALE_AUTH_CONNECT_V4</dd>
<dd>FWPM_LAYER_ALE_AUTH_CONNECT_V6</dd>
<dd>FWPM_LAYER_ALE_AUTH_CONNECT_V4_DISCARD</dd>
<dd>FWPM_LAYER_ALE_AUTH_CONNECT_V6_DISCARD</dd>
</dl>
</p>
</td>
</tr>
<tr>
<td>
<p>FWP_CONDITION_FLAG_IS_PROXY_CONNECTION</p>
<p>0x00200000</p>
</td>
<td>
<p>指示该连接已通过代理，并因此以前的重定向记录存在。</p>
<p>此标志是适用于 Windows Server 2012、 Windows 8 和更高版本的 Windows 中的以下筛选层：<dl>
<dd>FWPM_LAYER_ALE_AUTH_CONNECT_V4</dd>
<dd>FWPM_LAYER_ALE_AUTH_CONNECT_V6</dd>
<dd>FWPM_LAYER_ALE_AUTH_CONNECT_V4_DISCARD</dd>
<dd>FWPM_LAYER_ALE_AUTH_CONNECT_V6_DISCARD</dd>
<dd>FWPM_LAYER_ALE_FLOW_ESTABLISHED_V4</dd>
<dd>FWPM_LAYER_ALE_FLOW_ESTABLISHED_V6</dd>
<dd>FWPM_LAYER_ALE_FLOW_ESTABLISHED_V4_DISCARD</dd>
<dd>FWPM_LAYER_ALE_FLOW_ESTABLISHED_V6_DISCARD</dd>
<dd>FWPM_LAYER_ALE_CONNECT_REDIRECT_V4</dd>
<dd>FWPM_LAYER_ALE_CONNECT_REDIRECT_V6</dd>
</dl>
</p>
</td>
</tr>
<tr>
<td>
<p>FWP_CONDITION_FLAG_IS_APPCONTAINER_LOOPBACK</p>
<p>0x00400000</p>
</td>
<td>
<p>指示流量转到和从 AppContainer 使用环回。</p>
<p>此标志是适用于 Windows Server 2012、 Windows 8 和更高版本的 Windows 中的以下筛选层：<dl>
<dd>FWPM_LAYER_ALE_AUTH_RECV_ACCEPT_V4</dd>
<dd>FWPM_LAYER_ALE_AUTH_RECV_ACCEPT_V6</dd>
<dd>FWPM_LAYER_ALE_AUTH_RECV_ACCEPT_V4_DISCARD</dd>
<dd>FWPM_LAYER_ALE_AUTH_RECV_ACCEPT_V6_DISCARD</dd>
<dd>FWPM_LAYER_ALE_AUTH_CONNECT_V4</dd>
<dd>FWPM_LAYER_ALE_AUTH_CONNECT_V6</dd>
<dd>FWPM_LAYER_ALE_AUTH_CONNECT_V4_DISCARD</dd>
<dd>FWPM_LAYER_ALE_AUTH_CONNECT_V6_DISCARD</dd>
</dl>
</p>
</td>
</tr>
<tr>
<td>
<p>FWP_CONDITION_FLAG_IS_NON_APPCONTAINER_LOOPBACK</p>
<p>0x00800000</p>
</td>
<td>
<p>指示与正在使用环回的标准应用 (不 AppContainer) 将流量。</p>
<p>此标志是适用于 Windows Server 2012、 Windows 8 和更高版本的 Windows 中的以下筛选层：<dl>
<dd>FWPM_LAYER_ALE_AUTH_RECV_ACCEPT_V4</dd>
<dd>FWPM_LAYER_ALE_AUTH_RECV_ACCEPT_V6</dd>
<dd>FWPM_LAYER_ALE_AUTH_RECV_ACCEPT_V4_DISCARD</dd>
<dd>FWPM_LAYER_ALE_AUTH_RECV_ACCEPT_V6_DISCARD</dd>
<dd>FWPM_LAYER_ALE_AUTH_CONNECT_V4</dd>
<dd>FWPM_LAYER_ALE_AUTH_CONNECT_V6</dd>
<dd>FWPM_LAYER_ALE_AUTH_CONNECT_V4_DISCARD</dd>
<dd>FWPM_LAYER_ALE_AUTH_CONNECT_V6_DISCARD</dd>
</dl>
</p>
</td>
</tr>
<tr>
<td>
<p>FWP_CONDITION_FLAG_IS_RESERVED</p>
<p>0x01000000</p>
</td>
<td>
<p>保留供将来使用。</p>
</td>
</tr>
<tr>
<td>
<p>FWP_CONDITION_FLAG_IS_HONORING_POLICY_AUTHORIZE</p>
<p>0x02000000</p>
</td>
<td>
<p>指示当前分类执行遵循重定向的通用 Windows 应用程序的意向是连接到指定的主机。 这种分类将包含相同的与可分类字段值，就像应用程序已永远不会重定向。 标志还指示将调用将来分类以匹配有效的重定向的目标。 如果应用程序将重定向到代理服务以进行检查，这也意味着将代理连接上调用将来分类。 标注驱动程序通常应允许此分类。</p>
<p>此标志是适用于 Windows Server 2012、 Windows 8 和更高版本的 Windows 中的以下筛选层：<dl>
<dd>FWPM_LAYER_ALE_AUTH_CONNECT_V4</dd>
<dd>FWPM_LAYER_ALE_AUTH_CONNECT_V6</dd>
<dd>FWPM_LAYER_ALE_AUTH_CONNECT_V4_DISCARD</dd>
<dd>FWPM_LAYER_ALE_AUTH_CONNECT_V6_DISCARD</dd>
</dl>
</p>
</td>
</tr>
</table>

