---
title: 在校验和卸载中支持 NVGRE
description: 本部分介绍支持 NVGRE 中校验和卸载
ms.assetid: 933EE18B-917A-40BC-87AA-0F463615A082
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a50e45082a5e9fdb1035ed073ec8bf776d314b50
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56562085"
---
# <a name="supporting-nvgre-in-checksum-offload"></a>在校验和卸载中支持 NVGRE


NDIS 6.30 (Windows Server 2012) 引入了[网络虚拟化使用通用路由封装 (NVGRE)](network-virtualization-using-generic-routing-encapsulation--nvgre--task-offload.md)。 NDIS 微型端口、 协议和筛选器驱动程序和卸载校验和任务的 Nic 应该这样做支持 NVGRE 的方式。

**请注意**  此页面假定您熟悉中的信息[卸载校验和任务](offloading-checksum-tasks.md)。

 

如果[ **NDIS\_TCP\_发送\_将卸载\_补充\_NET\_缓冲区\_列表\_信息**](https://msdn.microsoft.com/library/windows/hardware/jj991957).**IsEncapsulatedPacket**是**TRUE**并**TcpIpChecksumNetBufferListInfo**带外 (OOB) 的信息是有效的这表示该 NVGRE需要的支持和 NIC 必须计算的校验和 （外部） 隧道 IP 标头、 传输 （内部联接） IP 标头和 TCP 或 UDP 标头。

**IsIPv4**并**IsIPv6**标记中[ **NDIS\_TCP\_IP\_校验和\_NET\_缓冲区\_列表\_信息**](https://msdn.microsoft.com/library/windows/hardware/ff567877)结构指示隧道 （外部） IP 标头的 IP 标头版本。 NIC 必须分析传输 （内部） IP 标头以确定该标头的 IP 版本。 因为允许混合模式的数据包 (请参阅[ **NDIS\_封装\_数据包\_任务\_卸载**](https://msdn.microsoft.com/library/windows/hardware/jj991956))，NIC 必须假定内部和外部 IP 标头将具有相同版本的 IP 标头。

Nic 微型端口驱动程序可能会通过**InnerFrameOffset**， **TransportIpHeaderRelativeOffset**，并**TcpHeaderRelativeOffset** 中提供值[ **NDIS\_TCP\_发送\_卸载\_补充\_NET\_缓冲区\_列表\_信息**](https://msdn.microsoft.com/library/windows/hardware/jj991957)结构。 NIC 或微型端口驱动程序可能会执行任何所需的标头检查隧道 （外部） IP 标头或后续标头来验证这些偏移量。

请注意，当[ **NDIS\_TCP\_发送\_将卸载\_补充\_NET\_缓冲区\_列表\_信息**](https://msdn.microsoft.com/library/windows/hardware/jj991957).**IsEncapsulatedPacket**为 TRUE 时，现有的标头的偏移量字段[ **NDIS\_TCP\_大\_发送\_卸载\_NET\_缓冲区\_列表\_信息**](https://msdn.microsoft.com/library/windows/hardware/ff567882)。**LsoV2Transmit**。**TcpHeaderOffset**并[ **NDIS\_TCP\_IP\_校验和\_NET\_缓冲区\_列表\_信息**](https://msdn.microsoft.com/library/windows/hardware/ff567877).**传输**。**TcpHeaderOffset**，将不能正确的值，而且必须不能由 NIC 或驱动程序。

微型端口驱动程序必须处理的情况其中[ **NDIS\_TCP\_发送\_将卸载\_补充\_NET\_缓冲区\_列表\_INFO**](https://msdn.microsoft.com/library/windows/hardware/jj991957)。**InnerFrameOffset**可能在不同散播-聚集列表比数据包的开头。 所有预置的封装标头 (ETH，IP，GRE) 将是物理上连续的且将在数据包的第一个 MDL 可以保证协议驱动程序。

## <a name="checksum-validation"></a>校验和验证


NVGRE 的校验和验证大体上是相同的其他如。

如果微型端口收到[OID\_TCP\_卸载\_参数](https://msdn.microsoft.com/library/windows/hardware/ff569807)OID 请求和成功，则为**NDIS\_封装\_类型\_GRE\_MAC** (请参阅[ **NDIS\_卸载\_参数**](https://msdn.microsoft.com/library/windows/hardware/ff566706))，NIC 必须对隧道 （执行校验和验证外部） 的 IP 标头、 传输 （内部联接） IP 标头和 TCP 或 UDP 标头。

对于具有 IPv4 隧道 （外部） 标头和 IPv4 传输 （内部联接） 标头的封装数据包，微型端口驱动程序应设**IpChecksumSucceeded**中的标志[ **NDIS\_TCP\_IP\_CHECKSUM\_NET\_缓冲区\_列表\_信息**](https://msdn.microsoft.com/library/windows/hardware/ff567877)结构，仅当这两个 IP 标头和校验和验证成功。 对于具有隧道 （外部） IPv4 标头和传输 （内部联接） IPv4 标头的封装数据包，微型端口驱动程序应设**IpChecksumFailed**标志，如果任一 IP 标头和校验和验证失败。

 

 





