---
title: 在大规模发送卸载 (LSO) 中支持 NVGRE
description: 本部分介绍支持 NVGRE 中大量发送卸载 (LSO)
ms.assetid: 1EB1B8C2-85C1-4256-BE96-C8B9F1D222B6
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 833c4ca772178774ad31b040effd5e41183400fc
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56565850"
---
# <a name="supporting-nvgre-in-large-send-offload-lso"></a>在大规模发送卸载 (LSO) 中支持 NVGRE


NDIS 6.30 (Windows Server 2012) 引入了[网络虚拟化使用通用路由封装 (NVGRE)](network-virtualization-using-generic-routing-encapsulation--nvgre--task-offload.md)。 NDIS 微型端口、 协议和筛选器驱动程序和执行较大的 Nic 发送卸载 (LSO) 版本 2 (LSOV2) 应支持 NVGRE 的方式执行此操作。

**请注意**  此页面假定您熟悉中的信息[卸载分段的大型 TCP 数据包](offloading-the-segmentation-of-large-tcp-packets.md)。

 

如果[ **NDIS\_TCP\_发送\_将卸载\_补充\_NET\_缓冲区\_列表\_信息**](https://msdn.microsoft.com/library/windows/hardware/jj991957).**IsEncapsulatedPacket**是**TRUE**并**TcpIpChecksumNetBufferListInfo**带外 (OOB) 的信息是有效的这表示该 NVGRE需要的支持和 NIC 必须执行 LSOV2 卸载格式 NVGRE 数据包，满足以下条件：

-   仅在值[ **NDIS\_TCP\_LARGE\_发送\_卸载\_NET\_缓冲区\_列表\_信息**](https://msdn.microsoft.com/library/windows/hardware/ff567882).**LsoV2Transmit**结构都有效。 中的值不能引用 NIC 和微型端口驱动程序**NDIS\_TCP\_LARGE\_发送\_卸载\_NET\_缓冲区\_列表\_INFO**。**LsoV1Transmit**结构。
-   [ **NDIS\_TCP\_LARGE\_发送\_卸载\_NET\_缓冲区\_列表\_信息**](https://msdn.microsoft.com/library/windows/hardware/ff567882).**LsoV2Transmit**。**TcpHeaderOffset**成员没有正确的偏移量的值，并且必须不能由 NIC 或微型端口驱动程序。

若要在 LSOV2 支持 NVGRE，协议和筛选器驱动程序必须进行以下更改：

-   减少**MSS**中的值[ **NDIS\_TCP\_大\_发送\_卸载\_NET\_缓冲区\_列表\_信息**](https://msdn.microsoft.com/library/windows/hardware/ff567882)。**LsoV2Transmit**结构来应对新 GRE 标头。
-   向下可能无法减少的精确倍数的 TCP 有效负载长度发送**MSS**值。
-   调整**InnerFrameOffset**， **TransportIpHeaderRelativeOffset**，并**TcpHeaderRelativeOffset**中的值[ **NDIS\_TCP\_发送\_将卸载\_补充\_NET\_缓冲区\_列表\_信息**](https://msdn.microsoft.com/library/windows/hardware/jj991957)结构来应对 GRE标头。

Nic 微型端口驱动程序可能会通过**InnerFrameOffset**， **TransportIpHeaderRelativeOffset**，并**TcpHeaderRelativeOffset** 中提供值[ **NDIS\_TCP\_发送\_卸载\_补充\_NET\_缓冲区\_列表\_信息**](https://msdn.microsoft.com/library/windows/hardware/jj991957)结构。 NIC 或微型端口驱动程序可能会执行任何所需的标头检查隧道 （外部） IP 标头或后续标头来验证这些偏移量。

微型端口驱动程序必须处理的情况其中[ **NDIS\_TCP\_发送\_将卸载\_补充\_NET\_缓冲区\_列表\_INFO**](https://msdn.microsoft.com/library/windows/hardware/jj991957)。**InnerFrameOffset**可能在不同散播-聚集列表比数据包的开头。 所有预置的封装标头 (ETH，IP，GRE) 将是物理上连续的且将在数据包的第一个 MDL 可以保证协议驱动程序。

协议和筛选器驱动程序不能确保总 TCP 有效负载长度是减少的精确倍数**MSS**值。 出于此原因，微型端口驱动程序和 Nic 必须更新 （外部） 隧道 IP 标头。 Nic 必须尽可能减少基于生成多大段**MSS**中的值[ **NDIS\_TCP\_大\_发送\_卸载\_NET\_缓冲区\_列表\_信息**](https://msdn.microsoft.com/library/windows/hardware/ff567882)。**LsoV2Transmit** OOB 信息。 只有一个子-**MSS**段可能会生成针对每个 LSOv2 发送。

微型端口驱动程序必须执行以下操作：

-   计算的校验和，隧道 （外部） IP 标头。
-   递增的隧道 （外部） IP 标头的每个数据包的 IP 标识号 (IP ID) 值。 第一个数据包必须使用 IP ID 中的原始隧道 （外部） IP 标头。
-   增加每个数据包的传输 （内部联接） IP 标头的 IP ID。 第一个数据包必须在原始传输 （内部） IP 标头中使用 IP ID。
-   计算的校验和，TCP 标头和传输 （内部） IP 标头。
-   请确保所完成的标头，包括封装隧道 （外部） 标头添加到生成的每个数据包。

## <a name="related-topics"></a>相关主题


[卸载大型 TCP 数据包的分段](offloading-the-segmentation-of-large-tcp-packets.md)

 

 






