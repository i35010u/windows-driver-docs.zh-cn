---
title: 卸载大型 TCP 数据包的段
description: 卸载大型 TCP 数据包的段
ms.assetid: 6ae162fb-a8fc-47b8-80ae-ff39f3059d53
keywords:
- 任务卸载 WDK TCP/IP 传输、大数据包分段
- 大型 TCP 数据包分段 WDK 网络
- 大 TCP 数据包的分段 WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 59534e248be58ec5fb612d91fb1f9c4da964ccfa
ms.sourcegitcommit: d1fb8dfd78e0f4993e428a47c231bcbebb9e223c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/04/2019
ms.locfileid: "71967031"
---
# <a name="offloading-the-segmentation-of-large-tcp-packets"></a>卸载大型 TCP 数据包的段





NDIS 微型端口驱动程序可以卸载大于网络介质的最大传输单位（MTU）的大型 TCP 数据包的分段。 支持分段大 TCP 数据包的 NIC 还必须能够：

-   为发送包含 IP 选项的数据包计算 IP 校验和。

-   为发送包含 TCP 选项的数据包计算 TCP 校验和。

NDIS 版本6.0 及更高版本支持大型发送卸载版本1（LSOV1），这类似于 NDIS 5 中的大量发送卸载（LSO）。*x*。 NDIS 版本6.0 及更高版本还支持大型发送卸载版本2（LSOV2），该版本提供增强的大型数据包分段服务，包括对 IPv6 的支持。

支持 LSOV2 和 LSOV1 的微型端口驱动程序必须通过[**NET @ no__t-2BUFFER @ no__t-3LIST**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list)结构 OOB 信息确定卸载类型。 驱动程序可以使用[**NDIS @ no__t-3TCP @ no__t-4LARGE @ no__t-5SEND @ no__t-6OFFLOAD @** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_tcp_large_send_offload_net_buffer_list_info) no__t-7NET @ no__t-8BUFFER @ no__t-9LIST @ no__t-10INFO 结构的**类型**成员来确定驱动程序堆栈是使用 LSOV2 还是 LSOV1，执行适当的卸载服务。 包含 LSOv1 或 LSOv2 OOB 数据的任何 NET @ no__t-0BUFFER @ no__t-1LIST 结构还包含一个[**net @ no__t-4BUFFER**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer)结构。 有关 NDIS @ no__t-0TCP @ no__t-1LARGE @ no__t-2SEND @ no__t-3OFFLOAD @ no__t-4NET @ no__t-5BUFFER @ no__t-6LIST @ no__t-7INFO 的详细信息，请参阅[访问 Tcp/ip 卸载 NET @ no__t-9BUFFER @ no__t-10LIST 信息](accessing-tcp-ip-offload-net-buffer-list-information.md)。

但是，在这种情况下，微型端口已收到[**OID @ no__t-2TCP @ no__t-3OFFLOAD @ no__t-4PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/network/oid-tcp-offload-parameters) ，以便在微型端口上关闭 LSO 功能，并且在微型端口成功完成 OID 后，微型端口应丢弃所有[**NET @ no__t-7BUFFER @ no__t-8LIST**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list) ，其中包含任何非零 LSOv1 或 LSOV2 OOB 数据（[**NDIS @ NO__T-11TCP @ NO__T-12LARGE @** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_tcp_large_send_offload_net_buffer_list_info)no__t-13SEND @ no__t-14OFFLOAD @ no__t-15NET @ no__t）。 

TCP/IP 传输仅卸载满足以下条件的那些大型 TCP 数据包：

-   数据包是 TCP 数据包。 TCP/IP 传输不会卸载用于分段的大型 UDP 数据包。

-   数据包的最小数量只能为微型端口驱动程序指定的最小段数。 有关详细信息，请参阅[报告 nic 的 LSOV1 Tcp 数据包分段功能](reporting-a-nic-s-lsov1-tcp-packet-segmentation-capabilities.md)和[报告 NIC 的 LSOV2 Tcp 数据包分段功能](reporting-a-nic-s-lsov2-tcp-packet-segmentation-capabilities.md)。

-   数据包不是环回数据包。

-   数据包将不会通过隧道发送。

