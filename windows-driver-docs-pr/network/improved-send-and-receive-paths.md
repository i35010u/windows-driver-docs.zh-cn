---
title: 改进的发送和接收路径
description: 改进的发送和接收路径
ms.assetid: 7edecb49-576f-4058-92e8-39f14268a130
keywords:
- NDIS WDK，发送和接收数据
- 发送数据 WDK 网络
- 接收数据 WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: dd9f2f76835eede23309aa5da68b362719853714
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72827355"
---
# <a name="improved-send-and-receive-paths"></a>改进的发送和接收路径





为了提高性能，已按如下方式改进了 NDIS 6.0 发送和接收路径：

-   所有 NDIS 6.0 和更高版本的驱动程序发送和接收函数都可以使用单个函数调用传输链接的[**网络\_缓冲区\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)结构及其关联[**网络\_缓冲区**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer)结构的列表。 这种对真正 multipacket 发送和接收操作的支持显著减少了驱动程序必须进行的函数调用数。

-   在调用 send 或 receive 函数时，在调度\_级别上运行的驱动程序可以指示其 IRQL 到 NDIS。 当 NDIS 随后调用堆栈中的其他驱动程序时，这些驱动程序无需测试 IRQL 或将其设置为调度\_级别。 这会减少与在关键代码部分中测试和设置 IRQL 相关的开销。

-   当驱动程序在驱动程序堆栈中向上和向下传递数据包时，它们可以请求 NDIS 调整网络\_缓冲区数据偏移量，以容纳标头信息。 发送数据包时，驱动程序可以扩展已使用的数据空间，以容纳驱动程序的标头信息。 当指明接收数据包时，驱动程序在访问其标头信息后可能会减少使用的数据空间。 此功能可以动态调整网络\_缓冲区结构中的已用数据空间，而无需分配和释放内存或复制数据，从而减少了处理网络数据所需的开销。

有关 NDIS 6.0 中的发送和接收数据处理的详细信息，请参阅[NET\_BUFFER 体系结构](net-buffer-architecture.md)。

 

 





