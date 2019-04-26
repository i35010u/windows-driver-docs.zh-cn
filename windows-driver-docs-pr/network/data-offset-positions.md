---
title: 数据偏移位置
description: 本部分介绍 Windows 筛选平台标注驱动程序的数据偏移量的位置。
ms.assetid: cf4656cf-b978-4539-9fff-8f0aa5de1b5e
keywords:
- 数据偏移的位置的网络驱动程序
ms.date: 11/09/2017
ms.localizationpriority: medium
ms.openlocfilehash: 568d5f786aef4c385d5637babf6ff9741284d73a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63330191"
---
# <a name="data-offset-positions"></a>数据偏移位置

当筛选器引擎调用标注驱动程序[classifyFn](https://msdn.microsoft.com/library/windows/hardware/ff544890)标注函数，它将指针传递到一个结构*数据*参数。 对于筛选数据包数据层，该指针指向[NET_BUFFER_LIST](https://msdn.microsoft.com/library/windows/hardware/ff568388)结构。 具体取决于在其中筛选层*classifyFn*标注函数被调用时，筛选器引擎将指针数据 * 参数中传递给以下结构：

- 为流层*数据*参数包含一个指向[FWPS_STREAM_CALLOUT_IO_PACKET0](https://msdn.microsoft.com/library/windows/hardware/ff552417)结构。 此结构的 streamData 成员包含一个指向[FWPS_STREAM_DATA0](https://msdn.microsoft.com/library/windows/hardware/ff552419)结构。 

    **NetBufferListChain**的成员[FWPS_STREAM_DATA0](https://msdn.microsoft.com/library/windows/hardware/ff552419)结构包含一个指向[NET_BUFFER_LIST](https://msdn.microsoft.com/library/windows/hardware/ff568388)结构。 

- 对于所有其他层，*数据*参数包含一个指向[NET_BUFFER_LIST](https://msdn.microsoft.com/library/windows/hardware/ff568388)结构。

> [!NOTE]
> *数据*参数可以为 NULL，具体取决于要筛选的层和在其下的条件的驱动程序[classifyFn](https://msdn.microsoft.com/library/windows/hardware/ff544890)标注函数进行调用。
 
[NET_BUFFER_LIST](https://msdn.microsoft.com/library/windows/hardware/ff568388)结构中包含的链接的列表[NET_BUFFER](https://msdn.microsoft.com/library/windows/hardware/ff568376)结构。 内[NET_BUFFER_DATA](https://msdn.microsoft.com/library/windows/hardware/ff568381)结构的每个**NET_BUFFER**结构**DataOffset**成员指向的数据包数据中的特定位置。 位置的**DataOffset**成员指向取决于筛选的筛选器引擎将调用标注驱动程序的一层*classifyFn*标注函数。 

对于每个筛选层，由指定的数据包数据中的位置**DataOffset**成员定义，如下所示：

<table>
<tr>
<th>运行时筛选层标识符 （从 Windows Vista 开始）</th>
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
<p>TCP/IP 堆栈的位置的偏移量已停止处理。</p>
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
<p>TCP/IP 堆栈的位置的偏移量已停止处理。</p>
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
<p>数据的起始处。</p>
<div class="alert"><b>请注意</b>  对于 TCP/IP 堆栈 ICMP 套接字上接收到的入站数据包，偏移量是 ICMP 标头的开头。</div>
<div> </div>
</td>
</tr>
<tr>
<td>
<p>FWPS_LAYER_INBOUND_TRANSPORT_V4_DISCARD</p>
<p>FWPS_LAYER_INBOUND_TRANSPORT_V6_DISCARD</p>
</td>
<td>
<p>数据的起始处。</p>
<div class="alert"><b>请注意</b>  对于 TCP/IP 堆栈 ICMP 套接字上接收到的入站数据包，偏移量是 ICMP 标头的开头。</div>
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
<p>数据的起始处。</p>
<div class="alert"><b>请注意</b>  数据包数据中的位置包含没有 IP、 IPv6 和的传输标头。</div>
<div> </div>
</td>
</tr>
<tr>
<td>
<p>FWPS_LAYER_STREAM_V4_DISCARD</p>
<p>FWPS_LAYER_STREAM_V6_DISCARD</p>
</td>
<td>
<p>数据的起始处。</p>
<div class="alert"><b>请注意</b>  数据包数据中的位置不包含任何 IP、 IPv6 或传输标头。</div>
<div> </div>
</td>
</tr>
<tr>
<td>
<p>FWPS_LAYER_DATAGRAM_DATA_V4</p>
<p>FWPS_LAYER_DATAGRAM_DATA_V6</p>
</td>
<td>
<p>为入站数据报：数据的起始处。</p>
<div class="alert"><b>请注意</b>  对于 TCP/IP 堆栈 ICMP 套接字上接收到的入站数据包，偏移量是 ICMP 标头的开头。</div>
<div> </div>
<p>为出站数据报：传输标头的开头。</p>
</td>
</tr>
<tr>
<td>
<p>FWPS_LAYER_DATAGRAM_DATA_V4_DISCARD</p>
<p>FWPS_LAYER_DATAGRAM_DATA_V6_DISCARD</p>
</td>
<td>
<p>为入站数据报：数据的起始处。</p>
<div class="alert"><b>请注意</b>  对于 TCP/IP 堆栈 ICMP 套接字上接收到的入站数据包，偏移量是 ICMP 标头的开头。</div>
<div> </div>
<p>为出站数据报：传输标头的开头。</p>
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
<p>对于入站的数据包的方向：数据的起始处。</p>
<div class="alert"><b>请注意</b>  对于 TCP/IP 堆栈 ICMP 套接字上接收到的入站数据包，偏移量是 ICMP 标头的开头。</div>
<div> </div>
<p>对于出站数据包的方向：传输标头的开头。</p>
</td>
</tr>
<tr>
<td>
<p>FWPS_LAYER_ALE_AUTH_RECV_ACCEPT_V4_DISCARD</p>
<p>FWPS_LAYER_ALE_AUTH_RECV_ACCEPT_V6_DISCARD</p>
</td>
<td>
<p>对于入站的数据包的方向：数据的起始处。</p>
<div class="alert"><b>请注意</b>  对于 TCP/IP 堆栈 ICMP 套接字上接收到的入站数据包，偏移量是 ICMP 标头的开头。</div>
<div> </div>
<p>对于出站数据包的方向：传输标头的开头。</p>
</td>
</tr>
<tr>
<td>
<p>FWPS_LAYER_ALE_AUTH_CONNECT_V4</p>
<p>FWPS_LAYER_ALE_AUTH_CONNECT_V6</p>
</td>
<td>
<p>为非 TCP 流量：传输标头的开头。</p>
<p>TCP 流量：不适用。</p>
</td>
</tr>
<tr>
<td>
<p>FWPS_LAYER_ALE_AUTH_CONNECT_V4_DISCARD</p>
<p>FWPS_LAYER_ALE_AUTH_CONNECT_V6_DISCARD</p>
</td>
<td>
<p>为非 TCP 流量：传输标头的开头。</p>
<p>TCP 流量：不适用。</p>
</td>
</tr>
<tr>
<td>
<p>FWPS_LAYER_ALE_FLOW_ESTABLISHED_V4</p>
<p>FWPS_LAYER_ALE_FLOW_ESTABLISHED_V6</p>
</td>
<td>
<p>对于入站的数据包的方向：数据的起始处。</p>
<div class="alert"><b>请注意</b>  对于 TCP/IP 堆栈 ICMP 套接字上接收到的入站数据包，偏移量是 ICMP 标头的开头。</div>
<div> </div>
<p>对于出站数据包的方向：传输标头的开头。</p>
</td>
</tr>
<tr>
<td>
<p>FWPS_LAYER_ALE_FLOW_ESTABLISHED_V4_DISCARD</p>
<p>FWPS_LAYER_ALE_FLOW_ESTABLISHED_V6_DISCARD</p>
</td>
<td>
<p>对于入站的数据包的方向：数据的起始处。</p>
<div class="alert"><b>请注意</b>  对于 TCP/IP 堆栈 ICMP 套接字上接收到的入站数据包，偏移量是 ICMP 标头的开头。</div>
<div> </div>
<p>对于出站数据包的方向：传输标头的开头。
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
<th>运行时筛选层标识符 （从 Windows 7 开始）</th>
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
<div class="alert"><b>请注意</b>筛选层，这些<i><em>数据</em></i>参数包含一个指向<a href="https://msdn.microsoft.com/library/windows/hardware/ff551231"> <b>FWPS_CONNECT_REQUEST0</b> </a>结构。 此结构不引用<a href="https://msdn.microsoft.com/library/windows/hardware/ff568388"> <b>NET_BUFFER_LIST</b> </a>描述包的数据结构。</div>
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
<div class="alert"><b>请注意</b>筛选层，这些<i><em>数据</em></i>参数包含一个指向<a href="https://msdn.microsoft.com/library/windows/hardware/ff551221"> <b>FWPS_BIND_REQUEST0</b> </a>结构。 此结构不引用<a href="https://msdn.microsoft.com/library/windows/hardware/ff568388"> <b>NET_BUFFER_LIST</b> </a>描述包的数据结构。</div>
<div> </div>
</td>
</tr>
<tr>
<td>
<p>FWPS_LAYER_STREAM_PACKET_V4</p>
<p>FWPS_LAYER_STREAM_PACKET_V6</p>
</td>
<td>
<p>对于入站的数据包的方向：数据的起始处。</p>
<p>对于出站数据包的方向：传输标头的开头。</p>
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
<th>运行时筛选层标识符 （从 Windows 8 开始）</th>
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

