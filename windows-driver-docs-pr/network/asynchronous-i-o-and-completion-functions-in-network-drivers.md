---
title: 网络驱动程序中的异步 I/O 和 Completion 函数
description: 网络驱动程序中的异步 I/O 和 Completion 函数
ms.assetid: fbb940d8-41ad-4f66-998b-f5dc829b54cc
keywords:
- 网络驱动程序 WDK，异步操作
- 网络的异步 I/O WDK
- 完成 WDK 网络函数
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 078bc15a489bb0c7edac4b335d08026942d2911c
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384411"
---
# <a name="asynchronous-io-and-completion-functions-in-network-drivers"></a>网络驱动程序中的异步 I/O 和 Completion 函数





某些网络操作中固有的延迟。 因为此延迟，很多的微型端口驱动程序和协议驱动程序的较低边缘函数提供的上边缘功能旨在支持异步操作。 而不是浪费 CPU 周期为一些耗时的任务完成或硬件事件发出信号，网络驱动程序依赖于以异步方式处理大多数操作的能力循环中等待。

通过使用支持异步网络 I/O*完成*函数。 下面的示例演示如何针对某个网络使用完成函数*发送*操作，但此相同的机制存在许多其他协议或微型端口驱动程序执行的操作。

当协议驱动程序调用 NDIS 发送数据包时，从而导致微型端口驱动程序调用[ *MiniportSendNetBufferLists* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_send_net_buffer_lists)函数，微型端口驱动程序可以尝试立即完成此请求并作为结果返回相应的状态的值。 为同步操作的可能响应是 NDIS\_状态\_成功的成功完成此次发送，NDIS\_状态\_资源和 NDIS\_状态\_失败表示某种类型的失败。

但发送操作可能需要一些时间才能完成时的微型端口驱动程序 （或 NDIS） 队列数据包并等待 NIC 以指示发送操作的结果。 微型端口驱动程序*MiniportSendNetBufferLists*函数可以以异步方式处理此操作，通过返回在 status 值为 NDIS\_状态\_PENDING。 微型端口驱动程序完成发送操作，它调用完成函数时， [ **NdisMSendNetBufferListsComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismsendnetbufferlistscomplete)，指针传递给数据包描述符的已发送。 此信息传递给协议驱动程序，信号传输完成。

可能需要较长的时间来完成与完成相似的支持异步操作的大多数驱动程序操作。 此类函数具有名称的窗体**NdisM*Xxx*完成**。

完成函数也将提供给：

-   设置和查询的配置。

-   重置硬件。

-   指示状态。

-   指示接收到的数据。

-   传输接收的数据。

 

 





