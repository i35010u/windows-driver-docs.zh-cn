---
title: 在大规模发送卸载 (LSO) 中支持 NVGRE
description: '本部分介绍 (LSO 的大规模发送卸载中的支持 NVGRE) '
ms.assetid: 1EB1B8C2-85C1-4256-BE96-C8B9F1D222B6
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 26d2f62b24604cfe1d2eae5609cec9fd099286c7
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89207397"
---
# <a name="supporting-nvgre-in-large-send-offload-lso"></a>在大规模发送卸载 (LSO) 中支持 NVGRE


 (Windows Server 2012) NDIS 6.30 介绍了 [使用通用路由封装的网络虚拟化 (NVGRE) ](network-virtualization-using-generic-routing-encapsulation--nvgre--task-offload.md)。 执行大型发送卸载 (LSO) 版本 2 (LSOV2) 的 NDIS 微型端口、协议和筛选器驱动程序和 Nic 应该以支持 NVGRE 的方式实现此目的。

**注意**   本页假设你熟悉如何[分担大 TCP 数据包的分段](offloading-the-segmentation-of-large-tcp-packets.md)。

 

如果 [**NDIS \_ TCP \_ 发送将 \_ 卸载 \_ 补充的 \_ 网络 \_ 缓冲区 \_ 列表 \_ 信息**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_tcp_send_offloads_supplemental_net_buffer_list_info)。**IsEncapsulatedPacket** 为 **TRUE** ，并且 **TCPIPCHECKSUMNETBUFFERLISTINFO** 带外 (OOB) 信息有效，这表示需要 NVGRE 支持，而 NIC 必须在 NVGRE 格式的数据包上执行 LSOV2 卸载，条件如下：

-   仅 [**NDIS \_ TCP \_ 大规模 \_ 发送 \_ 卸载 \_ 网络 \_ 缓冲区 \_ 列表 \_ 信息**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_tcp_large_send_offload_net_buffer_list_info)中的值。**LsoV2Transmit** 结构有效。 NIC 和微型端口驱动程序不得引用 **NDIS \_ TCP \_ 大规模 \_ 发送 \_ 卸载 \_ 网络 \_ 缓冲区 \_ 列表 \_ 信息**中的值。**LsoV1Transmit** 结构。
-   [**NDIS \_ TCP \_ 大规模 \_ 发送 \_ 卸载 \_ 网络 \_ 缓冲区 \_ 列表 \_ 信息**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_tcp_large_send_offload_net_buffer_list_info)。**LsoV2Transmit**。**TcpHeaderOffset**成员没有正确的偏移值，且不能由 NIC 或微型端口驱动程序使用。

若要支持 LSOV2 中的 NVGRE，协议和筛选器驱动程序必须进行以下更改：

-   减少[**NDIS \_ TCP \_ 大规模 \_ 发送 \_ 卸载 \_ 网络 \_ 缓冲区 \_ 列表 \_ 信息**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_tcp_large_send_offload_net_buffer_list_info)中的**MSS**值。**LsoV2Transmit**要用于新的 GRE 标头的 LsoV2Transmit 结构。
-   发送一个 TCP 负载长度，该长度可能不是已减少的 **MSS** 值的准确倍数。
-   调整[**NDIS \_ TCP \_ 发送 \_ \_ \_ \_ \_ \_ **](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_tcp_send_offloads_supplemental_net_buffer_list_info)中的**InnerFrameOffset**、 **TransportIpHeaderRelativeOffset**和**TcpHeaderRelativeOffset**值，以考虑 GRE 标头。

Nic 和微型端口驱动程序可以使用[**NDIS \_ TCP \_ 发送 \_ \_ \_ \_ \_ \_ **](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_tcp_send_offloads_supplemental_net_buffer_list_info)中提供的**InnerFrameOffset**、 **TransportIpHeaderRelativeOffset**和**TcpHeaderRelativeOffset**值。 NIC 或微型端口驱动程序可以在隧道上执行任何所需的标头检查 (外部) IP 标头或后续标头来验证这些偏移量。

微型端口驱动程序必须处理 [**NDIS \_ TCP \_ 发送 \_ 卸载补充的 \_ \_ 网络 \_ 缓冲区 \_ 列表 \_ 信息**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_tcp_send_offloads_supplemental_net_buffer_list_info)的情况。**InnerFrameOffset** 可能在不同于数据包开头的分散列表列表中。 协议驱动程序将保证所有预置的封装标头 (ETH、IP、GRE) 在物理上是连续的，并将位于数据包的第一 MDL。

协议和筛选器驱动程序不能确保 TCP 有效负载的总长度是缩减 **MSS** 值的精确倍数。 出于此原因，小型端口驱动程序和 Nic 必须 (外部) IP 标头更新隧道。 Nic 必须根据[**NDIS \_ TCP \_ 大规模 \_ 发送 \_ 卸载 \_ 网络 \_ 缓冲区 \_ 列表 \_ 信息**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_tcp_large_send_offload_net_buffer_list_info)中的 "减少的**MSS** " 值生成尽可能多的全尺寸段。**LsoV2Transmit** OOB 信息。 每个 LSOv2 发送只能生成一个子**MSS** 段。

微型端口驱动程序必须执行以下操作：

-   计算隧道 (外部) IP 标头的校验和。
-   递增 IP ID (IP ID) 隧道的 ip 标识， (每个数据包的外部) IP 标头。 第一个数据包必须使用原始隧道中的 IP ID (外部) IP 标头。
-   为每个数据包递增传输 (内部) IP 标头的 IP ID。 第一个数据包必须使用原始传输 (内部) IP 标头中的 IP ID。
-   计算 TCP 标头的校验和和传输 (内部) IP 标头。
-   确保将完整的标头（包括封装隧道 (外部) 标头添加到每个生成的数据包中。

## <a name="related-topics"></a>相关主题


[卸载大型 TCP 数据包的段](offloading-the-segmentation-of-large-tcp-packets.md)

 

