---
title: 在筛选器驱动程序中接收数据
description: 在筛选器驱动程序中接收数据
keywords:
- 接收数据 WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5ad14bce09b76f4c41329cefa734f5fd3e6db385
ms.sourcegitcommit: a9fb2c30adf09ee24de8e68ac1bc6326ef3616b8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2021
ms.locfileid: "102248311"
---
# <a name="receiving-data-in-a-filter-driver"></a>在筛选器驱动程序中接收数据





筛选器驱动程序可以从基础驱动程序启动接收指示或筛选接收指示。 当微型端口驱动程序调用 [**NdisMIndicateReceiveNetBufferLists**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismindicatereceivenetbufferlists) 函数时，NDIS 会将指定的 [**网络 \_ 缓冲区 \_ 列表**](/windows-hardware/drivers/ddi/nbl/ns-nbl-net_buffer_list) 结构提交给驱动程序堆栈中的最低过量筛选器模块。

### <a name="receive-indications-initiated-by-a-filter-driver"></a>筛选器驱动程序启动的接收指示

下图说明了由筛选器驱动程序启动的接收指示。

![说明筛选器驱动程序启动的接收指示的关系图](images/filterreceive.png)

筛选器驱动程序调用 [**NdisFIndicateReceiveNetBufferLists**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfindicatereceivenetbufferlists) 函数以指示收到的数据。 **NdisFIndicateReceiveNetBufferLists** 函数将指示的 [**网络 \_ 缓冲区 \_ 列表**](/windows-hardware/drivers/ddi/nbl/ns-nbl-net_buffer_list)结构的列表向上传递给过量的驱动程序。 筛选器驱动程序将从它在初始化过程中创建的池分配结构。

如果筛选器驱动程序在 [**NdisFIndicateReceiveNetBufferLists**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfindicatereceivenetbufferlists)的 *ReceiveFlags* 参数中设置 **NDIS \_ 接收 \_ 标志 \_ 资源** 标志，则表明筛选器驱动程序必须立即重新获取 [**网络 \_ 缓冲区 \_ 列表**](/windows-hardware/drivers/ddi/nbl/ns-nbl-net_buffer_list)结构的所有权。 在这种情况下，NDIS 不会调用筛选器驱动程序的 [*FilterReturnNetBufferLists*](/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_return_net_buffer_lists) 函数来返回 **网络 \_ 缓冲区 \_ 列表** 结构。 筛选器驱动程序在 **NdisFIndicateReceiveNetBufferLists** 返回后立即重新获得所有权。

如果筛选器驱动程序未在 [**NdisFIndicateReceiveNetBufferLists**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfindicatereceivenetbufferlists)的 *ReceiveFlags* 参数中设置 **ndis \_ 接收 \_ 标志 \_ 资源** 标志，NDIS 将向筛选器驱动程序的 [*FilterReturnNetBufferLists*](/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_return_net_buffer_lists)函数返回指定的 [**网络 \_ 缓冲区 \_ 列表**](/windows-hardware/drivers/ddi/nbl/ns-nbl-net_buffer_list)结构。 在这种情况下，筛选器驱动程序让给指示的结构的所有权，直到 NDIS 将其返回给 *FilterReturnNetBufferLists*。

**注意**  筛选器驱动程序应跟踪其启动的接收指示，并确保接收操作完成后，它不会调用 [**NdisFReturnNetBufferLists**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfreturnnetbufferlists) 函数。

 

### <a name="filtering-receive-indications"></a>筛选接收指示

下图说明了由基础驱动程序启动的筛选接收指示。

![说明由底层驱动程序启动的筛选接收指示的关系图](images/receivefilter.png)

NDIS 调用筛选器驱动程序的 [*FilterReceiveNetBufferLists*](/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_receive_net_buffer_lists) 函数来处理来自基础驱动程序的接收指示。 在基础驱动程序调用接收指示 (函数后，NDIS 将调用 FilterReceiveNetBufferLists，例如， [**NdisMIndicateReceiveNetBufferLists**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismindicatereceivenetbufferlists)) 指示收到的网络数据或环回数据。 

如果未设置 [*FilterReceiveNetBufferLists*](/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_receive_net_buffer_lists)的 *ReceiveFlags* 参数中的 **NDIS \_ 接收 \_ 标志 \_ 资源** 标志，则筛选器驱动程序将保留 [**网络 \_ 缓冲区 \_ 列表**](/windows-hardware/drivers/ddi/nbl/ns-nbl-net_buffer_list)结构的所有权，直到调用 [**NdisFReturnNetBufferLists**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfreturnnetbufferlists)函数。

如果设置了 *ReceiveFlags* 参数中的 **NDIS \_ 接收 \_ 标志 \_ 资源** 标志，筛选器驱动程序将无法保留 [**网络 \_ 缓冲区 \_ 列表**](/windows-hardware/drivers/ddi/nbl/ns-nbl-net_buffer_list)结构和关联的基础驱动程序分配的资源。 此标志可以指示基础驱动程序在接收资源上运行不足。 [*FilterReceiveNetBufferLists*](/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_receive_net_buffer_lists)函数应尽快返回。