在为分段卸载大的 TCP 数据包之前，TCP/IP 传输：

-   更新与[**NET @ no__t-2BUFFER @ no__t-3LIST**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list)结构关联的大数据包分段信息。 此信息是一个[**NDIS @ no__t-2TCP @ no__t-3LARGE @ no__t-4SEND @ no__t-5OFFLOAD @** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_tcp_large_send_offload_net_buffer_list_info) no__t-6NET @ no__t-7BUFFER @ no__t-8LIST @ no__t 结构，它是与关联的**NET @ 9INFO-no__t @ 11BUFFER-** no__t具有**NET @ no__t-14BUFFER @ no__t-15LIST**结构。 有关**NET @ no__t-1BUFFER @ no__t-2LIST**信息的详细信息，请参阅[访问 tcp/ip 卸载 NET @ no__t-4BUFFER @ No__t-5LIST 信息](accessing-tcp-ip-offload-net-buffer-list-information.md)。 TCP/IP 传输将**MSS**值设置为最大段大小（mss）。

- 对于 LSOv1，将大 TCP 数据包的总长度写入数据包的 IP 标头的总长度字段。 总长度包括 IP 标头的长度、IP 选项的长度（如果存在）、TCP 标头的长度、TCP 选项的长度（如果存在，则为 tcp 有效负载的长度）。 对于 LSOv2，将数据包的 IP 标头的总长度字段设置为0。 微型端口驱动程序应根据 NET_BUFFER_LIST 结构中第一个 NET_BUFFER 结构的长度确定数据包的长度。

-   计算 TCP pseudoheader 的补码总和，并将此 sum 写入 TCP 标头的校验和字段。 TCP/IP 传输通过 pseudoheader 中的以下字段来计算1的补数总和：源 IP 地址、目标 IP 地址和协议。 TCP/IP 传输提供的 pseudoheader 的补码总和为 NIC 提供了一个早期开始，用于计算 NIC 从大 TCP 数据包派生的每个数据包的实际 TCP 校验和，而无需检查 IP 标头。 请注意，RFC 793 规定在源 IP 地址、目标 IP 地址、协议和 TCP 长度的情况下，对伪标头校验和进行计算。 （TCP 长度为 TCP 标头的长度加上 TCP 有效负载的长度。 TCP 长度不包括伪标头的长度。）但是，由于基础微型端口驱动程序和 NIC 从通过 TCP/IP 传输方式向下传递的大型数据包生成 TCP 段，因此传输不知道每个 TCP 段的 TCP 有效负载的大小，因此不能将 TCP 长度包含在伪标头。 相反，如上所述，NIC 扩展了 TCP/IP 传输提供的伪标头校验和，以涵盖每个生成的 TCP 段的 TCP 长度。

-   将正确的序列号写入 TCP 标头的序列号字段。 序列号标识 TCP 有效负载的第一个字节。

