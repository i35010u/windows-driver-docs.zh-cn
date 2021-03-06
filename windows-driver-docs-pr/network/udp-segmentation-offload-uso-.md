---
title: UDP 分段卸载 (USO)
description: UDP 分段卸载 (USO)
keywords:
- '网络驱动程序 WDK，UDP 分段卸载 (USO) '
- UDP 分段卸载 (USO) WDK 网络
- 'UDP 分段卸载 (USO) WDK 网络，关于 UDP 分段卸载 (USO) '
- '关于 UDP 分段卸载 (USO) '
ms.date: 02/27/2020
ms.localizationpriority: medium
ms.openlocfilehash: 982d1039e13a1d5fe3035298a5b80b156384a7d6
ms.sourcegitcommit: a9fb2c30adf09ee24de8e68ac1bc6326ef3616b8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2021
ms.locfileid: "102248106"
---
# <a name="udp-segmentation-offload-uso"></a>UDP 分段卸载 (USO)

Windows 10 版本2004及更高版本中支持的 UDP 分段卸载 (USO) ，这是一项功能，该功能使网络接口卡 (Nic) 卸载大于最大传输单元的 UDP 数据报的分段， (MTU) 网络介质。 通过这样做，Windows 可减少与每个数据包的 TCP/IP 处理相关的 CPU 利用率。 USO 的要求类似于 [LSOv2](offloading-the-segmentation-of-large-tcp-packets.md)，后者用于 TCP 传输协议。

## <a name="requirements-for-uso"></a>USO 的要求

本部分主要涉及 NDIS 协议和微型端口驱动程序。 在修改或发送数据包时， (LWFs) 的 NDIS 轻型筛选器驱动程序必须遵循协议驱动程序要求，还可以假设提供给其 [*FilterSendNetBufferLists*](/windows-hardware/drivers/ddi/content/ndis/nc-ndis-filter_send_net_buffer_lists) 处理程序的任何数据包都满足协议驱动程序要求。

微型端口驱动程序可以卸载大于网络介质的 MTU 的大规模 UDP 数据包的分段。 支持分割大型 UDP 数据包的 NIC 还必须能够执行以下操作：

- 为包含 IPv4 选项的已发送数据包计算 IP 校验和
- 为发送的数据包计算 UDP 校验和

支持 USO 的微型端口驱动程序必须根据 [**NET_BUFFER_LIST**](/windows-hardware/drivers/ddi/content/nbl/ns-nbl-net_buffer_list) 结构的带外 (OOB) 信息确定卸载类型。 如果 [**NDIS_UDP_SEGMENTATION_OFFLOAD_NET_BUFFER_LIST_INFO**](/windows-hardware/drivers/ddi/content/nbluso/ns-nbluso-ndis_udp_segmentation_offload_net_buffer_list_info) 结构的值为非零，则微型端口驱动程序必须执行 USO。 包含 USO OOB 数据的任何 **NET_BUFFER_LIST** 也包含单个 [**NET_BUFFER**](/windows-hardware/drivers/ddi/content/nbl/ns-nbl-net_buffer) 结构。 但是，在微型端口驱动程序已收到 [OID_TCP_OFFLOAD_PARAMETERS](oid-tcp-offload-parameters.md) 关闭 USO 的情况下，在微型端口驱动程序成功完成后，OID 应该会拒绝并返回具有 USO OOB 字段集的任何 **NET_BUFFER_LIST** 。

TCP/IP 传输仅卸载满足以下条件的 UDP 数据包：

- 数据包是 UDP 数据包。
- 包长度必须大于最大段大小 **(MSS) \* (MinSegmentCount)**。
- 如果微型端口驱动程序未设置 **SubMssFinalSegmentSupported** 功能，则传输卸载的每个大型 UDP 数据包的长度必须 **为% MSS = = 0**。 也就是说，较大的数据包可被分割为 **N** 个数据包，每个数据包段包含完全 **MSS** 用户字节。 如果微型端口驱动程序设置 **SubMssFinalSegmentSupported** 功能，则传输上的此数据包长度 divisibility 条件不适用。 换句话说，最后一段可以少于 **MSS**。
- 数据包不是环回数据包。
- 不会设置卸载 TCP/IP 传输的大型 UDP 数据包的 IP 标头中的 **MF** 位，并且 ip 标头中的 **片段偏移量** 将为零。
- 应用程序已指定 UDP_SEND_MSG_SIZE/[WSASetUdpSendMessageSize](/windows/win32/api/ws2tcpip/nf-ws2tcpip-wsasetudpsendmessagesize)。

在为分段卸载大型 UDP 数据包之前，TCP/IP 传输会执行以下操作：

