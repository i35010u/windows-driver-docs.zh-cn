---
title: 运行时筛选层标识符
description: 本部分介绍运行时筛选层标识符。
ms.assetid: 21c466a3-cdfc-4e94-83d3-1c2c7a58a2ca
keywords:
- 运行时筛选层标识符网络驱动程序
ms.date: 11/08/2017
ms.localizationpriority: medium
ms.openlocfilehash: 682b0e92f9a1707de00e7363acdc4d4e709c6785
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89217483"
---
# <a name="run-time-filtering-layer-identifiers"></a>运行时筛选层标识符

运行时筛选层标识符由内核模式标注驱动程序使用，每个标识符由本地唯一标识符 ([LUID](/windows-hardware/drivers/ddi/igpupvdev/ns-igpupvdev-_luid)) （大小为64位）。 这些标识符是 Fwpsk 中定义的 FWPS_BUILTIN_LAYERS 枚举中的常量值。 这些标识符定义如下：

> [!NOTE]
> 运行时层标识符结尾的 V4 和 V6 后缀指示该层是位于 IPv4 网络堆栈中还是位于 IPv6 网络堆栈中。

| 运行时筛选层标识符 | 筛选层描述 |
| --- | --- |
| <p>FWPS_LAYER_INBOUND_IPPACKET_V4</p><p>FWPS_LAYER_INBOUND_IPPACKET_V6</p> | 此筛选层位于接收路径中，刚好在分析收到的数据包的 IP 标头之后、发生任何 IP 标头处理之前。 未发生 IPsec 解密或重新组合。 |
| <p>FWPS_LAYER_INBOUND_IPPACKET_V4_DISCARD</p><p>FWPS_LAYER_INBOUND_IPPACKET_V6_DISCARD</p> | 此筛选层位于接收路径中，用于处理已在网络层丢弃的任何已接收的数据包。 |
| <p>FWPS_LAYER_OUTBOUND_IPPACKET_V4</p><p>FWPS_LAYER_OUTBOUND_IPPACKET_V6</p> | 此筛选层位于发送路径中，刚好在对发送的数据包进行碎片计算之前。 所有 IP 标头处理已完成，并且所有扩展标头都已准备就绪。 已进行 IPsec 身份验证和加密。 |
| <p>FWPS_LAYER_OUTBOUND_IPPACKET_V4_DISCARD</p><p>FWPS_LAYER_OUTBOUND_IPPACKET_V6_DISCARD</p> | 此筛选层位于发送路径中，用于处理已在网络层丢弃的任何已发送的数据包。 |
| <p>FWPS_LAYER_IPFORWARD_V4</p><p>FWPS_LAYER_IPFORWARD_V6</p> | 此筛选层位于转发路径中接收的数据包转发到的位置。 |
| <p>FWPS_LAYER_IPFORWARD_V4_DISCARD</p><p>FWPS_LAYER_IPFORWARD_V6_DISCARD</p> | 此筛选层位于转发路径中，用于处理已在转发层上丢弃的任何转发的数据包。 |
| <p>FWPS_LAYER_INBOUND_TRANSPORT_V4</p><p>FWPS_LAYER_INBOUND_TRANSPORT_V6</p> | 在传输层上的网络堆栈对接收的数据包标头进行分析后，但在发生任何传输层处理之前，此筛选层位于接收路径中。 |
| <p>FWPS_LAYER_INBOUND_TRANSPORT_V4_DISCARD</p><p>FWPS_LAYER_INBOUND_TRANSPORT_V6_DISCARD</p> | 此筛选层位于接收路径中，用于处理在传输层被丢弃的任何已接收的数据包。 |
| <p>FWPS_LAYER_OUTBOUND_TRANSPORT_V4</p><p>FWPS_LAYER_OUTBOUND_TRANSPORT_V6</p> | <p>此筛选层位于发送路径中，就在发送的数据包被传递到网络层以进行处理，但在发生任何网络层处理之前。</p><p>此筛选层位于网络层的顶部，而不是位于传输层的底部，以便第三方传输或原始数据包发送的任何数据包都在此层上进行筛选。</p> |
| <p>FWPS_LAYER_OUTBOUND_TRANSPORT_V4_DISCARD</p><p>FWPS_LAYER_OUTBOUND_TRANSPORT_V6_DISCARD</p> | 此筛选层位于发送路径中，用于处理在传输层被丢弃的任何已发送的数据包。 |
| <p>FWPS_LAYER_STREAM_V4</p><p>FWPS_LAYER_STREAM_V6</p> | 此筛选层位于流数据路径中。 此层允许每个流处理网络数据。 在流层，网络数据是双向的。 |
| <p>FWPS_LAYER_STREAM_V4_DISCARD</p><p>FWPS_LAYER_STREAM_V6_DISCARD</p> | 此筛选层保留供将来使用。 |
| <p>FWPS_LAYER_DATAGRAM_DATA_V4</p><p>FWPS_LAYER_DATAGRAM_DATA_V6</p> | 此筛选层位于数据报数据路径中。 此层允许按照每个数据报来处理网络数据。 在数据报层，网络数据是双向的。 |
| <p>FWPS_LAYER_DATAGRAM_DATA_V4_DISCARD</p><p>FWPS_LAYER_DATAGRAM_DATA_V6_DISCARD</p> | 此筛选层位于数据报数据路径中，用于处理任何已丢弃的数据报。 |
| <p>FWPS_LAYER_INBOUND_ICMP_ERROR_V4</p><p>FWPS_LAYER_INBOUND_ICMP_ERROR_V6</p> | 此筛选层位于接收路径中，用于处理传输协议的已接收 ICMP 消息。 |
| <p>FWPS_LAYER_INBOUND_ICMP_ERROR_V4_DISCARD</p><p>FWPS_LAYER_INBOUND_ICMP_ERROR_V6_DISCARD</p> | 此筛选层位于接收路径中，用于处理已被丢弃的已接收 ICMP 消息。 |
| <p>FWPS_LAYER_OUTBOUND_ICMP_ERROR_V4</p><p>FWPS_LAYER_OUTBOUND_ICMP_ERROR_V6</p> | 此筛选层位于用于处理传输协议的已发送 ICMP 消息的发送路径中。 |
| <p>FWPS_LAYER_OUTBOUND_ICMP_ERROR_V4_DISCARD</p><p>FWPS_LAYER_OUTBOUND_ICMP_ERROR_V6_DISCARD</p> | 此筛选层位于发送路径中，用于处理已丢弃的已发送的 ICMP 消息。 |
| <p>FWPS_LAYER_ALE_RESOURCE_ASSIGNMENT_V4</p><p>FWPS_LAYER_ALE_RESOURCE_ASSIGNMENT_V6</p> | 此筛选层允许授权传输端口分配、绑定请求、混杂模式请求和 raw 模式请求。 |
| <p>FWPS_LAYER_ALE_RESOURCE_ASSIGNMENT_V4_DISCARD</p><p>FWPS_LAYER_ALE_RESOURCE_ASSIGNMENT_V6_DISCARD</p> | 此筛选层允许处理以下丢弃的项：传输端口分配、绑定请求、混杂模式请求和 raw 模式请求。 |
| <p>FWPS_LAYER_ALE_AUTH_LISTEN_V4</p><p>FWPS_LAYER_ALE_AUTH_LISTEN_V6</p> | 此筛选层允许授权 TCP 侦听请求。 |
| <p>FWPS_LAYER_ALE_AUTH_LISTEN_V4_DISCARD</p><p>FWPS_LAYER_ALE_AUTH_LISTEN_V6_DISCARD</p> | 此筛选层允许处理已丢弃的 TCP 侦听请求。 |
| <p>FWPS_LAYER_ALE_AUTH_RECV_ACCEPT_V4</p><p>FWPS_LAYER_ALE_AUTH_RECV_ACCEPT_V6</p> | 此筛选层允许向传入的 TCP 连接授权接受请求，并根据收到的第一个数据包授权传入的非 TCP 流量。 |
| <p>FWPS_LAYER_ALE_AUTH_RECV_ACCEPT_V4_DISCARD</p><p>FWPS_LAYER_ALE_AUTH_RECV_ACCEPT_V6_DISCARD</p> | 此筛选层允许处理已丢弃的传入 TCP 连接的接受请求，以及处理已丢弃的传入非 TCP 流量的授权。 |
| <p>FWPS_LAYER_ALE_AUTH_CONNECT_V4</p><p>FWPS_LAYER_ALE_AUTH_CONNECT_V6</p> | 此筛选层允许为传出 TCP 连接授权连接请求，并根据发送的第一个数据包授权传出的非 TCP 流量。 |
| <p>FWPS_LAYER_ALE_AUTH_CONNECT_V4_DISCARD</p><p>FWPS_LAYER_ALE_AUTH_CONNECT_V6_DISCARD</p> | 此筛选层允许处理已丢弃的传出 TCP 连接的连接请求，并为已丢弃的传出非 TCP 流量处理授权。 |
| <p>FWPS_LAYER_ALE_FLOW_ESTABLISHED_V4</p><p>FWPS_LAYER_ALE_FLOW_ESTABLISHED_V6</p> | 如果已建立 TCP 连接，或者未授权 TCP 流量，则可以使用此筛选层通知。 |
| <p>FWPS_LAYER_ALE_FLOW_ESTABLISHED_V4_DISCARD</p><p>FWPS_LAYER_ALE_FLOW_ESTABLISHED_V6_DISCARD</p> | 当已建立的 TCP 连接在流建立的层上被丢弃时，以及在流建立的层上已放弃授权的非 TCP 流量时，此筛选层允许处理。 |
| <p>FWPS_LAYER_RESERVED1_V4</p><p>FWPS_LAYER_RESERVED1_V6</p> | 此筛选层不受支持。 |
| <p>FWPS_LAYER_NAME_RESOLUTION_CACHE_V4</p><p>FWPS_LAYER_NAME_RESOLUTION_CACHE_V6</p> | 此筛选层允许查询系统最近解析的名称。 |
| <p>FWPS_LAYER_ALE_RESOURCE_RELEASE_V4</p><p>FWPS_LAYER_ALE_RESOURCE_RELEASE_V6</p> | 此筛选层用于回收由任意 ALE_RESOURCE_ASSIGNMENT 层中的标注驱动程序所分配的资源。 |
| <p>FWPS_LAYER_ALE_ENDPOINT_CLOSURE_V4</p><p>FWPS_LAYER_ALE_ENDPOINT_CLOSURE_V6</p> | 此筛选层用于回收 ALE_AUTH_CONNECT 或 ALE_AUTH_RECV_ACCEPT 层中的标注驱动程序所分配的资源。 |
| <p>FWPS_LAYER_ALE_CONNECT_REDIRECT_V4</p><p>FWPS_LAYER_ALE_CONNECT_REDIRECT_V6</p> | 此筛选层允许将连接请求重定向到另一个 IPV4/IPV6 地址和 TCP/UDP 端口。 |
| <p>FWPS_LAYER_ALE_BIND_REDIRECT_V4</p><p>FWPS_LAYER_ALE_BIND_REDIRECT_V6</p> | 此筛选层允许将绑定请求重定向到不同的本地 IPV4/IPV6 地址和/或本地 TCP/UDP 端口。 |
| FWPS_LAYER_INBOUND_MAC_FRAME_ETHERNET | 此筛选层允许将入站下限 (的 MAC 帧数据检查到 NDIS 协议驱动程序) 层。 **注意**：仅在 Windows 8 和更高版本上可用。 |
| FWPS_LAYER_OUTBOUND_MAC_FRAME_ETHERNET | 此筛选层允许将出站上限 (的 MAC 帧数据检查到 NDIS 协议驱动程序) 层。 **注意**：仅在 Windows 8 和更高版本上可用。 |
| FWPS_LAYER_INBOUND_MAC_FRAME_NATIVE | 此筛选层允许将入站下限 (的 MAC 帧数据检查到 NDIS 微型端口驱动程序) 层。 **注意**：仅在 Windows 8 和更高版本上可用。 |
| FWPS_LAYER_OUTBOUND_MAC_FRAME_NATIVE | 此筛选层允许将出站下 (的 MAC 帧数据检查到 NDIS 微型端口驱动程序) 层。 **注意**：仅在 Windows 8 和更高版本上可用。 |
| FWPS_LAYER_INGRESS_VSWITCH_ETHERNET | 此筛选层允许检查 Hyper-v 可扩展交换机的入口802.3 数据。 **注意**：仅在 Windows 8 和更高版本上可用。 |
| FWPS_LAYER_EGRESS_VSWITCH_ETHERNET | 此筛选层允许检查 Hyper-v 可扩展交换机的出口802.3 数据。 **注意**：仅在 Windows 8 和更高版本上可用。 |
| <p>FWPS_LAYER_INGRESS_VSWITCH_TRANSPORT_V4</p><p>FWPS_LAYER_INGRESS_VSWITCH_TRANSPORT_V6</p> | 此筛选层允许检查 Hyper-v 可扩展交换机的入口传输数据。 **注意**：仅在 Windows 8 和更高版本上可用。 |
| <p>FWPS_LAYER_EGRESS_VSWITCH_TRANSPORT_V4</p><p>FWPS_LAYER_EGRESS_VSWITCH_TRANSPORT_V6</p> | 此筛选层允许检查 Hyper-v 可扩展交换机的出口传输数据。 **注意**：仅在 Windows 8 和更高版本上可用。 |
| <p>FWPS_LAYER_STREAM_PACKET_V4</p><p>FWPS_LAYER_STREAM_PACKET_V6</p> | 此筛选层允许按 TCP 数据包（包括握手和流控制交换）检查网络数据。 在流数据包层，网络数据是双向的。 |
| <p>FWPS_LAYER_IPSEC_KM_DEMUX_V4</p><p>FWPS_LAYER_IPSEC_KM_DEMUX_V6</p> | 此筛选层用于确定本地系统为发起方时要调用的密钥模块。 这是用户模式筛选层。 |
| <p>FWPS_LAYER_IPSEC_V4</p><p>FWPS_LAYER_IPSEC_V6</p> | 此筛选层允许键控模块在协商快速模式安全关联时查找快速模式策略信息。 这是用户模式筛选层。 |
| <p>FWPS_LAYER_IKEEXT_V4</p><p>FWPS_LAYER_IKEEXT_V6</p> | 在协商主模式安全关联时，此筛选层允许 IKE 和经过身份验证的 IP 模块查找主模式策略信息。 这是用户模式筛选层。 |
| FWPS_LAYER_RPC_UM | 此筛选层允许检查用户模式下提供的 RPC 数据字段。 这是用户模式筛选层。 |
| FWPS_LAYER_RPC_EPMAP | 此筛选层允许检查终结点解析期间用户模式下可用的 RPC 数据字段。 这是用户模式筛选层。 |
| FWPS_LAYER_RPC_EP_ADD | 此筛选层允许在添加新的终结点时检查用户模式下可用的 RPC 数据字段。 这是用户模式筛选层。 |
| FWPS_LAYER_RPC_PROXY_CONN | 此筛选层允许检查 RpcProxy 连接请求。 这是用户模式筛选层。 |
| FWPS_LAYER_RPC_PROXY_IF | 此筛选层允许检查用于 RpcProxy 连接的接口。 这是用户模式筛选层。 |
| FWPS_LAYER_KM_AUTHORIZATION | 此筛选层允许授权建立安全关联。 |

每个运行时层标识符都具有关联的运行时数据字段标识符，该标识符表示一组常量值。 这些数据字段标识符在 Fwpsk 中声明为 FWPS_FIELDS_XXX 枚举。 有关详细信息，请参阅 [数据字段标识符](./data-field-identifiers.md)。