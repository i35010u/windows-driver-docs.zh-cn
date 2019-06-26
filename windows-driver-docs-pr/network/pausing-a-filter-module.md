---
title: 暂停筛选器模块
description: 暂停筛选器模块
ms.assetid: da75b92d-b662-416a-b350-e5384b870b7f
keywords:
- 筛选器模块 WDK 连接网络、 暂停
- 正在暂停的筛选器模块
- 筛选器驱动程序 WDK 网络，暂停筛选器模块
- NDIS 筛选器驱动程序 WDK，暂停筛选器模块
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 14b6670906e5fbaa536b81adcbc6682e537b93c5
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384546"
---
# <a name="pausing-a-filter-module"></a>暂停筛选器模块





若要暂停正在运行的筛选器模块，NDIS 调用筛选器驱动程序[ *FilterPause* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-filter_pause)函数。 筛选器模块进入*暂停*中执行的开始处的状态*FilterPause*函数。

NDIS 暂停插操作暂停驱动程序堆栈的一部分的筛选器模块。 有关暂停的驱动程序堆栈的概述，请参阅[暂停驱动程序堆栈](pausing-a-driver-stack.md)。

在筛选器模块代表*暂停*状态时，筛选器驱动程序：

-   应不会发生任何新的接收的指示。

    有关详细信息大约发送和接收操作，请参阅[筛选器模块发送和接收操作](filter-module-send-and-receive-operations.md)。

-   如果有接收操作筛选器驱动程序发起的而且的 NDIS 尚未完成，筛选器驱动程序必须等待 NDIS 以完成此类操作。 NDIS 调用才会完成暂停操作[ *FilterReturnNetBufferLists* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-filter_return_net_buffer_lists)函数为所有此类未完成接收的指示。

-   应返回所有未完成收到指示立即发起到 NDIS 该基础驱动程序。 驱动程序调用才会完成暂停操作[ **NdisFReturnNetBufferLists** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisfreturnnetbufferlists)函数为此类未完成接收的指示。 这些未完成接收指示如果驱动程序队列从基础驱动程序收到的缓冲区可存在。

-   应返回新接收指示基础驱动程序发出的到 NDIS 立即通过调用**NdisFReturnNetBufferLists**函数。 如果有必要，驱动程序可以将复制接收指示并将它们返回之前对它们进行排队。

    **请注意**  [**NdisFReturnNetBufferLists** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisfreturnnetbufferlists)应不会调用功能的 Nbl 用 NDIS\_接收\_标志\_资源标志中的设置对应[ *FilterReceiveNetBufferLists* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-filter_receive_net_buffer_lists)调用。 此类功能的 Nbl 返回到 NDIS 以同步方式返回从*FilterReceiveNetBufferLists*例程。

     

-   应不是源自任何新的发送请求。

-   如果发送的操作筛选器驱动程序产生，NDIS 尚未完成，筛选器驱动程序必须等待 NDIS 以完成此类操作。 NDIS 调用才会完成暂停操作[ *FilterSendNetBufferListsComplete* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-filter_send_net_buffer_lists_complete)函数的所有此类未完成发送请求。

-   所有新发送到发出的请求应返回其[ *FilterSendNetBufferLists* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-filter_send_net_buffer_lists)立即通过调用函数[ **NdisFSendNetBufferListsComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisfsendnetbufferlistscomplete)函数。 筛选器驱动程序应设置**状态**中每个 NET 成员\_缓冲区\_到 NDIS 列表结构\_状态\_已暂停。

-   可以提供与状态指示[ **NdisFIndicateStatus** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisfindicatestatus)函数。

    有关状态指示的详细信息，请参阅[筛选器模块状态指示](filter-module-status-indications.md)。

-   应处理状态指示在其[ *FilterStatus* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-filter_status)函数。

-   应处理中的 OID 请求[ *FilterOidRequest* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-filter_oid_request)函数。

    有关 OID 的请求的详细信息，请参阅[筛选器模块 OID 请求](filter-module-oid-requests.md)。

-   可以启动 OID 请求。

-   应释放资源在附加操作期间分配的驱动程序。

-   应取消计时器，如果需要停止发送和接收操作。

    有关计时器的详细信息，请参阅[NDIS 6.0 计时器服务](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_netvista/)。

筛选器驱动程序已成功暂停发送和接收操作后，它必须完成暂停操作。 筛选器驱动程序可以完成暂停操作以同步方式还是以异步方式返回 NDIS\_状态\_成功或 NDIS\_状态\_分别从 PENDING [ *FilterPause*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-filter_pause)。

如果该驱动程序返回 NDIS\_状态\_挂起，它必须调用[ **NdisFPauseComplete** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisfpausecomplete)后完成暂停操作正常。

在筛选器模块代表*已暂停*状态时，筛选器驱动程序：

-   应不会发生新的接收的指示。

-   应返回新接收指示基础驱动程序发出的到 NDIS 立即通过调用[ **NdisFReturnNetBufferLists** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisfreturnnetbufferlists)函数。 如果有必要，驱动程序可以将复制接收指示并将它们返回之前对它们进行排队。

-   应不是源自新的发送请求。

-   所有新发送到发出的请求应返回其[ *FilterSendNetBufferLists* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-filter_send_net_buffer_lists)立即通过调用函数[ **NdisFSendNetBufferListsComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisfsendnetbufferlistscomplete)函数。 筛选器驱动程序应设置**状态**中每个 NET 成员\_缓冲区\_到 NDIS 列表结构\_状态\_已暂停。

-   可以提供与状态指示[ **NdisFIndicateStatus** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisfindicatestatus)函数。

-   应处理状态指示在其[ *FilterStatus* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-filter_status)函数。

-   应处理中的 OID 请求[ *FilterOidRequest* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-filter_oid_request)函数。

-   可以启动 OID 请求。

NDIS 并不会启动其他插操作，例如，附加、 分离，或重新启动请求，而筛选器驱动程序位于*暂停*状态。 可以启动 NDIS 分离或在筛选器驱动程序后，重新启动请求*已暂停*状态。 有关如何分离筛选器模块的详细信息，请参阅[分离筛选器模块](detaching-a-filter-module.md)。 有关如何重新启动筛选器模块的详细信息，请参阅[启动筛选器模块](starting-a-filter-module.md)。

 

 





