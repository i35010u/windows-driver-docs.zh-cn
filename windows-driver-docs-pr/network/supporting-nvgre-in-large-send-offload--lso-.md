---
title: 在大规模发送卸载 (LSO) 中支持 NVGRE
description: 本部分介绍了在大型发送卸载（LSO）中支持 NVGRE
ms.assetid: 1EB1B8C2-85C1-4256-BE96-C8B9F1D222B6
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0c0cbb039154408e217fd85ad804fdea1bcf0c99
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841795"
---
# <a name="supporting-nvgre-in-large-send-offload-lso"></a>在大规模发送卸载 (LSO) 中支持 NVGRE


NDIS 6.30 （Windows Server 2012）[使用通用路由封装（NVGRE）引入网络虚拟化](network-virtualization-using-generic-routing-encapsulation--nvgre--task-offload.md)。 执行大型发送卸载（LSO）版本2（LSOV2）的 NDIS 微型端口、协议和筛选器驱动程序和 Nic 应该以支持 NVGRE 的方式实现此目的。

**请注意**  本页假设你熟悉了如何[分担大 TCP 数据包的分段](offloading-the-segmentation-of-large-tcp-packets.md)。

 

如果[**NDIS\_TCP\_发送\_卸载\_补充\_NET\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_tcp_send_offloads_supplemental_net_buffer_list_info)\_\_的信息。**IsEncapsulatedPacket**为**TRUE** ，并且**TcpIpChecksumNetBufferListInfo**带外（OOB）信息有效，这表示需要 NVGRE 支持，而 NIC 必须在 NVGRE 格式的数据包，条件如下：

-   只有[**NDIS\_TCP\_大\_发送\_卸载\_NET\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_tcp_large_send_offload_net_buffer_list_info)\_\_的信息。**LsoV2Transmit**结构有效。 NIC 和微型端口驱动程序不得引用**NDIS\_TCP\_大型\_发送\_卸载\_NET\_** \_\_的信息。**LsoV1Transmit**结构。
-   [**NDIS\_TCP\_大型\_发送\_卸载\_NET\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_tcp_large_send_offload_net_buffer_list_info)\_\_的信息。**LsoV2Transmit**。**TcpHeaderOffset**成员没有正确的偏移值，且不能由 NIC 或微型端口驱动程序使用。

若要支持 LSOV2 中的 NVGRE，协议和筛选器驱动程序必须进行以下更改：

-   减小[**NDIS\_TCP\_大型\_发送\_卸载\_NET\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_tcp_large_send_offload_net_buffer_list_info)\_\_的信息。要用于新的 GRE 标头的**LsoV2Transmit**结构。
-   发送一个 TCP 负载长度，该长度可能不是已减少的**MSS**值的准确倍数。
-   调整 NDIS 中的**InnerFrameOffset**、 **TransportIpHeaderRelativeOffset**和**TCPHEADERRELATIVEOFFSET**值[ **\_TCP\_发送\_卸载\_补充\_NET\_缓存\_列出**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_tcp_send_offloads_supplemental_net_buffer_list_info)了要为 GRE 标头帐户\_信息结构。

Nic 和微型端口驱动程序可以使用 NDIS\_TCP\_中提供的**InnerFrameOffset**、 **TransportIpHeaderRelativeOffset**和**TcpHeaderRelativeOffset**值[**发送\_卸载\_补充\_NET\_缓冲器\_列表\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_tcp_send_offloads_supplemental_net_buffer_list_info)结构。 NIC 或微型端口驱动程序可以对隧道（外部） IP 标头或后续标头执行任何所需的标头检查来验证这些偏移量。

微型端口驱动程序必须处理[**NDIS\_TCP\_发送\_卸载\_补充\_NET\_\_\_列表信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_tcp_send_offloads_supplemental_net_buffer_list_info)的情况。**InnerFrameOffset**可能在不同于数据包开头的分散列表列表中。 协议驱动程序将保证所有预置的封装标头（ETH、IP、GRE）在物理上是连续的，并将位于数据包的第一 MDL。

协议和筛选器驱动程序不能确保 TCP 有效负载的总长度是缩减**MSS**值的精确倍数。 出于此原因，小型端口驱动程序和 Nic 必须更新隧道（外部） IP 标头。 Nic 必须生成尽可能多的完整大小的段，这是因为在 [**NDIS\_TCP\_大型\_发送\_卸载\_NET\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_tcp_large_send_offload_net_buffer_list_info)\_\_的信息。**LsoV2Transmit**OOB 信息。 每个 LSOv2 发送只能生成一个子**MSS**段。

微型端口驱动程序必须执行以下操作：

-   计算隧道（外部） IP 标头的校验和。
-   递增每个数据包的隧道（外部） IP 标头的 IP 标识（IP ID）值。 第一个数据包必须使用原始隧道（外部） IP 标头中的 IP ID。
-   递增每个数据包的传输（内部） IP 标头的 IP ID。 第一个数据包必须使用原始传输（内部） IP 标头中的 IP ID。
-   计算 TCP 标头和传输（内部） IP 标头的校验和。
-   确保将完整的标头（包括封装隧道（外部）标头）添加到每个生成的数据包中。

## <a name="related-topics"></a>相关主题


[卸载大 TCP 数据包的细分](offloading-the-segmentation-of-large-tcp-packets.md)

 

 






