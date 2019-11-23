---
title: 数据偏移位置
description: 本部分介绍 Windows 筛选平台标注驱动程序的数据偏移位置。
ms.assetid: cf4656cf-b978-4539-9fff-8f0aa5de1b5e
keywords:
- 数据偏移位置网络驱动程序
ms.date: 11/09/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5585ea707800c47b3f4fc3c3b10e770fcb7eeb37
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838164"
---
# <a name="data-offset-positions"></a>数据偏移位置

当筛选器引擎调用标注驱动程序的[classifyFn](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nc-fwpsk-fwps_callout_classify_fn0) callout 函数时，它会在*layerData*参数中传递一个指向结构的指针。 对于筛选数据包数据的层，指针引用[NET_BUFFER_LIST](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)结构。 根据调用*classifyFn* callout 函数的筛选层，筛选器引擎会将 layerData * 参数中的指针传递到以下结构之一：

- 对于流层， *layerData*参数包含指向[FWPS_STREAM_CALLOUT_IO_PACKET0](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/ns-fwpsk-fwps_stream_callout_io_packet0_)结构的指针。 此结构的 streamData 成员包含指向[FWPS_STREAM_DATA0](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/ns-fwpsk-fwps_stream_data0_)结构的指针。 

    [FWPS_STREAM_DATA0](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/ns-fwpsk-fwps_stream_data0_)结构的**netBufferListChain**成员包含指向[NET_BUFFER_LIST](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)结构的指针。 

- 对于所有其他层， *layerData*参数包含指向[NET_BUFFER_LIST](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)结构的指针。

> [!NOTE]
> *LayerData*参数可能为 NULL，具体取决于正在筛选的层以及用于调用驱动程序的[classifyFn](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nc-fwpsk-fwps_callout_classify_fn0) callout 函数的条件。
 
[NET_BUFFER_LIST](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)结构包含[NET_BUFFER](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer)结构的链接列表。 在每个**NET_BUFFER**结构的[NET_BUFFER_DATA](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_data)结构内，**数据偏移量**成员指向数据包数据中的特定位置。 **数据偏移量**成员指向的位置取决于筛选器引擎调用标注驱动程序的*classifyFn*标注函数的筛选层。 

对于每个筛选层，由**数据偏移量**成员指定的数据包数据中的位置定义如下：

