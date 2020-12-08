---
title: 标头数据拆分体系结构
description: 标头数据拆分体系结构
keywords:
- 标头-数据拆分 WDK，体系结构
- 标头-数据拆分提供程序 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 958cfa772df7e0d45dbdc8808ea4e7f6b81583fc
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96821371"
---
# <a name="header-data-split-architecture"></a>标头数据拆分体系结构





标头-数据拆分提供程序通过将接收的以太网帧中的标头和数据拆分为单独的缓冲区来提高网络性能。 标头-数据拆分提供程序包括一个网络接口卡 (NIC) ，以及用于为 NIC 提供服务的 NDIS 6.1 或更高版本的微型端口驱动程序。

下图显示了标头数据拆分结构。

![说明标头-数据拆分体系结构的关系图](images/hdsplitarchitecture.png)

微型端口驱动程序接收来自 NDIS 的配置信息，以设置用于标头数据拆分接收操作的 NIC。 此外，小型小型驱动程序驱动程序将 NIC 的服务公开给用于运行时操作（如发送和接收操作）的 NDIS。

支持标头数据拆分操作的 NIC 接收以太网帧，并将标头和数据拆分为单独的接收缓冲区。

微型端口驱动程序使用常规 NDIS 接收函数将接收的数据指示到 NDIS。 同时，驱动程序必须在指示收到的数据时，将确切的 [**网络 \_ 缓冲区**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer) 结构分配给 [**网络 \_ 缓冲区 \_ 列表**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list) 结构。 有关详细信息，请参阅 [指示收到的以太网帧](indicating-received-ethernet-frames.md)。

对于标头数据拆分，接收指示中的 [**NET \_ BUFFER**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer) 结构使用单独的内存描述符列表拆分接收的以太网帧， (MDLs) 标头和数据。 而且， [**net \_ buffer \_ 列表**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list) 结构包含网络 \_ 缓冲区列表信息中的标头数据拆分信息 \_ 。

下图显示了接收的帧、拆分缓冲区和标头缓冲区的内存布局。

![阐释接收的帧、拆分缓冲区和标头缓冲区的内存布局的关系图](images/hdspllitbuffers.png)

标头缓冲区应全部位于连续的存储块中。

*上层协议* 是 IP 传输协议，例如 TCP、UDP 或 ICMP。

**注意**  出于定义标头数据拆分要求，IPsec 不被视为上层协议。 有关拆分 IPsec 帧的详细信息，请参阅 [拆分 Ipsec 帧](splitting-ipsec-frames.md)。

 

 

