---
title: 卸载大型 TCP 数据包的段
description: 卸载大型 TCP 数据包的段
ms.assetid: 6ae162fb-a8fc-47b8-80ae-ff39f3059d53
keywords:
- 任务卸载 WDK TCP/IP 传输、大数据包分段
- 大型 TCP 数据包分段 WDK 网络
- 大 TCP 数据包的分段 WDK 网络
ms.date: 10/24/2019
ms.localizationpriority: medium
ms.openlocfilehash: a00fca691f54fd42d850694e45c4c41552565fb7
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89217532"
---
# <a name="offloading-the-segmentation-of-large-tcp-packets"></a>卸载大型 TCP 数据包的段

NDIS 微型端口驱动程序可以卸载大于网络媒体 (MTU) 的大 TCP 数据包的分段。 支持分段大 TCP 数据包的 NIC 还必须能够：

-   为发送包含 IP 选项的数据包计算 IP 校验和。

-   为发送包含 TCP 选项的数据包计算 TCP 校验和。

NDIS 版本6.0 及更高版本支持大型发送卸载版本 1 (LSOv1) ，这类似于在 NDIS 5 中 (LSO) 进行大量发送卸载。*x*。 NDIS 版本6.0 及更高版本还支持大型发送卸载版本 2 (LSOv2) ，它提供了增强的大型数据包分段服务，包括对 IPv6 的支持。

支持 LSOv2 和 LSOv1 的微型端口驱动程序必须从 [**网络 \_ 缓冲区 \_ 列表**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list) 结构 OOB 信息确定卸载类型。 驱动程序可以使用[**NDIS \_ TCP \_ 大规模发送卸载的类型成员 \_ \_ \_ 网络 \_ 缓冲区 \_ 列表 \_ 信息**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_tcp_large_send_offload_net_buffer_list_info)结构来确定驱动程序堆栈是使用 LSOv2 还是 LSOv1，并执行适当的卸载服务。 **Type** \_ \_ 包含 LSOv1 或 LSOv2 OOB 数据的任何网络缓冲区列表结构还包含单一[**网络 \_ 缓冲区**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer)结构。 有关 NDIS \_ TCP \_ 大规模 \_ 发送 \_ 卸载 \_ 网络 \_ 缓冲区列表信息的详细信息 \_ \_ ，请参阅 [访问 tcp/ip 卸载网络 \_ 缓冲区 \_ 列表信息](accessing-tcp-ip-offload-net-buffer-list-information.md)。

但是，在这种情况下，微型端口已收到[**OID \_ tcp \_ 卸载 \_ 参数**](./oid-tcp-offload-parameters.md)，可在微型端口上关闭 LSO 功能，并且在微型端口成功完成 OID 后，小型端口将删除包含任何非零 LSOv1 或 LSOv2 OOB 数据 ([**NDIS \_ TCP \_ 大规模 \_ 发送 \_ 卸载 \_ 网络 \_ 缓冲区 \_ 列表 \_ 信息**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_tcp_large_send_offload_net_buffer_list_info)) 。 [** \_ \_ **](/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list) 

TCP/IP 传输仅卸载满足以下条件的那些大型 TCP 数据包：

-   数据包是 TCP 数据包。 TCP/IP 传输不会卸载用于分段的大型 UDP 数据包。

-   数据包的最小数量只能为微型端口驱动程序指定的最小段数。 有关详细信息，请参阅 [报告 nic 的 LSOV1 Tcp 数据包分段功能](reporting-a-nic-s-lsov1-tcp-packet-segmentation-capabilities.md) 和 [报告 NIC 的 LSOv2 Tcp 数据包分段功能](reporting-a-nic-s-lsov2-tcp-packet-segmentation-capabilities.md)。

-   数据包不是环回数据包。

-   数据包将不会通过隧道发送。

在为分段卸载大的 TCP 数据包之前，TCP/IP 传输：

