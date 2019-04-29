---
title: 卸载校验和任务
description: 卸载校验和任务
ms.assetid: 5fb2f379-c357-4ec3-b103-bdbe23fcc033
keywords:
- 任务卸载，WDK TCP/IP 传输，校验和任务
- 校验和任务 WDK 网络
ms.date: 09/19/2018
ms.localizationpriority: medium
ms.openlocfilehash: 36e50d3218236b52430e2f0e00f1b9d47a09453c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63359196"
---
# <a name="offloading-checksum-tasks"></a>卸载校验和任务

NDIS 支持在运行时将 TCP/IP 校验和任务。

> [!NOTE]
> 校验和卸载带外 (OOB) 数据存储在[ **NET\_缓冲区\_列表**](https://msdn.microsoft.com/library/windows/hardware/ff568388)信息数组。 OOB 数据有关的详细信息，请参阅[访问 TCP/IP 卸载 NET\_缓冲区\_列出信息](accessing-tcp-ip-offload-net-buffer-list-information.md)。

然后再将传递到微型端口驱动程序 NET\_缓冲区\_列表结构的微型端口驱动程序将在其执行校验和任务的数据包，TCP/IP 传输指定 NET与相关联的校验和信息\_缓冲区\_列表结构。 此信息由指定[ **NDIS\_TCP\_IP\_校验和\_NET\_缓冲区\_列表\_信息**](https://msdn.microsoft.com/library/windows/hardware/ff567877)结构，它是网络的一部分\_缓冲区\_与网络相关联的列表信息 （带外数据）\_缓冲区\_列表结构。

卸载 TCP 数据包的校验和计算之前, TCP/IP 传输计算 1 的补数的总和 TCP pseudoheader。 TCP/IP 传输计算 pseudoheader，包括源 IP 地址、 目标 IP 地址、 协议和 TCP 数据包的 TCP 长度中的所有字段中的 1 的补数之和。 TCP/IP 传输会为 pseudoheader TCP 标头的校验和字段中输入 1 的补数之和。

1 的补数的总和通过 TCP/IP 传输提供 pseudoheader 为 NIC 提供了在发送数据包的实际 TCP 校验和计算最早开始时间。 若要计算的实际 TCP 校验和，NIC 计算 TCP 校验和 （适用于 TCP 标头和有效负载中） 的变量部分，此校验和 1 的补数的总和计算通过 TCP/IP 传输 pseudoheader 并添加计算的 16 位一个的校验和的补数。 有关计算此类校验和的详细信息，请参阅 RFC 793 和 RFC 1122。

> [!NOTE]
> TCP/IP 传输计算 1 的补数的总和 pseudoheader UDP 数据包，因为它会为 TCP 数据包时，并将值存储在 UDP 标头的校验和字段使用相同的步骤。

请注意，TCP/IP 传输始终将确保数据包的 IP 标头中的校验和字段设置为零，然后再将数据包传递到基础的微型端口驱动程序。 微型端口驱动程序应忽略 IP 标头中的校验和字段。 微型端口驱动程序不需要验证校验和字段设置为零，并且不需要将此字段设置为零。

收到 NET 后\_缓冲区\_列表中的结构及其[ *MiniportSendNetBufferLists* ](https://msdn.microsoft.com/library/windows/hardware/ff559440)或者[ **MiniportCoSendNetBufferLists** ](https://msdn.microsoft.com/library/windows/hardware/ff559365)函数，微型端口驱动程序通常执行以下的校验和处理：

1.  微型端口驱动程序调用[ **NET\_缓冲区\_列表\_信息**](https://msdn.microsoft.com/library/windows/hardware/ff568401)宏替换 *\_Id*的**TcpIpChecksumNetBufferListInfo**以获取[ **NDIS\_TCP\_IP\_校验和\_NET\_缓冲区\_列表\_INFO** ](https://msdn.microsoft.com/library/windows/hardware/ff567877)结构。

2.  微型端口驱动程序测试**IsIPv4**并**IsIPv6**标志在 NDIS\_TCP\_IP\_校验和\_NET\_缓冲区\_列表\_信息结构。 如果这两个**IsIPv4**并**IsIPv6**标志未设置、 NIC 不应执行对数据包的任何校验和操作。

3.  如果**IsIPv4**或**IsIPv6**设置标志，微型端口驱动程序测试**TcpChecksum**， **UdpChecksum**，和**IpHeaderChecksum**标志以确定 NIC 数据包应计算的校验和。

4.  微型端口驱动程序将数据包传递到 NIC，计算的数据包的适当校验和。 如果数据包具有隧道 IP 标头和传输 IP 标头，支持 IP 校验和卸载的 NIC 只能在隧道标头上执行 IP 校验和任务。 TCP/IP 传输上传输 IP 标头执行 IP 校验和任务。

之前，该值指示[ **NET\_缓冲区\_列表**](https://msdn.microsoft.com/library/windows/hardware/ff568388)结构对于它在其执行校验和任务的接收数据包，微型端口驱动程序来验证相应的校验和并设置适当*Xxx * * * ChecksumFailed** 或*Xxx * * * ChecksumSucceeded** 中 NDIS 标志\_TCP\_IP\_校验和\_NET\_缓冲区\_列表\_信息结构。

关闭地址校验和卸载时启用大量发送卸载 (LSO) 不会阻止从计算并将校验和插入由 LSO 功能生成的数据包中的微型端口驱动程序。 若要禁用地址校验和卸载在这种情况下用户还必须禁用 LSO。

 

 