<table>
<tr>
<th>运行时筛选层标识符（从 Windows Vista 开始）</th>
<th>数据包数据中的位置</th>
</tr>
<tr>
<td>
<p>FWPS_LAYER_INBOUND_IPPACKET_V4</p>
<p>FWPS_LAYER_INBOUND_IPPACKET_V6</p>
</td>
<td>
<p>传输标头的开头。</p>
</td>
</tr>
<tr>
<td>
<p>FWPS_LAYER_INBOUND_IPPACKET_V4_DISCARD</p>
<p>FWPS_LAYER_INBOUND_IPPACKET_V6_DISCARD</p>
</td>
<td>
<p>TCP/IP 堆栈停止处理的偏移量。</p>
</td>
</tr>
<tr>
<td>
<p>FWPS_LAYER_OUTBOUND_IPPACKET_V4</p>
<p>FWPS_LAYER_OUTBOUND_IPPACKET_V6</p>
</td>
<td>
<p>IP 标头的开头。</p>
</td>
</tr>
<tr>
<td>
<p>FWPS_LAYER_OUTBOUND_IPPACKET_V4_DISCARD</p>
<p>FWPS_LAYER_OUTBOUND_IPPACKET_V6_DISCARD</p>
</td>
<td>
<p>TCP/IP 堆栈停止处理的偏移量。</p>
</td>
</tr>
<tr>
<td>
<p>FWPS_LAYER_IPFORWARD_V4</p>
<p>FWPS_LAYER_IPFORWARD_V6</p>
</td>
<td>
<p>IP 标头的开头。</p>
</td>
</tr>
<tr>
<td>
<p>FWPS_LAYER_IPFORWARD_V4_DISCARD</p>
<p>FWPS_LAYER_IPFORWARD_V6_DISCARD</p>
</td>
<td>
<p>IP 标头的开头。</p>
</td>
</tr>
<tr>
<td>
<p>FWPS_LAYER_INBOUND_TRANSPORT_V4</p>
<p>FWPS_LAYER_INBOUND_TRANSPORT_V6</p>
</td>
<td>
<p>数据的开头。</p>
<div class="alert"><b>请注意</b>，  在 tcp/ip 堆栈的 icmp 套接字上收到的入站数据包，偏移量是 icmp 标头的开头。</div>
<div> </div>
</td>
</tr>
<tr>
<td>
<p>FWPS_LAYER_INBOUND_TRANSPORT_V4_DISCARD</p>
<p>FWPS_LAYER_INBOUND_TRANSPORT_V6_DISCARD</p>
</td>
<td>
<p>数据的开头。</p>
<div class="alert"><b>请注意</b>，  在 tcp/ip 堆栈的 icmp 套接字上收到的入站数据包，偏移量是 icmp 标头的开头。</div>
<div> </div>
</td>
</tr>
<tr>
<td>
<p>FWPS_LAYER_OUTBOUND_TRANSPORT_V4</p>
<p>FWPS_LAYER_OUTBOUND_TRANSPORT_V6</p>
</td>
<td>
<p>传输标头的开头。</p>
</td>
</tr>
<tr>
<td>
<p>FWPS_LAYER_OUTBOUND_TRANSPORT_V4_DISCARD</p>
<p>FWPS_LAYER_OUTBOUND_TRANSPORT_V6_DISCARD</p>
</td>
<td>
<p>传输标头的开头。</p>
</td>
</tr>
<tr>
<td>
<p>FWPS_LAYER_STREAM_V4</p>
<p>FWPS_LAYER_STREAM_V6</p>
</td>
<td>
<p>数据的开头。</p>
<div class="alert"><b>请注意</b>   数据包数据中的位置不包含 IP、IPv6 和传输标头。</div>
<div> </div>
</td>
</tr>
<tr>
<td>
<p>FWPS_LAYER_STREAM_V4_DISCARD</p>
<p>FWPS_LAYER_STREAM_V6_DISCARD</p>
</td>
<td>
<p>数据的开头。</p>
<div class="alert"><b>请注意</b>   数据包数据中的位置不包含 IP、IPv6 或传输标头。</div>
<div> </div>
</td>
</tr>
<tr>
<td>
<p>FWPS_LAYER_DATAGRAM_DATA_V4</p>
<p>FWPS_LAYER_DATAGRAM_DATA_V6</p>
</td>
<td>
<p>对于入站数据报：数据的开头。</p>
<div class="alert"><b>请注意</b>，  在 tcp/ip 堆栈的 icmp 套接字上收到的入站数据包，偏移量是 icmp 标头的开头。</div>
<div> </div>
<p>对于出站数据报：传输标头的开头。</p>
</td>
</tr>
<tr>
<td>
<p>FWPS_LAYER_DATAGRAM_DATA_V4_DISCARD</p>
<p>FWPS_LAYER_DATAGRAM_DATA_V6_DISCARD</p>
</td>
<td>
<p>对于入站数据报：数据的开头。</p>
<div class="alert"><b>请注意</b>，  在 tcp/ip 堆栈的 icmp 套接字上收到的入站数据包，偏移量是 icmp 标头的开头。</div>
<div> </div>
<p>对于出站数据报：传输标头的开头。</p>
</td>
</tr>
<tr>
<td>
<p>FWPS_LAYER_INBOUND_ICMP_ERROR_V4</p>
<p>FWPS_LAYER_INBOUND_ICMP_ERROR_V6</p>
</td>
<td>
<p>内部 IP 标头的开头。</p>
</td>
</tr>
<tr>
<td>
<p>FWPS_LAYER_INBOUND_ICMP_ERROR_V4_DISCARD</p>
<p>FWPS_LAYER_INBOUND_ICMP_ERROR_V6_DISCARD</p>
</td>
<td>
<p>内部 IP 标头的开头。</p>
</td>
</tr>
<tr>
<td>
<p>FWPS_LAYER_OUTBOUND_ICMP_ERROR_V4</p>
<p>FWPS_LAYER_OUTBOUND_ICMP_ERROR_V6</p>
</td>
<td>
<p>ICMP 标头的开头。</p>
</td>
</tr>
<tr>
<td>
<p>FWPS_LAYER_OUTBOUND_ICMP_ERROR_V4_DISCARD</p>
<p>FWPS_LAYER_OUTBOUND_ICMP_ERROR_V6_DISCARD</p>
</td>
<td>
<p>ICMP 标头的开头。</p>
</td>
</tr>
<tr>
<td>
<p>FWPS_LAYER_ALE_RESOURCE_ASSIGNMENT_V4</p>
<p>FWPS_LAYER_ALE_RESOURCE_ASSIGNMENT_V6</p>
</td>
<td>
<p>不适用。</p>
</td>
</tr>
<tr>
<td>
<p>FWPS_LAYER_ALE_RESOURCE_ASSIGNMENT_V4_DISCARD</p>
<p>FWPS_LAYER_ALE_RESOURCE_ASSIGNMENT_V6_DISCARD</p>
</td>
<td>
<p>不适用。</p>
</td>
</tr>
<tr>
<td>
<p>FWPS_LAYER_ALE_AUTH_LISTEN_V4</p>
<p>FWPS_LAYER_ALE_AUTH_LISTEN_V6</p>
</td>
<td>
<p>不适用。</p>
</td>
</tr>
<tr>
<td>
<p>FWPS_LAYER_ALE_AUTH_LISTEN_V4_DISCARD</p>
<p>FWPS_LAYER_ALE_AUTH_LISTEN_V6_DISCARD</p>
</td>
<td>
<p>不适用。</p>
</td>
</tr>
<tr>
<td>
<p>FWPS_LAYER_ALE_AUTH_RECV_ACCEPT_V4</p>
<p>FWPS_LAYER_ALE_AUTH_RECV_ACCEPT_V6</p>
</td>
<td>
<p>对于入站数据包方向：数据的开头。</p>
<div class="alert"><b>请注意</b>，  在 tcp/ip 堆栈的 icmp 套接字上收到的入站数据包，偏移量是 icmp 标头的开头。</div>
<div> </div>
<p>对于出站数据包方向：传输标头的开头。</p>
</td>
</tr>
<tr>
<td>
<p>FWPS_LAYER_ALE_AUTH_RECV_ACCEPT_V4_DISCARD</p>
<p>FWPS_LAYER_ALE_AUTH_RECV_ACCEPT_V6_DISCARD</p>
</td>
<td>
<p>对于入站数据包方向：数据的开头。</p>
<div class="alert"><b>请注意</b>，  在 tcp/ip 堆栈的 icmp 套接字上收到的入站数据包，偏移量是 icmp 标头的开头。</div>
<div> </div>
<p>对于出站数据包方向：传输标头的开头。</p>
</td>
</tr>
<tr>
<td>
<p>FWPS_LAYER_ALE_AUTH_CONNECT_V4</p>
<p>FWPS_LAYER_ALE_AUTH_CONNECT_V6</p>
</td>
<td>
<p>对于非 TCP 流量：传输标头的开头。</p>
<p>对于 TCP 流量：不适用。</p>
</td>
</tr>
<tr>
<td>
<p>FWPS_LAYER_ALE_AUTH_CONNECT_V4_DISCARD</p>
<p>FWPS_LAYER_ALE_AUTH_CONNECT_V6_DISCARD</p>
</td>
<td>
<p>对于非 TCP 流量：传输标头的开头。</p>
<p>对于 TCP 流量：不适用。</p>
</td>
</tr>
<tr>
<td>
<p>FWPS_LAYER_ALE_FLOW_ESTABLISHED_V4</p>
<p>FWPS_LAYER_ALE_FLOW_ESTABLISHED_V6</p>
</td>
<td>
<p>对于入站数据包方向：数据的开头。</p>
<div class="alert"><b>请注意</b>，  在 tcp/ip 堆栈的 icmp 套接字上收到的入站数据包，偏移量是 icmp 标头的开头。</div>
<div> </div>
<p>对于出站数据包方向：传输标头的开头。</p>
</td>
</tr>
<tr>
<td>
<p>FWPS_LAYER_ALE_FLOW_ESTABLISHED_V4_DISCARD</p>
<p>FWPS_LAYER_ALE_FLOW_ESTABLISHED_V6_DISCARD</p>
</td>
<td>
<p>对于入站数据包方向：数据的开头。</p>
<div class="alert"><b>请注意</b>，  在 tcp/ip 堆栈的 icmp 套接字上收到的入站数据包，偏移量是 icmp 标头的开头。</div>
<div> </div>
<p>对于出站数据包方向：传输标头的开头。
      </p>