-   更新与 [**网络 \_ 缓冲区 \_ 列表**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list) 结构关联的大数据包分段信息。 此信息是一个[**NDIS \_ TCP \_ 大型 \_ 发送 \_ 卸载 \_ 网络 \_ 缓冲区 \_ 列表 \_ 信息**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_tcp_large_send_offload_net_buffer_list_info)结构，它是与**网络 \_ 缓冲区 \_ 列表**结构关联的**网络 \_ 缓冲区 \_ 列表**信息的一部分。 有关 **网络 \_ 缓冲区 \_ 列表** 信息的详细信息，请参阅 [访问 Tcp/ip 卸载网络 \_ 缓冲区 \_ 列表信息](accessing-tcp-ip-offload-net-buffer-list-information.md)。 TCP/IP 传输将 **mss** 值设置为 (mss) 的最大段大小。

<a name="lsov1lengthrequirements"></a>

- 对于 LSOv1，将大 TCP 数据包的总长度写入数据包的 IP 标头的总长度字段。 总长度包括 IP 标头的长度、IP 选项的长度（如果存在）、TCP 标头的长度、TCP 选项的长度（如果存在，则为 tcp 有效负载的长度）。 对于 LSOv2，将数据包的 IP 标头的总长度字段设置为0。 微型端口驱动程序应根据 NET_BUFFER_LIST 结构中第一个 NET_BUFFER 结构的长度来确定数据包的长度。

-   计算 TCP pseudoheader 的补码总和，并将此 sum 写入 TCP 标头的校验和字段。 TCP/IP 传输通过 pseudoheader：源 IP 地址、目标 IP 地址和协议中的以下字段来计算一次补码之和。 TCP/IP 传输提供的 pseudoheader 的补码总和为 NIC 提供了一个早期开始，用于计算 NIC 从大 TCP 数据包派生的每个数据包的实际 TCP 校验和，而无需检查 IP 标头。 请注意，RFC 793 规定在源 IP 地址、目标 IP 地址、协议和 TCP 长度的情况下，对伪标头校验和进行计算。  (TCP 长度为 tcp 标头的长度加上 TCP 有效负载的长度。 TCP 长度不包括伪标头的长度。 ) 但是，因为基础微型端口驱动程序和 NIC 基于 TCP/IP 传输向下传递的大型数据包生成 TCP 段，所以传输不知道每个 TCP 段的 TCP 有效负载的大小，因此不能将 TCP 长度包含在伪标头中。 相反，如上所述，NIC 扩展了 TCP/IP 传输提供的伪标头校验和，以涵盖每个生成的 TCP 段的 TCP 长度。

-   将正确的序列号写入 TCP 标头的序列号字段。 序列号标识 TCP 有效负载的第一个字节。

当微型端口驱动程序在其[*MiniportSendNetBufferLists*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_send_net_buffer_lists)或[**MiniportCoSendNetBufferLists**](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_co_send_net_buffer_lists)函数中获取[**网络 \_ 缓冲区 \_ 列表**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)结构后，它可以调用* \_ Id*为**TcpLargeSendNetBufferListInfo**的[**网络 \_ 缓冲区 \_ 列表 \_ 信息**](/windows-hardware/drivers/ddi/ndis/nf-ndis-net_buffer_list_info)宏，以获取由 tcp/ip 传输写入的 MSS 值。

微型端口驱动程序从数据包的 IP 标头中获取大数据包的总长度，并使用 MSS 值将大 TCP 数据包分割为较小的数据包。 每个较小的数据包都包含 MSS 或更少的用户数据字节。 请注意，只有从分段大数据包创建的最后一个数据包应包含少于 MSS 用户数据字节。 通过分段数据包创建的所有其他数据包都应包含 MSS 用户数据字节。 如果不遵循此规则，创建和传输不必要的额外数据包可能会降低性能。

微型端口驱动程序将 MAC、IP 和 TCP 标头词缀到派生自大数据包的每个段。 微型端口驱动程序必须为这些派生的数据包计算 IP 和 TCP 校验和。 若要计算从大 TCP 数据包派生的每个数据包的 TCP 校验和，NIC 将计算 tcp 校验和的可变部分 (对于 TCP 标头和 TCP 负载) ，将此校验和添加到由 TCP/IP 传输计算的 pseudoheader 的补码和，然后计算该校验和的16位补码。 有关计算此类校验和的详细信息，请参阅 RFC 793 和 RFC 1122。

