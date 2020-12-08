---
title: NET_BUFFER 数据打包
description: NET_BUFFER 数据打包
keywords:
- NDIS WDK，发送和接收数据
- 数据打包 WDK 网络
- 发送数据 WDK 网络
- 接收数据 WDK 网络
- NDIS_PACKET
- NET_BUFFER 数据打包 WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b729cf87b0e41d8dc8e4eee43d3c89cf6edccf6e
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96825449"
---
# <a name="net_buffer-data-packaging"></a>网络 \_ 缓冲区数据打包





数据打包在 NDIS 6.0 中进行了重新设计。 基于 [**NDIS \_ 包**](/previous-versions/windows/hardware/network/ff557086(v=vs.85)) 结构的发送和接收体系结构已替换为基于 [**网络 \_ 缓冲区**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer) 和 [**网络 \_ 缓冲区 \_ 列表**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list) 结构的体系结构。 NET \_ BUFFER 结构是等效于 NDIS 包结构的功能 \_ 。 NET \_ BUFFER 结构指定网络数据的 (MDL 链) ，以及 NDIS、协议驱动程序和微型端口驱动程序的保留空间。 网络 \_ 缓冲区结构可以在由网络 \_ 缓冲区列表结构描述的列表中链接在一起 \_ 。 网络 \_ 缓冲区 \_ 列表结构还为带外 (OOB 提供适用于列表中所有网络缓冲区结构的带外 OOB) 数据 \_ 。

Microsoft 下一代网络驱动程序堆栈中的所有组件，包括 TCP/IP 传输和 Winsock，都使用网络 \_ 缓冲区数据打包。 在整个驱动程序堆栈中进行统一的数据打包，无需重新打包数据、简化数据处理并减少函数调用的数量。

为了适应使用 NDIS 数据包结构的旧驱动程序 \_ ，ndis 6.0 将 ndis \_ 数据包结构转换为网络 \_ 缓冲区结构，反之亦然。 这种转换对于 NDIS 驱动程序是透明的。

NDIS 将驱动程序的数据回填要求传播到更高级别的驱动程序。 在 \_ 为发送数据分配网络缓冲区和网络 \_ 缓冲区 \_ 列表结构时，较高级别的驱动程序会分配足够的数据空间，以容纳堆栈中的所有较低级别的驱动程序。 因此，较低级别的驱动程序无需分配额外的缓冲区空间来容纳特定于层的标头。 相反，他们可以使用预分配的回填空间来实现此目的。

有关 NET \_ buffer 体系结构的详细信息，请参阅 [Net \_ buffer 体系结构](net-buffer-architecture.md)。

 