- 更新与 [**NET_BUFFER_LIST**](/windows-hardware/drivers/ddi/content/nbl/ns-nbl-net_buffer_list) 结构关联的大数据包分段信息。 此信息是 [**NDIS_UDP_SEGMENTATION_OFFLOAD_NET_BUFFER_LIST_INFO**](/windows-hardware/drivers/ddi/content/nbluso/ns-nbluso-ndis_udp_segmentation_offload_net_buffer_list_info) 结构，它是 **NET_BUFFER_LIST** 结构的 OOB 信息的一部分。 TCP/IP 传输将 MSS 值设置为所需的 MSS。
- 计算 UDP pseudoheader 的补码总和，并将此 sum 写入 UDP 标头的 **校验** 和字段。 TCP/IP 传输通过 pseudoheader：源 IP 地址、目标 IP 地址和协议中的以下字段来计算一对其补充。  

TCP/IP 传输提供的 pseudoheader 的补码 sum 使 NIC 在计算 NIC 从大型 UDP 数据包中派生的每个数据包的实际 UDP 校验和时提前开始，而无需检查 IP 标头。 

请注意， [rfc 768](https://tools.ietf.org/html/rfc768) 和 [rfc 2460](https://tools.ietf.org/html/rfc2460) 规定通过源 IP 地址、目标 ip 地址、协议和 udp 长度来计算 pseudoheader， (udp 标头的长度加上 udp 有效负载的长度，不包括 pseudoheader) 的长度。 但是，由于基础微型端口驱动程序和 NIC 从通过 TCP/IP 传输方式向下传递的大型数据包生成 UDP 数据报，因此传输不知道每个 UDP 数据报的 UDP 有效负载的大小，因此不能在 pseudoheader 计算中包含 UDP 长度。 相反，如以下部分所述，NIC 扩展了 TCP/IP 传输提供的 pseudoheader 校验和，以涵盖每个生成的 UDP 数据报的 UDP 长度。

> [!IMPORTANT]
> 如果 TCP/IP 传输提供的 UDP 标头校验和字段为零，则 NIC 不应执行 UDP 校验和计算。

## <a name="sending-packets-with-uso"></a>通过 USO 发送数据包

在微型端口驱动程序获取 [*MiniportSendNetBufferLists*](/windows-hardware/drivers/ddi/content/nbl/ns-nbl-net_buffer_list)回调函数中的 [**NET_BUFFER_LIST**](/windows-hardware/drivers/ddi/content/nbl/ns-nbl-net_buffer_list)后，它可以使用 **UdpSegmentationOffloadInfo** 的 **_ID** 调用 [**NET_BUFFER_LIST_INFO**](/windows-hardware/drivers/ddi/content/nblaccessors/nf-nblaccessors-net_buffer_list_info)宏，以获取 MSS 值和 IP 协议。

微型端口驱动程序从第一个 [**NET_BUFFER**](/windows-hardware/drivers/ddi/content/nbl/ns-nbl-net_buffer) 结构的长度获取大数据包的总长度，并使用 **MSS** 值将大型 udp 数据包分割为较小的 udp 数据包。 每个较小的数据包都包含 **MSS** 或更少的用户数据字节。 请注意，只有从分段大数据包创建的最后一个数据包应包含少于 **MSS** 用户数据字节。 通过分段数据包创建的所有其他数据包都必须包含 **MSS** 用户数据字节。 如果微型端口驱动程序不遵循此规则，UDP 数据报将会错误地传递。 如果微型端口驱动程序未设置 **SubMssFinalSegmentSupported** 功能，则数据包长度除以 **mss** ，每个分段的数据包都包含 **MSS** 用户字节。

微型端口驱动程序将 MAC、IP 和 UDP 标头词缀到派生自大数据包的每个段。 微型端口驱动程序必须为这些派生的数据包计算 IP 和 UDP 校验和。 若要计算从大型 UDP 数据包派生的每个数据包的 UDP 校验和，NIC 将计算 udp 校验和的可变部分 (对于 UDP 标头和 UDP 负载) ，将此校验和添加到由 TCP/IP 传输计算的 pseudoheader 的补码和，然后为校验和计算16位的补码。 有关计算此类校验和的详细信息，请参阅 [rfc 768](https://tools.ietf.org/html/rfc768) 和 [rfc 2460](https://tools.ietf.org/html/rfc2460)。 

大型 UDP 数据包中 UDP 用户数据的长度必须小于或等于微型端口驱动程序分配给 **MaxOffLoadSize** 值的值。

当驱动程序发出指示 **MaxOffLoadSize** 值更改的状态指示后，如果驱动程序收到的 LSO 发送请求使用以前的 **MaxOffLoadSize** 值，则该驱动程序不得引发 bug 检查。 相反，驱动程序必须使发送请求失败。 驱动程序 **必须** 失败它们无法执行的任何发送请求，因为任何原因 (包括大小、最小段计数、IP 选项等 ) 。 驱动程序在其功能发生更改时，必须尽快发送状态指示。

独立发出报告 **MaxOffLoadSize** 值更改的状态指示的中间驱动程序必须确保未颁发状态指示的基础微型端口适配器不会获得大于微型端口适配器报告的 **MaxOffLoadSize** 值的任何数据包。

响应 [OID_TCP_OFFLOAD_PARAMETERS](oid-tcp-offload-parameters.md) 关闭 USO 服务的小型中间驱动程序必须准备好一小段时间，其中 USO 请求仍可访问微型端口驱动程序。

从大型 UDP 数据包派生的分段数据包的数量必须等于或大于微型端口驱动程序指定的 **MinSegmentCount** 值。

处理大型 UDP 数据包时，微型端口驱动程序只负责将数据包和后面 MAC、IP 和 UDP 标头划分为从大型 UDP 数据包派生的数据包。 如果微型端口未能发送至少一个分段数据包，则 NBL 必须最终以失败状态完成。 小型端口可以继续发送后续数据包，但这不是必需的。 在所有分段的数据包都传输或失败之前，NBL 无法完成回 NDIS。

支持 USO 的微型端口驱动程序还必须执行以下操作：

- 同时支持 IPv4 和 IPv6。
- 支持从 NIC 生成的每个分段数据包中的大型数据包复制 IPv4 选项。
- 使用 [**NET_BUFFER_LIST**](/windows-hardware/drivers/ddi/content/nbl/ns-nbl-net_buffer_list) 结构中的 IP 和 UDP 标头作为模板为每个分段数据包生成 UDP 和 IP 标头。
- 在 **0x0000** 到 **0xffff** 范围内，使用 IP ID (ip ID) 值。 例如，如果模板 IP 标头的标识字段值为 **0xFFFE**，则第一个 UDP 数据报包的值必须为 **0xFFFE**，后跟 **0xffff**、 **0x0000**、 **0x0001** 等。
- 如果大 UDP 数据包包含 IP 选项，则微型端口驱动程序会将这些选项更改后复制到从大型 UDP 数据包派生的每个数据包。
- 使用 [**NDIS_UDP_SEGMENTATION_OFFLOAD_NET_BUFFER_LIST_INFO**](/windows-hardware/drivers/ddi/content/nbluso/ns-nbluso-ndis_udp_segmentation_offload_net_buffer_list_info)的 **UdpHeaderOffset** 成员中的字节偏移量来确定 UDP 标头的位置（从数据包的第一个字节开始）。
- 根据分段数据包递增传输统计信息。 例如，包括每个数据包段的以太网、IP 和 UDP 标头字节计数，而数据包计数则为 **MSS** 大小段的数目，而不是 **1**。
- 基于每个分段的数据报大小设置 UDP 总长度和 IP 长度字段。

## <a name="ndis-interface-changes"></a>NDIS 接口更改

本部分介绍 NDIS 6.83 中的更改，这些更改使主机 TCP/IP 驱动程序堆栈能够利用微型端口驱动程序公开的 USO 功能。

NDIS 和微型端口驱动程序执行以下操作：

- 播发 NIC 支持 USO 功能
- 启用或禁用 USO
- 获取当前 USO 功能状态

### <a name="advertising-uso-capability"></a>广告 USO 功能

微型端口驱动程序通过填写在 [**NdisMSetMiniportAttributes**](/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismsetminiportattributes)的参数中传递的 [**NDIS_OFFLOAD**](/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_offload)结构的 **UdpSegmentation** 字段，播发 USO 功能。 **NDIS_OFFLOAD** 结构中的 **标头. 修订号** 字段必须设置为 **NDIS_OFFLOAD_REVISION_6** 并且必须将 "**标头大小**" 字段设置为 " **NDIS_SIZEOF_NDIS_OFFLOAD_REVISION_6**"。

### <a name="querying-uso-state"></a>正在查询 USO 状态

可以通过 [OID_TCP_OFFLOAD_CURRENT_CONFIG](oid-tcp-offload-current-config.md)查询当前 USO 状态。 NDIS 处理此 OID，不会将其向下传递到微型端口驱动程序。

### <a name="changing-uso-state"></a>更改 USO 状态

使用 [OID_TCP_OFFLOAD_PARAMETERS](oid-tcp-offload-parameters.md)可以启用或禁用 USO。 微型端口驱动程序处理 OID 后，它必须发送一个 [NDIS_STATUS_TASK_OFFLOAD_CURRENT_CONFIG](ndis-status-task-offload-current-config.md) 状态指示，其中包含更新的卸载状态。

## <a name="uso-keywords"></a>USO 关键字

USO 枚举关键字如下所示：

- **\*UsoIPv4**
- **\*UsoIPv6**

这些值描述了是为该特定 IP 协议启用还是禁用 USO。 USO 设置不依赖于 [**NDIS_TCP_IP_CHECKSUM_OFFLOAD**](/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_tcp_ip_checksum_offload) 配置。 例如，禁用 **\* UDPChecksumOffloadIPv4** 不会隐式禁用 **\* UsoIPv4**。

| 子项名称 | 参数说明 | 值 | 枚举说明 |
| --- | --- | --- | --- |
| **\*UsoIPv4** | UDP 分段卸载 (IPv4)  | 0 | 已禁用 |
|   |   | 1 | 已启用 |
| **\*UsoIPv6** | UDP 分段卸载 (IPV6)  | 0 | 已禁用 |
|   |   | 1 | 已启用 |