下图显示大数据包的分段。

![说明大型数据包的分段的示意图](images/segmentation.png)

大 TCP 数据包中的 TCP 用户数据的长度应等于或小于微型端口驱动程序分配给 **MaxOffLoadSize** 值的值。 有关 **MaxOffLoadSize** 值的详细信息，请参阅 [报告 NIC 的 LSOv1 Tcp 数据包分段功能](reporting-a-nic-s-lsov1-tcp-packet-segmentation-capabilities.md) 和 [报告 Nic 的 LSOv2 tcp 数据包分段功能](reporting-a-nic-s-lsov2-tcp-packet-segmentation-capabilities.md)。

驱动程序发出状态指示以指示对 **MaxOffLoadSize** 值的更改后，如果接收到使用以前的 **MAXOFFLOADSIZE** 值的 LSO 发送请求，则驱动程序不得崩溃。 相反，驱动程序可能会失败发送请求。

独立发出报告 **MaxOffLoadSize** 值更改的状态指示的中间驱动程序必须确保未颁发状态指示的基础微型端口适配器不会获得大小大于微型端口适配器所报告的 **MaxOffLoadSize** 值的任何数据包。

响应 [OID \_ TCP \_ 卸载 \_ 参数](./oid-tcp-offload-parameters.md) 以关闭 LSO 服务的小型中间驱动程序必须准备好一小段时间，其中，LSO 发送请求仍可访问微型端口驱动程序。

段数据包中 TCP 用户数据的长度必须小于或等于 MSS。 MSS 是 TCP 传输通过使用 \_ \_ 与 [**网络 \_ 缓冲区 \_ 列表**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list) 结构关联的 LSO 网络缓冲区列表信息向下传递的 ULONG 值。 请注意，只有从分段大数据包创建的最后一个数据包应包含少于 MSS 用户数据字节。 通过分段数据包创建的所有其他数据包都应包含 MSS 用户数据字节。 如果不遵循此规则，创建和传输不必要的额外数据包可能会降低性能。

派生自大 TCP 数据包的段数据包数必须等于或大于微型端口驱动程序指定的 **MinSegmentCount** 值。 有关 **MinSegmentCount** 值的详细信息，请参阅 [报告 NIC 的 LSOv1 Tcp 数据包分段功能](reporting-a-nic-s-lsov1-tcp-packet-segmentation-capabilities.md) 和 [报告 Nic 的 LSOv2 tcp 数据包分段功能](reporting-a-nic-s-lsov2-tcp-packet-segmentation-capabilities.md)。

以下假设和限制适用于处理任何支持 LSO 的微型端口驱动程序的 IP 和 TCP 标头，而不考虑版本：

-   不会设置卸载 TCP/IP 传输的大型 TCP 数据包的 IP 标头中的 MF 位，并且 IP 标头中的片段偏移量将为零。

