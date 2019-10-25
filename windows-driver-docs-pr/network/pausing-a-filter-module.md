---
title: 暂停筛选器模块
description: 暂停筛选器模块
ms.assetid: da75b92d-b662-416a-b350-e5384b870b7f
keywords:
- 筛选器模块 WDK 网络，暂停
- 暂停筛选器模块
- 筛选器驱动程序 WDK 网络，暂停筛选器模块
- NDIS 筛选器驱动程序 WDK，暂停筛选器模块
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 39eb86805043c4020ee254ed9df8fb8fbc746782
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843698"
---
# <a name="pausing-a-filter-module"></a>暂停筛选器模块





为了暂停正在运行的筛选器模块，NDIS 调用筛选器驱动程序的[*FilterPause*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_pause)函数。 在*FilterPause*函数中，筛选器模块将进入执行开始时的*暂停*状态。

NDIS 暂停筛选器模块，作为即插即用操作的一部分，用于暂停驱动程序堆栈。 有关暂停驱动程序堆栈的概述，请参阅[暂停驱动程序堆栈](pausing-a-driver-stack.md)。

代表处于*暂停*状态的筛选器模块，筛选器驱动程序：

-   不应产生任何新的接收指示。

    有关发送和接收操作的详细信息，请参阅[筛选模块发送和接收操作](filter-module-send-and-receive-operations.md)。

-   如果存在筛选器驱动程序的接收操作，并且 NDIS 尚未完成，则筛选器驱动程序必须等待 NDIS 完成此类操作。 暂停操作不会完成，直到 NDIS 为所有此类未完成的接收指示调用[*FilterReturnNetBufferLists*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_return_net_buffer_lists)函数。

-   应返回基础驱动程序立即产生的任何未完成的接收指示。 暂停操作不会完成，直到驱动程序为此类未完成的接收指示调用[**NdisFReturnNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfreturnnetbufferlists)函数。 如果驱动程序将从底层驱动程序接收的缓冲区排队，则这些未完成的接收指示可能存在。

-   应通过调用**NdisFReturnNetBufferLists**函数，返回基础驱动程序立即产生的新接收指示。 如有必要，驱动程序可以复制接收指示，并在返回它们之前对它们进行排队。

    **注意**不应为使用 NDIS\_接收\_标志\_资源标志在相应的[*FilterReceiveNetBufferLists*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_receive_net_buffer_lists)调用中设置的 nbl 调用  [**NdisFReturnNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfreturnnetbufferlists) 。 此类 Nbl 通过从*FilterReceiveNetBufferLists*例程返回来同步返回到 NDIS。

     

-   不应产生任何新的发送请求。

-   如果存在筛选器驱动程序生成的发送操作，并且 NDIS 尚未完成，则筛选器驱动程序必须等待 NDIS 完成此类操作。 在 NDIS 为所有此类未完成的发送请求调用[*FilterSendNetBufferListsComplete*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_send_net_buffer_lists_complete)函数之前，暂停操作不会完成。

-   应通过调用[**NdisFSendNetBufferListsComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfsendnetbufferlistscomplete)函数立即返回对其[*FilterSendNetBufferLists*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_send_net_buffer_lists)函数发出的所有新发送请求。 筛选器驱动程序应将每个 NET\_缓冲区\_列表结构中的**状态**成员设置为\_暂停的 NDIS\_状态。

-   可以通过[**NdisFIndicateStatus**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfindicatestatus)函数提供状态指示。

    有关状态指示的详细信息，请参阅[筛选模块状态指示](filter-module-status-indications.md)。

-   应在其[*FilterStatus*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_status)函数中处理状态指示。

-   应在[*FilterOidRequest*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_oid_request)函数中处理 OID 请求。

    有关 OID 请求的详细信息，请参阅[筛选器模块 OID 请求](filter-module-oid-requests.md)。

-   可以启动 OID 请求。

-   不应释放在附加操作期间分配的驱动程序资源。

-   如果需要停止发送和接收操作，应取消计时器。

    有关计时器的详细信息，请参阅[NDIS 6.0 Timer 服务](https://docs.microsoft.com/windows-hardware/drivers/ddi/_netvista/)。

筛选器驱动程序成功暂停发送和接收操作后，必须完成暂停操作。 筛选器驱动程序可以通过返回 NDIS\_状态\_SUCCESS 或 NDIS\_状态\_分别从[*FilterPause*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_pause)中挂起，来同步或异步完成暂停操作。

如果驱动程序返回 NDIS\_状态\_"挂起"，则它必须在完成暂停操作后调用[**NdisFPauseComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfpausecomplete)函数。

代表处于*暂停*状态的筛选器模块，筛选器驱动程序：

-   不应产生新的接收指示。

-   应通过调用[**NdisFReturnNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfreturnnetbufferlists)函数，返回基础驱动程序立即产生的新接收指示。 如有必要，驱动程序可以复制接收指示，并在返回它们之前对它们进行排队。

-   不应产生新的发送请求。

-   应通过调用[**NdisFSendNetBufferListsComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfsendnetbufferlistscomplete)函数立即返回对其[*FilterSendNetBufferLists*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_send_net_buffer_lists)函数发出的所有新发送请求。 筛选器驱动程序应将每个 NET\_缓冲区\_列表结构中的**状态**成员设置为\_暂停的 NDIS\_状态。

-   可以通过[**NdisFIndicateStatus**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfindicatestatus)函数提供状态指示。

-   应在其[*FilterStatus*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_status)函数中处理状态指示。

-   应在[*FilterOidRequest*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_oid_request)函数中处理 OID 请求。

-   可以启动 OID 请求。

当筛选器驱动程序处于*暂停*状态时，NDIS 不会启动其他即插即用操作，如、附加、分离或重新启动请求。 在筛选器驱动程序处于*暂停*状态之后，NDIS 可以启动分离或重新启动请求。 有关如何分离筛选器模块的详细信息，请参阅[分离筛选器模块](detaching-a-filter-module.md)。 有关如何重新启动筛选器模块的详细信息，请参阅[启动筛选器模块](starting-a-filter-module.md)。

 

 