**注意**  如果设置了 **NDIS \_ 接收 \_ 标志 \_ 资源** 标志，筛选器驱动程序必须在链接列表中保留一组原始的 [**网络 \_ 缓冲区 \_ 列表**](/windows-hardware/drivers/ddi/nbl/ns-nbl-net_buffer_list) 结构。 例如，设置此标志时，驱动程序可能会处理这些结构，并一次一个地指示其堆栈，但在函数返回之前，必须还原原始链接列表。

 

筛选器驱动程序可以在向过量驱动程序指示数据之前对接收到的数据执行筛选器操作。 对于提交到其 [*FilterReceiveNetBufferLists*](/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_receive_net_buffer_lists) 函数的每个缓冲区，筛选器驱动程序可以执行以下操作：

-   通过调用 [**NdisFIndicateReceiveNetBufferLists**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfindicatereceivenetbufferlists)将其传递到下一个过量驱动程序。 驱动程序可以修改缓冲区的内容。 NDIS 保证上下文空间的可用性 (参阅 [网络 \_ 缓冲区 \_ 列表 \_ 上下文结构](net-buffer-list-context-structure.md)) 。

    筛选器驱动程序可以更改 NDIS 传递到 [*FilterReceiveNetBufferLists*](/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_receive_net_buffer_lists) 的状态，或者只是将其传递到 [**NdisFIndicateReceiveNetBufferLists**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfindicatereceivenetbufferlists)。

    **注意** 即使 NDIS 在 [*FilterReceiveNetBufferLists*](/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_receive_net_buffer_lists)的 *ReceiveFlags* 参数中设置了 **ndis \_ 接收 \_ 标志 \_ 资源** 标志，筛选器驱动程序仍可以使用 [**NdisFIndicateReceiveNetBufferLists**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfindicatereceivenetbufferlists)在缓冲区上传递。 在这种情况下，筛选器驱动程序不能从 *FilterReceiveNetBufferLists* 返回，直到它重新获得缓冲区的所有权。

     

-   丢弃缓冲区。 如果 NDIS 在 [*FilterReceiveNetBufferLists*](/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_receive_net_buffer_lists)的 *ReceiveFlags* 参数中清除了 **ndis \_ 接收 \_ 标志 \_ 资源** 标志，则调用 [**NdisFReturnNetBufferLists**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfreturnnetbufferlists)函数以丢弃缓冲区。 如果 NDIS 在 *FilterReceiveNetBufferLists* 的 *ReceiveFlags* 参数中设置 **ndis \_ 接收 \_ 标志 \_ 资源** 标志，则不执行任何操作并从 *FilterReceiveNetBufferLists* 返回以放弃缓冲区。

-   在本地数据结构中对缓冲区排队，以便以后进行处理。 如果 NDIS 在 [*FilterReceiveNetBufferLists*](/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_receive_net_buffer_lists)的 *ReceiveFlags* 参数中设置 **ndis \_ 接收 \_ 标志 \_ 资源** 标志，则筛选器驱动程序必须在从 *FilterReceiveNetBufferLists* 返回之前创建副本。

-   复制缓冲区并使用副本产生接收指示。 接收指示类似于筛选器驱动程序启动的接收指示。 在这种情况下，驱动程序必须将原始缓冲区返回到底层驱动程序。

[**NdisFIndicateReceiveNetBufferLists**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfindicatereceivenetbufferlists)函数将显示的 [**网络 \_ 缓冲区 \_ 列表**](/windows-hardware/drivers/ddi/nbl/ns-nbl-net_buffer_list)结构的所指示的列表传递给过量驱动程序。 接收操作的执行方式类似于筛选器驱动程序启动的接收操作。

如果过量驱动程序保留了缓冲区的所有权，NDIS 将为筛选器模块调用 [*FilterReturnNetBufferLists*](/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_return_net_buffer_lists) 函数。 在 *FilterReturnNetBufferLists* 函数中，筛选器驱动程序将撤消它在接收指示路径上对缓冲区执行的操作。

当最低层筛选器模块指示它是使用缓冲区完成时，NDIS 会将缓冲区返回给微型端口驱动程序。 如果 NDIS 在 [*FilterReceiveNetBufferLists*](/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_receive_net_buffer_lists)的 *ReceiveFlags* 参数中清除了 **ndis \_ 接收 \_ 标志 \_ 资源** 标志，筛选器驱动程序将调用 [**NdisFReturnNetBufferLists**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfreturnnetbufferlists)以返回缓冲区。 如果 NDIS 在 *FilterReceiveNetBufferLists* 的 *ReceiveFlags* 参数中设置 **ndis \_ 接收 \_ 标志 \_ 资源** 标志，则从 *FilterReceiveNetBufferLists* 返回将返回缓冲区。

 