-   将不会设置大型 TCP 数据包的 TCP 标头中的 URG、RST 和 SYN 标志，并且 TCP 标头中) 的紧急偏移 (指针将为零。

-   如果设置大数据包的 TCP 标头中的 FIN 位，微型端口驱动程序必须在从大型 TCP 数据包创建的最后一个数据包的 TCP 标头中设置此位。

-   如果设置大 TCP 数据包的 TCP 标头中的 PSH 位，微型端口驱动程序必须在从大型 TCP 数据包创建的最后一个数据包的 TCP 标头中设置此位。

-   如果设置大 TCP 数据包的 TCP 标头中的 CWR 位，微型端口驱动程序必须在从大型 TCP 数据包创建的第一个数据包的 TCP 标头中设置此位。 小型端口驱动程序可能会选择在其从大 TCP 数据包创建的最后一个数据包的 TCP 标头中设置此位，不过这不太理想。

-   如果大 TCP 数据包包含 IP 选项或 TCP 选项 (或两者均) ，微型端口驱动程序会将这些选项更改为从大 TCP 数据包派生的每个数据包。 具体而言，NIC 不会递增时间戳选项。

-   数据包的第一个 MDL (以太网、IP、TCP) 的所有数据包标头。 标头不会跨多个 MDLs 拆分。 
    > [!TIP]
    > 当启用了 LSO 时，此假设是有效的。 否则，如果未启用 LSO，微型端口驱动程序将无法假定 IP 标头与以太网标头属于同一 MDL。


微型端口驱动程序必须按照从 TCP/IP 传输收到的网络缓冲区列表结构的顺序，在 [**网络 \_ 缓冲区 \_ 列表**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list) 结构中发送数据包 \_ \_ 。

当处理大型 TCP 数据包时，微型端口适配器仅负责将数据包和后面 MAC、IP 和 TCP 标头划分为从大 TCP 数据包派生的数据包。 TCP/IP 传输执行所有其他任务，例如根据远程主机的接收窗口大小调整 "发送" 窗口大小)  (。

在完成大型数据包 (的发送操作之前（例如 with [**NdisMSendNetBufferListsComplete**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsendnetbufferlistscomplete) 或 [**NdisMCoSendNetBufferListsComplete**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismcosendnetbufferlistscomplete)) ），微型端口驱动程序会将 [**NDIS \_ TCP \_ 大规模 \_ 发送 \_ 卸载 \_ 网络 \_ 缓冲区 \_ 列表 \_ 信息**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_tcp_large_send_offload_net_buffer_list_info) 值写入 \_ (\_ 用于大发送) 卸载的网络缓冲区列表信息，并在从大型 TCP 数据包创建的所有数据包中成功发送的 TCP 用户数据字节总数。

除了以前的 LSO 要求外，LSOv2 支持的微型端口驱动程序还必须：

-   支持 IPv4 或 IPv6，或者 IPv4 和 IPv6。

-   支持在网络接口卡 (NIC) 生成的每个段数据包的 IPv4 选项之间进行复制。

-   支持在每个 TCP 段数据包中从大 TCP 数据包复制 IPv6 扩展标头。

-   支持在微型端口驱动程序生成的每个 TCP 段数据包中复制 TCP 选项。

-   使用 [**网络 \_ 缓冲区 \_ 列表**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list) 结构中的 IP 和 TCP 标头作为模板为每个段数据包生成 tcp/ip 标头。

-   使用0x0000 到0x7FFF 范围内的 ip ID (IP ID) 值。  (为支持 TCP 烟囱卸载的设备保留的范围介于0x8000 到0xFFFF 之间。 ) 例如，如果模板 IP 标头以0x7FFE 的标识字段开头，则第一个 TCP 段数据包的 IP ID 值必须为0x7FFE，后跟0x7FFF、0x0000、0x0001 等。

-   使用 NDIS TCP 的 **TcpHeaderOffset** 成员中的字节偏移量 [** \_ \_ \_ 发送 \_ \_ 网络 \_ 缓冲区 \_ 列表 \_ 信息**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_tcp_large_send_offload_net_buffer_list_info) ，以从数据包的第一个字节开始确定 TCP 标头的位置。

-   将与每个 LSOv2[**网络 \_ 缓冲区 \_ 列表**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)结构关联的[**网络 \_ 缓冲区**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer)结构的数目限制为一个。
    > [!NOTE]
    > 这是支持 LSOv2 的微型端口驱动程序的新要求。 此规则不会显式强制用于 LSOv1 微型端口驱动程序，尽管建议这样做。

-   确定 \_ 网络 \_ 缓冲区列表结构中第一个网络缓冲区结构长度的数据包的总长度 \_ 。 这不同于 LSOv1 的 <a href="#lsov1lengthrequirements">方法驱动程序使用</a>。

-   支持 TCP 选项、IP 选项和 IP 扩展标头。

-   发送操作完成后，微型端口驱动程序必须将[**NDIS_TCP_LARGE_SEND_OFFLOAD_NET_BUFFER_LIST_INFO**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_tcp_large_send_offload_net_buffer_list_info)结构的**LsoV2TransmitComplete**成员设置为零，并将**LsoV2TransmitComplete**成员设置为 NDIS_TCP_LARGE_SEND_OFFLOAD_V2_TYPE。