当微型端口驱动程序在其[*MiniportSendNetBufferLists*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_send_net_buffer_lists)或[**MiniportCoSendNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_co_send_net_buffer_lists)函数中获取[**net @ no__t-2BUFFER @ no__t-3LIST**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list)结构后，它可以调用[**net @ no__t-10BUFFER @ no__t-11LIST @ no__12INFO**](https://docs.microsoft.com/windows-hardware/drivers/network/net-buffer-list-info)宏，其中包含 TcpLargeSendNetBufferListInfo *4Id* ，以获取由 tcp/ip 传输写入的 MSS 值。

微型端口驱动程序从数据包的 IP 标头中获取大数据包的总长度，并使用 MSS 值将大 TCP 数据包分割为较小的数据包。 每个较小的数据包都包含 MSS 或更少的用户数据字节。 请注意，只有从分段大数据包创建的最后一个数据包应包含少于 MSS 用户数据字节。 通过分段数据包创建的所有其他数据包都应包含 MSS 用户数据字节。 如果不遵循此规则，创建和传输不必要的额外数据包可能会降低性能。

微型端口驱动程序将 MAC、IP 和 TCP 标头词缀到派生自大数据包的每个段。 微型端口驱动程序必须为这些派生的数据包计算 IP 和 TCP 校验和。 若要计算从大 TCP 数据包派生的每个数据包的 TCP 校验和，NIC 将计算 TCP 校验和的可变部分（对于 TCP 标头和 TCP 负载），将此校验和添加到 pseudoheader 计算的TCP/IP 传输，然后为校验和计算16位的补码。 有关计算此类校验和的详细信息，请参阅 RFC 793 和 RFC 1122。

下图显示大数据包的分段。

![说明大型数据包的分段的示意图](images/segmentation.png)

大 TCP 数据包中的 TCP 用户数据的长度应等于或小于微型端口驱动程序分配给**MaxOffLoadSize**值的值。 有关**MaxOffLoadSize**值的详细信息，请参阅[报告 NIC 的 LSOV1 Tcp 数据包分段功能](reporting-a-nic-s-lsov1-tcp-packet-segmentation-capabilities.md)和[报告 Nic 的 LSOV2 tcp 数据包分段功能](reporting-a-nic-s-lsov2-tcp-packet-segmentation-capabilities.md)。

驱动程序发出状态指示以指示对**MaxOffLoadSize**值的更改后，如果接收到使用以前的**MAXOFFLOADSIZE**值的 LSO 发送请求，则驱动程序不得崩溃。 相反，驱动程序可能会失败发送请求。

独立发出报告**MaxOffLoadSize**值更改的状态指示的中间驱动程序必须确保未颁发状态指示的基础微型端口适配器不会获得大小较大的任何数据包。要报告的**MaxOffLoadSize**值。

对[OID @ no__t-1TCP @ no__t-2OFFLOAD @ no__t-3PARAMETERS](https://docs.microsoft.com/windows-hardware/drivers/network/oid-tcp-offload-parameters)关闭 LSO 服务的小型中间驱动程序必须准备好一小段时间，其中，lso 发送请求仍可访问微型端口驱动程序。

段数据包中 TCP 用户数据的长度必须小于或等于 MSS。 MSS 是 TCP 传输通过使用与[**NET @ no__t-4BUFFER @ no__t-5LIST**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list)结构关联的 LSO NET @ NO__T-0BUFFER @ NO__T-1LIST 信息向下传递的 ULONG 值。 请注意，只有从分段大数据包创建的最后一个数据包应包含少于 MSS 用户数据字节。 通过分段数据包创建的所有其他数据包都应包含 MSS 用户数据字节。 如果不遵循此规则，创建和传输不必要的额外数据包可能会降低性能。

派生自大 TCP 数据包的段数据包数必须等于或大于微型端口驱动程序指定的**MinSegmentCount**值。 有关**MinSegmentCount**值的详细信息，请参阅[报告 NIC 的 LSOV1 Tcp 数据包分段功能](reporting-a-nic-s-lsov1-tcp-packet-segmentation-capabilities.md)和[报告 Nic 的 LSOV2 tcp 数据包分段功能](reporting-a-nic-s-lsov2-tcp-packet-segmentation-capabilities.md)。

以下假设和限制适用于处理 IP 和 TCP 标头：

-   不会设置卸载 TCP/IP 传输的大型 TCP 数据包的 IP 标头中的 MF 位，并且 IP 标头中的片段偏移量将为零。

-   将不会设置大型 TCP 数据包的 TCP 标头中的 URG、RST 和 SYN 标志，并且 TCP 标头中的紧急偏移（指针）将为零。

-   如果设置大数据包的 TCP 标头中的 FIN 位，微型端口驱动程序必须在从大型 TCP 数据包创建的最后一个数据包的 TCP 标头中设置此位。

-   如果设置大 TCP 数据包的 TCP 标头中的 PSH 位，微型端口驱动程序必须在从大型 TCP 数据包创建的最后一个数据包的 TCP 标头中设置此位。

-   如果设置大 TCP 数据包的 TCP 标头中的 CWR 位，微型端口驱动程序必须在从大型 TCP 数据包创建的第一个数据包的 TCP 标头中设置此位。 小型端口驱动程序可能会选择在其从大 TCP 数据包创建的最后一个数据包的 TCP 标头中设置此位，不过这不太理想。

-   如果大 TCP 数据包包含 IP 选项或 TCP 选项（或两者），微型端口驱动程序会将这些选项更改后复制到它派生自大 TCP 数据包的每个数据包。 具体而言，NIC 不会递增时间戳选项。

-   所有数据包标头（以太网、IP、TCP）都将位于数据包的第一 MDL。 标头不会跨多个 MDLs 拆分。 
    > [!TIP]
    > 当启用了 LSO 时，此假设是有效的。 否则，如果未启用 LSO，微型端口驱动程序将无法假定 IP 标头与以太网标头属于同一 MDL。


微型端口驱动程序必须按照从 TCP/IP 传输接收 NET @ no__t-4BUFFER @ no__t 结构的顺序，将[**no__t-2BUFFER @ no__t-3LIST**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list)结构中的数据包发送到其中。

当处理大型 TCP 数据包时，微型端口适配器仅负责将数据包和后面 MAC、IP 和 TCP 标头划分为从大 TCP 数据包派生的数据包。 TCP/IP 传输执行所有其他任务（例如根据远程主机的接收窗口大小调整发送窗口大小）。

在完成大型数据包（例如 with [**NdisMSendNetBufferListsComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismsendnetbufferlistscomplete)或[**NdisMCoSendNetBufferListsComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismcosendnetbufferlistscomplete)）的发送操作之前，微型端口驱动程序会写入[**NDIS @ no__t-6TCP @ no__t-7LARGE @ no__t-8SEND @ no__t-9OFFLOAD @ no__t-10NET @ no__t-11BUFFER @ no__t-12LIST @ no__t-13INFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_tcp_large_send_offload_net_buffer_list_info) value （NET @ no__t-14BUFFER @ no__t），其中包含已创建的所有数据包中成功发送的 TCP 用户数据字节总数从大 TCP 数据包。

除了以前的 LSO 要求外，LSOV2 支持的微型端口驱动程序还必须：

-   支持 IPv4 或 IPv6，或者 IPv4 和 IPv6。

-   支持在网络接口卡（NIC）生成的每个段数据包中从大数据包复制 IPv4 选项。

-   支持在每个 TCP 段数据包中从大 TCP 数据包复制 IPv6 扩展标头。

-   支持在微型端口驱动程序生成的每个 TCP 段数据包中复制 TCP 选项。

-   使用[**NET @ no__t-2BUFFER @ no__t-3LIST**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list)结构中的 IP 和 TCP 标头作为模板，为每个段数据包生成 tcp/ip 标头。

-   使用范围从0x0000 到0x7FFF 的 IP 标识（IP ID）值。 （从0x8000 到0xFFFF 的范围为支持 TCP 烟囱卸载的设备保留。）例如，如果模板 IP 标头的标识字段值为0x7FFE，则第一个 TCP 段数据包的 IP ID 值必须为0x7FFE，后跟0x7FFF、0x0000、0x0001 等。

-   使用[**NDIS @ no__t-3TCP @ no__t-4LARGE @ no__t-5SEND @ no__t-6OFFLOAD**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_tcp_large_send_offload_net_buffer_list_info) @ no__t-7NET @ no__t-8BUFFER @ no__t-9LIST @ no__t-10INFO @-@-的**TcpHeaderOffset**成员中的字节偏移量来确定 TCP 标头的位置（从第一个字节。

-   将与每个 LSOV2 [**net @ no__t-5BUFFER @ no__t**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list)结构关联的[**net @ no__t-2BUFFER**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer)结构的数目限制为1。

-   根据 NET @ no__t-1BUFFER @ no__t-2LIST 结构中第一个 NET @ no__t-0BUFFER 结构的长度确定数据包的总长度。

-   支持 TCP 选项、IP 选项和 IP 扩展标头。

-   发送操作完成后，微型端口驱动程序必须将[**NDIS_TCP_LARGE_SEND_OFFLOAD_NET_BUFFER_LIST_INFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_tcp_large_send_offload_net_buffer_list_info)结构的**LsoV2TransmitComplete**成员设置为零，并将**LsoV2TransmitComplete**成员设置为到 NDIS_TCP_LARGE_SEND_OFFLOAD_V2_TYPE。 
 

 





