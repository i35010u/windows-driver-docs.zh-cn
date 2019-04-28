---
title: 使用 IPsec 卸载版本 2 发送网络数据
description: 使用 IPsec 卸载版本 2 发送网络数据
ms.assetid: d3580313-a98b-4150-b344-e3e395ce68e9
keywords:
- IPsecOV2 WDK TCP/IP 传输，将数据发送
- 发送数据 WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bb98bbf7cab9961e7d5c2361a763a4ec9ed91234
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63346751"
---
# <a name="sending-network-data-with-ipsec-offload-version-2"></a>使用 IPsec 卸载版本 2 发送网络数据

\[IPsec 任务卸载功能已弃用，不应使用。\]




TCP/IP 传输提供的一个或多个 SAs，用于 IPsec 卸载版本 2 (IPsecOV2) 信息[OID\_TCP\_任务\_IPSEC\_卸载\_V2\_添加\_SA](https://msdn.microsoft.com/library/windows/hardware/ff569812) OID。 之前的微型端口驱动程序返回成功结果的 OID\_TCP\_任务\_IPSEC\_卸载\_V2\_添加\_SA，微型端口驱动程序初始化卸载句柄。 TCP/IP 传输请求要卸载的处理的微型端口驱动程序[ **NET\_缓冲区\_列表**](https://msdn.microsoft.com/library/windows/hardware/ff568388)通过中指定IPsecOV2信息结构[ **NDIS\_IPSEC\_卸载\_V2\_NET\_缓冲区\_列表\_信息**](https://msdn.microsoft.com/library/windows/hardware/ff565818)和[ **NDIS\_IPSEC\_卸载\_V2\_标头\_NET\_缓冲区\_列表\_信息**](https://msdn.microsoft.com/library/windows/hardware/ff565812)结构，都是一部分的**NET\_缓冲区\_列表**带外 (OOB) 的信息。

TCP/IP 传输提供中的卸载句柄**OffloadHandle**的成员[ **NDIS\_IPSEC\_卸载\_V2\_NET\_缓冲区\_列表\_信息**](https://msdn.microsoft.com/library/windows/hardware/ff565818)指定发送数据包的传输 （端到端连接） 部分的句柄的出站安全关联 (SA)。

TCP/IP 传输提供中的以下标头信息[ **NDIS\_IPSEC\_卸载\_V2\_标头\_NET\_缓冲区\_列表\_信息**](https://msdn.microsoft.com/library/windows/hardware/ff565812)结构：

-   标头的 AH 标头、 ESP 标头，或两者的偏移量。

-   下一个协议值 （等同于 ESP 尾部中包含的代码）。

-   用于组合的大量发送卸载 (LSO) 和 IPsec 卸载板长度。

此外，如果将通过隧道传输发送数据包，TCP/IP 传输提供[ **NDIS\_IPSEC\_卸载\_V2\_隧道\_NET\_缓冲区\_列表\_信息**](https://msdn.microsoft.com/library/windows/hardware/ff565843)结构。 此结构指定的卸载句柄发送数据包的隧道部分的出站 SA。 有关访问 OOB 信息的详细信息，请参阅[访问 NET\_缓冲区\_IPsec 卸载版本 2 中的列表信息](accessing-net-buffer-list-information-in-ipsec-offload-version-2.md)。

微型端口驱动程序提供对 OID 集请求的响应中的卸载句柄[OID\_TCP\_任务\_IPSEC\_卸载\_V2\_添加\_SA](https://msdn.microsoft.com/library/windows/hardware/ff569812). 有关 SAs 的详细信息，请参阅[IPsec 卸载版本 2 中管理安全关联](managing-security-associations-in-ipsec-offload-version-2.md)。

微型端口驱动程序时处理中的发送请求[ *MiniportSendNetBufferLists* ](https://msdn.microsoft.com/library/windows/hardware/ff559440)函数、 微型端口驱动程序：

-   验证硬件配置为处理 IPsec 卸载服务。 如果硬件未配置为处理 IPsec 卸载服务，微型端口驱动程序应处理在发送请求，而无需提供卸载服务。

-   验证中的图柄[ **NDIS\_IPSEC\_卸载\_V2\_NET\_缓冲区\_列表\_信息**](https://msdn.microsoft.com/library/windows/hardware/ff565818)并[ **NDIS\_IPSEC\_卸载\_V2\_隧道\_NET\_缓冲区\_列表\_信息**](https://msdn.microsoft.com/library/windows/hardware/ff565843)结构以确定是否需要 IPsec 加密处理。 卸载句柄值零指示应为执行的任何 IPsec 任务卸载[ **NET\_缓冲区\_列表**](https://msdn.microsoft.com/library/windows/hardware/ff568388)。 如果微型端口驱动程序找不到对应于指定的卸载句柄已卸载的 SA，发送数据包应失败，并**NDIS\_状态\_失败**值。

-   验证中的图柄[ **NDIS\_TCP\_LARGE\_发送\_卸载\_NET\_缓冲区\_列表\_信息**](https://msdn.microsoft.com/library/windows/hardware/ff567882)结构，以确定是否应为执行分段卸载[ **NET\_缓冲区\_列表**](https://msdn.microsoft.com/library/windows/hardware/ff568388)。

-   完成所有中发送的数据包所需的 AH 和 ESP 处理[ **NET\_缓冲区\_列表**](https://msdn.microsoft.com/library/windows/hardware/ff568388)。 当 NIC 执行 IPsec 上发送数据包的处理时，它执行加密操作的数据包数据。 TCP/IP 传输已构建框架数据包、 填充它 （如果有必要），并为其分配序列号和安全参数索引 (SPI)。 以进行组合 LSO 和 IPsec 卸载[ **NET\_缓冲区**](https://msdn.microsoft.com/library/windows/hardware/ff568376)可能具有 NIC 段大数据包时将被放弃的填充。 中指定的填充量**PadLength**的成员[ **NDIS\_IPSEC\_卸载\_V2\_标头\_NET\_缓冲区\_列表\_信息**](https://msdn.microsoft.com/library/windows/hardware/ff565812)结构。 分段的数据包可能需要填充，以支持 IPsec 操作。

协议驱动程序将请求 LSO 和 IPsecOV2 有数据包发送，它不将帧 ESP 尾部。 这是因为 ESP 尾部，如填充长度中的信息将会不准确的 NIC 已生成的最后一个段

 

 





