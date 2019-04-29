---
title: 改进的发送和接收路径
description: 改进的发送和接收路径
ms.assetid: 7edecb49-576f-4058-92e8-39f14268a130
keywords:
- NDIS WDK、 发送和接收数据
- 发送数据 WDK 网络
- 接收数据 WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b3abde686105c8f92a86c9068e75647d1ad58e86
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63363157"
---
# <a name="improved-send-and-receive-paths"></a>改进的发送和接收路径





NDIS 6.0 发送和接收路径已得到改进，如下所示增强性能：

-   NDIS 6.0 和更高版本的驱动程序的所有发送和接收函数可将传输的链接的列表[ **NET\_缓冲区\_列表**](https://msdn.microsoft.com/library/windows/hardware/ff568388)结构和其关联[**NET\_缓冲区**](https://msdn.microsoft.com/library/windows/hardware/ff568376)具有单个函数调用的结构。 这种支持的 true multipacket 发送和接收操作大大减少了驱动程序必须进行的函数调用数。

-   当调用发送或接收函数，在调度运行的驱动程序\_级别可以指示其 IRQL 到 NDIS。 当 NDIS 随后发出对其他驱动程序的调用堆栈中时，不需要这些驱动程序以测试 IRQL 或将其设置为调度\_级别。 这将减少测试和关键代码部分中设置的 IRQL 与相关联的开销。

-   如果驱动程序通过向上和向下驱动程序堆栈的数据包，他们可以请求 NDIS 调整 NET\_缓冲区数据偏移量，以适应标头信息。 在发送数据包时，驱动程序可以扩展使用的数据空间来容纳驱动程序的标头信息。 该驱动程序完成后，驱动程序时，该值指示接收数据包，可以减少使用的数据空间访问其标头信息。 此功能可以动态调整.NET 中使用的数据空间\_缓冲区结构，而无需分配和释放内存或复制数据，可以减少需要处理网络数据的开销。

有关详细信息大约发送和接收 NDIS 6.0 中的数据处理，请参阅[NET\_缓冲体系结构](net-buffer-architecture.md)。

 

 





