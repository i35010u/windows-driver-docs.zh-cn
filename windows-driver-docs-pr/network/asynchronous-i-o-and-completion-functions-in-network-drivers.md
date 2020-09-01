---
title: 网络驱动程序中的异步 I/O 和 Completion 函数
description: 网络驱动程序中的异步 I/O 和 Completion 函数
ms.assetid: fbb940d8-41ad-4f66-998b-f5dc829b54cc
keywords:
- 网络驱动程序 WDK，异步操作
- 异步 i/o WDK 网络
- 完成函数 WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 66c291cb42fc7ce8a04d068214fb0dd1209f6d81
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89215998"
---
# <a name="asynchronous-io-and-completion-functions-in-network-drivers"></a>网络驱动程序中的异步 I/O 和 Completion 函数





延迟在某些网络操作中是固有的。 由于这种延迟，小型端口驱动程序提供的许多高边缘功能和协议驱动程序的较小边缘功能旨在支持异步操作。 网络驱动程序依赖于异步处理大多数操作，而不是浪费等待循环中等待某个耗时的任务完成或硬件事件的 CPU 周期。

使用 *完成* 函数支持异步网络 i/o。 下面的示例说明了如何对网络 *发送* 操作使用完成功能，但此相同的机制适用于通过协议或微型端口驱动程序执行的许多其他操作。

当协议驱动程序调用 NDIS 来发送数据包时，会导致调用微型端口驱动程序的 [*MiniportSendNetBufferLists*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_send_net_buffer_lists) 函数，微型端口驱动程序可以尝试立即完成此请求并返回相应的状态值。 对于同步操作，可能的响应是 \_ \_ 成功完成发送的 ndis 状态成功，ndis \_ 状态 \_ 资源，以及 \_ \_ 指示某种故障的 ndis 状态故障。

但发送操作可能需要一些时间才能完成，而微型端口驱动程序 (或 NDIS) 会将数据包排队，并等待 NIC 指示发送操作的结果。 微型端口驱动程序 *MiniportSendNetBufferLists* 函数可以通过返回 NDIS 状态为 "挂起" 的状态值来异步处理此操作 \_ \_ 。 当微型端口驱动程序完成发送操作时，它将调用完成函数 [**NdisMSendNetBufferListsComplete**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsendnetbufferlistscomplete)，并将一个指针传递到已发送的数据包说明符。 此信息将传递给协议驱动程序，即信号完成。

大多数需要延长时间才能完成的驱动程序操作都支持带有类似完成函数的异步操作。 此类函数的名称**NdisM*Xxx***。

还提供了完成函数来执行以下操作：

-   设置和查询配置。

-   重置硬件。

-   指示状态。

-   指示接收的数据。

-   传输已接收数据。

 