</td>
</tr>
<tr>
<td>
<p>FWPS_LAYER_IPSEC_KM_DEMUX_V4</p>
<p>FWPS_LAYER_IPSEC_KM_DEMUX_V6</p>
</td>
<td>
<p>不适用。</p>
</td>
</tr>
<tr>
<td>
<p>FWPS_LAYER_IPSEC_V4</p>
<p>FWPS_LAYER_IPSEC_V6</p>
</td>
<td>
<p>不适用。</p>
</td>
</tr>
<tr>
<td>
<p>FWPS_LAYER_IKEEXT_V4</p>
<p>FWPS_LAYER_IKEEXT_V6</p>
</td>
<td>
<p>不适用。</p>
</td>
</tr>
<tr>
<td>
<p>FWPS_LAYER_RPC_UM</p>
</td>
<td>
<p>不适用。</p>
</td>
</tr>
<tr>
<td>
<p>FWPS_LAYER_RPC_EPMAP</p>
</td>
<td>
<p>不适用。</p>
</td>
</tr>
<tr>
<td>
<p>FWPS_LAYER_RPC_EP_ADD</p>
</td>
<td>
<p>不适用。</p>
</td>
</tr>
<tr>
<td>
<p>FWPS_LAYER_RPC_PROXY_CONN</p>
</td>
<td>
<p>不适用。</p>
</td>
</tr>
<tr>
<td>
<p>FWPS_LAYER_RPC_PROXY_IF</p>
</td>
<td>
<p>不适用。</p>
</td>
</tr>
<tr>
<th>运行时筛选层标识符（从 Windows 7 开始）</th>
<th>数据包数据中的位置</th>
</tr>
<tr>
<td>
<p>FWPS_LAYER_NAME_RESOLUTION_CACHE_V4</p>
<p>
FWPS_LAYER_NAME_RESOLUTION_CACHE_V6</p>
</td>
<td>
<p>不适用。</p>
</td>
</tr>
<tr>
<td>
<p>FWPS_LAYER_ALE_RESOURCE_RELEASE_V4</p>
<p>FWPS_LAYER_ALE_RESOURCE_RELEASE_V6</p>
</td>
<td>
<p>不适用。</p>
</td>
</tr>
<tr>
<td>
<p>FWPS_LAYER_ALE_ENDPOINT_CLOSURE_V4</p>
<p>FWPS_LAYER_ALE_ENDPOINT_CLOSURE_V6</p>
</td>
<td>
<p>不适用。</p>
</td>
</tr>
<tr>
<td>
<p>FWPS_LAYER_ALE_CONNECT_REDIRECT_V4</p>
<p>FWPS_LAYER_ALE_CONNECT_REDIRECT_V6</p>
</td>
<td>
<p>不适用。</p>
<div class="alert"><b>注意</b> 对于这些筛选层， <i><em>layerData</em></i>参数包含指向<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/ns-fwpsk-_fwps_connect_request0"><b>FWPS_CONNECT_REQUEST0</b></a>结构的指针。 此结构不引用描述数据包数据的<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list"><b>NET_BUFFER_LIST</b></a>结构。</div>
<div> </div>
</td>
</tr>
<tr>
<td>
<p>FWPS_LAYER_ALE_BIND_REDIRECT_V4</p>
<p>FWPS_LAYER_ALE_BIND_REDIRECT_V6</p>
</td>
<td>
<p>不适用。</p>
<div class="alert"><b>注意</b> 对于这些筛选层， <i><em>layerData</em></i>参数包含指向<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/ns-fwpsk-_fwps_bind_request0"><b>FWPS_BIND_REQUEST0</b></a>结构的指针。 此结构不引用描述数据包数据的<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list"><b>NET_BUFFER_LIST</b></a>结构。</div>
<div> </div>
</td>
</tr>
<tr>
<td>
<p>FWPS_LAYER_STREAM_PACKET_V4</p>
<p>FWPS_LAYER_STREAM_PACKET_V6</p>
</td>
<td>
<p>对于入站数据包方向：数据的开头。</p>
<p>对于出站数据包方向：传输标头的开头。</p>
</td>
</tr>
<tr>
<td>
<p>FWPS_LAYER_KM_AUTHORIZATION</p>
</td>
<td>
<p>不适用。</p>
</td>
</tr>
<tr>
<th>运行时筛选层标识符（从 Windows 8 开始）</th>
<th>数据包数据中的位置</th>
</tr>
<tr>
<td>
<p>FWPS_LAYER_INBOUND_MAC_FRAME_ETHERNET</p>
</td>
<td>
<p>IP 标头的开头。</p>
</td>
</tr>
<tr>
<td>
<p>FWPS_LAYER_OUTBOUND_MAC_FRAME_ETHERNET</p>
</td>
<td>
<p>MAC 标头的开头。</p>
</td>
</tr>
<tr>
<td>
<p>FWPS_LAYER_INBOUND_MAC_FRAME_NATIVE</p>
</td>
<td>
<p>MAC 标头的开头。</p>
</td>
</tr>
<tr>
<td>
<p>FWPS_LAYER_OUTBOUND_MAC_FRAME_NATIVE</p>
</td>
<td>
<p>MAC 标头的开头。</p>
</td>
</tr>
<tr>
<td>
<p>FWPS_LAYER_INGRESS_VSWITCH_ETHERNET</p>
</td>
<td>
<p>以太网标头的开头。</p>
</td>
</tr>
<tr>
<td>
<p>FWPS_LAYER_EGRESS_VSWITCH_ETHERNET</p>
</td>
<td>
<p>以太网标头的开头。</p>
</td>
</tr>
<tr>
<td>
<p>FWPS_LAYER_INGRESS_VSWITCH_TRANSPORT_V4</p>
</td>
<td>
<p>IP 标头的开头。</p>
</td>
</tr>
<tr>
<td>
<p>FWPS_LAYER_INGRESS_VSWITCH_TRANSPORT_V6</p>
</td>
<td>
<p>IP 标头的开头。</p>
</td>
</tr>
<tr>
<td>
<p>FWPS_LAYER_EGRESS_VSWITCH_TRANSPORT_V4</p>
</td>
<td>
<p>IP 标头的开头。</p>
</td>
</tr>
<tr>
<td>
<p>FWPS_LAYER_EGRESS_VSWITCH_TRANSPORT_V6</p>
</td>
<td>
<p>IP 标头的开头。</p>
</td>
</tr>
</table>

