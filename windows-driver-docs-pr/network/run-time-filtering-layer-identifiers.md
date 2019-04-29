---
title: 运行时筛选层标识符
description: 本部分介绍运行时筛选层标识符。
ms.assetid: 21c466a3-cdfc-4e94-83d3-1c2c7a58a2ca
keywords:
- 运行时筛选层标识符网络驱动程序
ms.date: 11/08/2017
ms.localizationpriority: medium
ms.openlocfilehash: 091079e2f5f170fcc139fcac724d7a8990ecabc5
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63386202"
---
# <a name="run-time-filtering-layer-identifiers"></a>运行时筛选层标识符

运行时筛选层标识符由内核模式标注驱动程序和为每个所表示的本地唯一标识符 ([LUID](https://msdn.microsoft.com/library/windows/hardware/ff557080))，这是 64 位大小。 这些标识符是 Fwpsk.h 中定义的 FWPS_BUILTIN_LAYERS 枚举中的常量值。 这些标识符定义，如下所示：

> [!NOTE]
> 在运行时层标识符末尾的 V4 和 v6 上后缀表示层是否位于 IPv4 网络堆栈中或 IPv6 网络堆栈中。

| 运行时筛选层标识符 | 筛选层说明 |
| --- | --- |
| <p>FWPS_LAYER_INBOUND_IPPACKET_V4</p><p>FWPS_LAYER_INBOUND_IPPACKET_V6</p> | 已分析的接收的数据包 IP 标头后，此筛选层位于接收路径中，但在处理所需的任何 IP 标头之前放置。 不发生任何 IPsec 解密或重新组合。 |
| <p>FWPS_LAYER_INBOUND_IPPACKET_V4_DISCARD</p><p>FWPS_LAYER_INBOUND_IPPACKET_V6_DISCARD</p> | 此筛选层位于处理已放弃在网络层的任何接收的数据包的接收路径中。 |
| <p>FWPS_LAYER_OUTBOUND_IPPACKET_V4</p><p>FWPS_LAYER_OUTBOUND_IPPACKET_V6</p> | 此筛选层位于发送路径之前发送的数据包进行评估的碎片。 所有 IP 标头处理都已完成，所有扩展标头都均已到位。 已发生的任何 IPsec 身份验证和加密。 |
| <p>FWPS_LAYER_OUTBOUND_IPPACKET_V4_DISCARD</p><p>FWPS_LAYER_OUTBOUND_IPPACKET_V6_DISCARD</p> | 此筛选层位于处理已放弃在网络层的任何发送的数据包的发送路径中。 |
| <p>FWPS_LAYER_IPFORWARD_V4</p><p>FWPS_LAYER_IPFORWARD_V6</p> | 此筛选层位于在其中接收的数据包将转发的点转发路径中。 |
| <p>FWPS_LAYER_IPFORWARD_V4_DISCARD</p><p>FWPS_LAYER_IPFORWARD_V6_DISCARD</p> | 此筛选层位于用于处理在正向层已放弃的任何转发的数据包转发路径中。 |
| <p>FWPS_LAYER_INBOUND_TRANSPORT_V4</p><p>FWPS_LAYER_INBOUND_TRANSPORT_V6</p> | 此筛选层位于接收路径后接收的数据包的标头已分析由网络堆栈在传输层上，但在任何传输层之前处理将会发生。 |
| <p>FWPS_LAYER_INBOUND_TRANSPORT_V4_DISCARD</p><p>FWPS_LAYER_INBOUND_TRANSPORT_V6_DISCARD</p> | 此筛选层位于处理任何接收到的数据包在传输层已丢弃的接收路径中。 |
| <p>FWPS_LAYER_OUTBOUND_TRANSPORT_V4</p><p>FWPS_LAYER_OUTBOUND_TRANSPORT_V6</p> | <p>此筛选层位于发送路径之后发送的数据包已传递到网络层进行处理，但之前的任何网络层处理将会发生。</p><p>此筛选层位于底部的传输层而不是网络层的顶部，以便由第三方传输或以原始数据包的形式发送任何数据包筛选在此层上。</p> |
| <p>FWPS_LAYER_OUTBOUND_TRANSPORT_V4_DISCARD</p><p>FWPS_LAYER_OUTBOUND_TRANSPORT_V6_DISCARD</p> | 此筛选层位于处理已放弃在传输层的任何发送的数据包的发送路径中。 |
| <p>FWPS_LAYER_STREAM_V4</p><p>FWPS_LAYER_STREAM_V6</p> | 此筛选层位于流数据路径中。 此层允许用于处理在每个流的基础上的网络数据。 在流层的网络数据是双向的。 |
| <p>FWPS_LAYER_STREAM_V4_DISCARD</p><p>FWPS_LAYER_STREAM_V6_DISCARD</p> | 此筛选层保留供将来使用。 |
| <p>FWPS_LAYER_DATAGRAM_DATA_V4</p><p>FWPS_LAYER_DATAGRAM_DATA_V6</p> | 此筛选层位于数据报数据路径中。 此层允许用于处理在每个数据报的基础上的网络数据。 在数据报层上，网络数据是双向的。 |
| <p>FWPS_LAYER_DATAGRAM_DATA_V4_DISCARD</p><p>FWPS_LAYER_DATAGRAM_DATA_V6_DISCARD</p> | 此筛选层位于处理任何数据报的已丢弃的数据报数据路径。 |
| <p>FWPS_LAYER_INBOUND_ICMP_ERROR_V4</p><p>FWPS_LAYER_INBOUND_ICMP_ERROR_V6</p> | 此筛选层位于处理接收的 ICMP 消息的传输协议的接收路径中。 |
| <p>FWPS_LAYER_INBOUND_ICMP_ERROR_V4_DISCARD</p><p>FWPS_LAYER_INBOUND_ICMP_ERROR_V6_DISCARD</p> | 此筛选层位于已放弃的处理收到 ICMP 消息的接收路径中。 |
| <p>FWPS_LAYER_OUTBOUND_ICMP_ERROR_V4</p><p>FWPS_LAYER_OUTBOUND_ICMP_ERROR_V6</p> | 此筛选层位于处理发送的 ICMP 消息的传输协议的发送路径中。 |
| <p>FWPS_LAYER_OUTBOUND_ICMP_ERROR_V4_DISCARD</p><p>FWPS_LAYER_OUTBOUND_ICMP_ERROR_V6_DISCARD</p> | 此筛选层位于处理发送的已丢弃 ICMP 消息的发送路径中。 |
| <p>FWPS_LAYER_ALE_RESOURCE_ASSIGNMENT_V4</p><p>FWPS_LAYER_ALE_RESOURCE_ASSIGNMENT_V6</p> | 此筛选层允许授权传输端口分配、 绑定请求、 混杂模式请求和 raw 模式请求。 |
| <p>FWPS_LAYER_ALE_RESOURCE_ASSIGNMENT_V4_DISCARD</p><p>FWPS_LAYER_ALE_RESOURCE_ASSIGNMENT_V6_DISCARD</p> | 此筛选层允许处理以下丢弃项： 传输端口分配，请将绑定请求、 混杂模式请求和 raw 模式请求。 |
| <p>FWPS_LAYER_ALE_AUTH_LISTEN_V4</p><p>FWPS_LAYER_ALE_AUTH_LISTEN_V6</p> | 此筛选层允许授权 TCP 侦听请求。 |
| <p>FWPS_LAYER_ALE_AUTH_LISTEN_V4_DISCARD</p><p>FWPS_LAYER_ALE_AUTH_LISTEN_V6_DISCARD</p> | 此筛选层允许 TCP 侦听已丢弃的请求处理。 |
| <p>FWPS_LAYER_ALE_AUTH_RECV_ACCEPT_V4</p><p>FWPS_LAYER_ALE_AUTH_RECV_ACCEPT_V6</p> | 此筛选层允许将用于授权接受请求的传入 TCP 连接，以及根据收到的第一个数据包的授权传入非 TCP 流量。 |
| <p>FWPS_LAYER_ALE_AUTH_RECV_ACCEPT_V4_DISCARD</p><p>FWPS_LAYER_ALE_AUTH_RECV_ACCEPT_V6_DISCARD</p> | 此筛选层允许将用于处理接受的以及处理已丢弃的传入非 TCP 流量授权，已丢弃的传入 TCP 连接请求。 |
| <p>FWPS_LAYER_ALE_AUTH_CONNECT_V4</p><p>FWPS_LAYER_ALE_AUTH_CONNECT_V6</p> | 此筛选层允许授权连接请求的传出 TCP 连接，以及授权传出非 TCP 流量基于发送的第一个数据包。 |
| <p>FWPS_LAYER_ALE_AUTH_CONNECT_V4_DISCARD</p><p>FWPS_LAYER_ALE_AUTH_CONNECT_V6_DISCARD</p> | 此筛选层允许将用于处理连接请求的传出 TCP 连接已丢弃，以及处理传出的非 TCP 流量已放弃的授权。 |
| <p>FWPS_LAYER_ALE_FLOW_ESTABLISHED_V4</p><p>FWPS_LAYER_ALE_FLOW_ESTABLISHED_V6</p> | 此筛选层允许时建立 TCP 连接，或非 TCP 流量授权时的通知。 |
| <p>FWPS_LAYER_ALE_FLOW_ESTABLISHED_V4_DISCARD</p><p>FWPS_LAYER_ALE_FLOW_ESTABLISHED_V6_DISCARD</p> | 此筛选层进行处理时建立的 TCP 连接已被丢弃在建立流层上，以及当获得授权时允许非 TCP 流量已被丢弃在建立流层。 |
| <p>FWPS_LAYER_RESERVED1_V4</p><p>FWPS_LAYER_RESERVED1_V6</p> | 不支持此筛选层。 |
| <p>FWPS_LAYER_NAME_RESOLUTION_CACHE_V4</p><p>FWPS_LAYER_NAME_RESOLUTION_CACHE_V6</p> | 此筛选层允许用于查询系统最近解析的名称。 |
| <p>FWPS_LAYER_ALE_RESOURCE_RELEASE_V4</p><p>FWPS_LAYER_ALE_RESOURCE_RELEASE_V6</p> | 这个机会，将使用此筛选层以回收标注驱动程序中的任何 ALE_RESOURCE_ASSIGNMENT 层分配的资源。 |
| <p>FWPS_LAYER_ALE_ENDPOINT_CLOSURE_V4</p><p>FWPS_LAYER_ALE_ENDPOINT_CLOSURE_V6</p> | 这个机会，将使用此筛选层以回收标注驱动程序中的任何 ALE_AUTH_CONNECT 或 ALE_AUTH_RECV_ACCEPT 层分配的资源。 |
| <p>FWPS_LAYER_ALE_CONNECT_REDIRECT_V4</p><p>FWPS_LAYER_ALE_CONNECT_REDIRECT_V6</p> | 此筛选层允许的重定向的连接请求到不同的 IPV4 / IPV6 地址和 TCP/UDP 端口。 |
| <p>FWPS_LAYER_ALE_BIND_REDIRECT_V4</p><p>FWPS_LAYER_ALE_BIND_REDIRECT_V6</p> | 此筛选层允许的重定向的绑定请求到不同的本地 IPV4 / IPV6 地址和/或本地 TCP/UDP 端口。 |
| FWPS_LAYER_INBOUND_MAC_FRAME_ETHERNET | 此筛选层允许用于检查在入站 （到 NDIS 协议驱动程序） 较低层的 MAC 帧数据。 **注意**：仅适用于 Windows 8 及更高版本。 |
| FWPS_LAYER_OUTBOUND_MAC_FRAME_ETHERNET | 此筛选层允许用于检查在出站的上限 （到 NDIS 协议驱动程序） 层的 MAC 帧数据。 **注意**：仅适用于 Windows 8 及更高版本。 |
| FWPS_LAYER_INBOUND_MAC_FRAME_NATIVE | 此筛选层允许用于检查在入站 （到 NDIS 微型端口驱动程序） 较低层的 MAC 帧数据。 **注意**：仅适用于 Windows 8 及更高版本。 |
| FWPS_LAYER_OUTBOUND_MAC_FRAME_NATIVE | 此筛选层允许用于检查在出站 （到 NDIS 微型端口驱动程序） 较低层的 MAC 帧数据。 **注意**：仅适用于 Windows 8 及更高版本。 |
| FWPS_LAYER_INGRESS_VSWITCH_ETHERNET | 此筛选层允许用于检查 HYPER-V 可扩展交换机的入口 802.3 数据。 **注意**：仅适用于 Windows 8 及更高版本。 |
| FWPS_LAYER_EGRESS_VSWITCH_ETHERNET | 此筛选层允许用于检查 HYPER-V 可扩展交换机的出口 802.3 数据。 **注意**：仅适用于 Windows 8 及更高版本。 |
| <p>FWPS_LAYER_INGRESS_VSWITCH_TRANSPORT_V4</p><p>FWPS_LAYER_INGRESS_VSWITCH_TRANSPORT_V6</p> | 此筛选层允许用于检查 HYPER-V 可扩展交换机的入口传输数据。 **注意**：仅适用于 Windows 8 及更高版本。 |
| <p>FWPS_LAYER_EGRESS_VSWITCH_TRANSPORT_V4</p><p>FWPS_LAYER_EGRESS_VSWITCH_TRANSPORT_V6</p> | 此筛选层允许用于检查 HYPER-V 可扩展交换机的出口传输数据。 **注意**：仅适用于 Windows 8 及更高版本。 |
| <p>FWPS_LAYER_STREAM_PACKET_V4</p><p>FWPS_LAYER_STREAM_PACKET_V6</p> | 此筛选层允许网络上的数据的每个 TCP 数据包基础，包括握手和流控制交换的检查。 在流数据包层上，网络数据是双向的。 |
| <p>FWPS_LAYER_IPSEC_KM_DEMUX_V4</p><p>FWPS_LAYER_IPSEC_KM_DEMUX_V6</p> | 此筛选层用于确定哪些密钥模块在本地系统发起方时调用。 这是用户模式下筛选层。 |
| <p>FWPS_LAYER_IPSEC_V4</p><p>FWPS_LAYER_IPSEC_V6</p> | 此筛选层允许密钥的模块，若要查看快速模式策略信息的协商快速模式安全关联时。 这是用户模式下筛选层。 |
| <p>FWPS_LAYER_IKEEXT_V4</p><p>FWPS_LAYER_IKEEXT_V6</p> | 此筛选层允许 IKE，经过身份验证 IP 模块协商主模式安全关联时查看主模式策略信息。 这是用户模式下筛选层。 |
| FWPS_LAYER_RPC_UM | 此筛选层允许用于检查在用户模式下可用的 RPC 数据字段。 这是用户模式下筛选层。 |
| FWPS_LAYER_RPC_EPMAP | 此筛选层允许用于检查在终结点解析过程会在用户模式下可用的 RPC 数据字段。 这是用户模式下筛选层。 |
| FWPS_LAYER_RPC_EP_ADD | 此筛选层允许用于检查 RPC 数据字段时添加新的终结点在用户模式下可用的。 这是用户模式下筛选层。 |
| FWPS_LAYER_RPC_PROXY_CONN | 此筛选层允许用于检查 RpcProxy 连接请求。 这是用户模式下筛选层。 |
| FWPS_LAYER_RPC_PROXY_IF | 此筛选层允许用于检查 RpcProxy 连接时使用的接口。 这是用户模式下筛选层。 |
| FWPS_LAYER_KM_AUTHORIZATION | 此筛选层允许授权建立安全关联。 |

每个运行时层标识符具有关联的运行时数据字段标识符表示的一组常量值。 这些数据字段标识符被声明为中 Fwpsk.h FWPS_FIELDS_XXX 枚举。 有关详细信息，请参阅[数据字段标识符](https://msdn.microsoft.com/library/windows/hardware/ff546312)。

