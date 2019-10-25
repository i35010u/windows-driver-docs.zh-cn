---
title: NET_BUFFER 数据打包
description: NET_BUFFER 数据打包
ms.assetid: f0d539ab-c6ed-4cd9-9891-ef4235016d50
keywords:
- NDIS WDK，发送和接收数据
- 数据打包 WDK 网络
- 发送数据 WDK 网络
- 接收数据 WDK 网络
- NDIS_PACKET
- NET_BUFFER 数据打包 WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4a33ddb5c21b601d255f9897e2a99dbd9ee7aced
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844930"
---
# <a name="net_buffer-data-packaging"></a>NET\_缓冲区数据打包





数据打包在 NDIS 6.0 中进行了重新设计。 基于[**NDIS\_数据包**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff557086(v=vs.85))结构的发送和接收体系结构已替换为基于[**net\_缓冲区**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer)和[**net\_缓冲区\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)结构的体系结构。 NET\_BUFFER 结构是等效于 NDIS\_数据包结构的函数。 NET\_缓冲区结构为网络数据指定了缓冲区（MDL 链），并为 NDIS、协议驱动程序和微型端口驱动程序指定了保留空间。 NET\_缓冲区结构可以在由 NET\_BUFFER\_列表结构描述的列表中链接在一起。 NET\_BUFFER\_列表结构还为应用于列表中所有 NET\_缓冲结构的带外（OOB）数据提供存储。

Microsoft 下一代网络驱动程序堆栈中的所有组件，包括 TCP/IP 传输和 Winsock，使用 NET\_BUFFER 数据打包。 在整个驱动程序堆栈中进行统一的数据打包，无需重新打包数据、简化数据处理并减少函数调用的数量。

为了适应使用 NDIS\_数据包结构的旧驱动程序，NDIS 6.0 将 NDIS\_数据包结构转换为 NET\_缓冲结构，反之亦然。 这种转换对于 NDIS 驱动程序是透明的。

NDIS 将驱动程序的数据回填要求传播到更高级别的驱动程序。 在分配 NET\_缓冲区和 NET\_缓冲区\_用于发送数据的列表结构时，较高级别的驱动程序会分配足够的数据空间以容纳堆栈中的所有较低级别的驱动程序。 因此，较低级别的驱动程序无需分配额外的缓冲区空间来容纳特定于层的标头。 相反，他们可以使用预分配的回填空间来实现此目的。

有关 NET\_缓冲区体系结构的详细信息，请参阅[net\_Buffer 体系结构](net-buffer-architecture.md)。

 

 





