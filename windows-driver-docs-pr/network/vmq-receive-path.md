---
title: VMQ 接收路径
description: VMQ 接收路径
ms.assetid: e59907fc-94dc-45c4-943d-1628c63961dc
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 449ee68618e1e53d2fd0195f66bd7026db57dbf6
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842943"
---
# <a name="vmq-receive-path"></a>VMQ 接收路径





仅当网络适配器传递了在队列中设置的筛选器的所有筛选器字段测试时，它才会指示已接收的数据包。 有关筛选器测试的详细信息，请参阅[VMQ 筛选器操作](vmq-filter-operations.md)。

如果过量协议驱动程序设置**ndis\_接收\_队列\_参数\_每个\_队列\_** 接收\_的**Flags**成员的\_\_\_[**参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_queue_parameters)结构，则微型端口驱动程序不得混合使用此队列的**net\_缓冲区**\_[**列表结构，** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)这是在单个调用[**NdisMIndicateReceiveNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismindicatereceivenetbufferlists)函数。\_\_ 另外，驱动程序必须在**NdisMIndicateReceiveNetBufferLists**函数的*ReceiveFlags*参数中将**NDIS\_接收\_标志\_单一\_队列**标志。

如果**NDIS\_接收\_队列\_参数\_每个\_队列\_未设置接收\_指示**，微型端口驱动程序可以将帧的[**网络\_缓冲区\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)不同的 VM 队列，并在对[**NdisMIndicateReceiveNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismindicatereceivenetbufferlists)的单个调用中指示它们。 在这种情况下，不需要按队列号对所指示的**NET\_缓冲区\_列表**结构的链接列表进行排序。 不同队列的**NET\_缓冲区\_列表**结构不需要组合在一起。

当协议驱动程序设置**NDIS\_将\_标志\_为单个\_队列**并返回接收缓冲区时， [**NdisReturnNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisreturnnetbufferlists)函数的*NetBufferLists*参数中的所有[**NET\_缓冲区\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)结构都必须属于同一个 VM 队列。 但是，不要求协议驱动程序返回在对**NdisReturnNetBufferLists**的单个调用中[**ProtocolReceiveNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_receive_net_buffer_lists)函数的单个调用中指定的所有**NET\_缓冲区\_列表**结构。 此外，返回的列表可以包含来自多个接收指示的**NET\_缓冲区\_列表**结构，前提是它们属于同一 VM 队列。

协议驱动程序设置 NDIS\_在[**NdisReturnNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisreturnnetbufferlists)的*RETURNFLAGS*参数上**返回\_单一\_队列位的\_标志**，以指示所有返回的[**NET\_缓冲区\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)结构属于同一 VM 队列。

VMQ 接收指示必须在[**网络\_缓冲区**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)的**NetBufferListInfo**成员中包括以下带外（OOB）信息\_列表结构。

-   在**NetBufferListFilteringInfo**信息中指定队列标识符。

-   将**NetBufferListFilteringInfo**信息中的筛选器标识符设置为零。

**NetBufferListFilteringInfo**信息在[**NDIS\_NET\_缓冲器\_列表中指定\_筛选\_INFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_net_buffer_list_filtering_info)结构。 若要访问 NDIS\_NET\_BUFFER\_列表\_在[**NET\_buffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)中筛选\_INFO 结构\_列出 OOB 数据，NDIS 驱动程序调用[**net\_缓冲区\_列表\_INFO**](https://docs.microsoft.com/windows-hardware/drivers/network/net-buffer-list-info)宏并指定**NetBufferListFilteringInfo**信息类型。

若要直接访问筛选器标识符和队列标识符，请使用[**NET\_buffer\_列表\_接收\_筛选器\_id**](https://docs.microsoft.com/windows-hardware/drivers/network/net-buffer-list-receive-filter-id)和[**NET\_buffer\_\_\_\_id**](https://docs.microsoft.com/windows-hardware/drivers/network/net-buffer-list-receive-queue-id)宏。

VMQ 接收指示必须定义[**NET\_缓冲区**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer)结构的**SharedMemoryInfo**成员的共享内存信息。

**请注意**  在删除 VMQ 时（例如，在 VM 实时迁移期间），微型端口驱动程序可以接收包含无效**QUEUEID**值的 NBL。 如果发生这种情况，微型端口应忽略无效的队列 ID 并改用0（默认队列）。 **QueueId**是在 NBL 的 OOB 数据的**NetBufferListFilteringInfo**部分中找到的，使用[**NET\_BUFFER\_列表\_接收\_队列\_ID**](https://docs.microsoft.com/windows-hardware/drivers/network/net-buffer-list-receive-queue-id)宏来检索。

 

若要指示在**SharedMemoryInfo**上[**共享\_内存指针\_的 NET\_缓冲区**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_shared_memory)有效，微型端口驱动程序必须将 NDIS\_接收\_\_\_\_@no_[**NdisMIndicateReceiveNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismindicatereceivenetbufferlists)函数的*ReceiveFlags*参数中的 _t_11_ 有效标志。\_ 有关 VMQ 接收缓冲区中共享内存缓冲区布局的详细信息，请参阅[接收缓冲区中的共享内存](shared-memory-in-receive-buffers.md)。

接收指示必须在网络\_缓冲区中包含以下信息[ **\_SHARED\_内存**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_shared_memory)结构。

<a href="" id="nextsharedmemorysegment"></a>**NextSharedMemorySegment**  
指向下一个网络\_缓冲区的指针\_此类结构的以**NULL**结尾的链接列表中[**共享\_内存**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_shared_memory)结构。

<a href="" id="sharedmemoryhandle"></a>**SharedMemoryHandle**  
[**NdisAllocateSharedMemory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisallocatesharedmemory)返回的 NDIS 共享内存句柄。

<a href="" id="sharedmemoryoffset"></a>**SharedMemoryOffset**  
从共享内存缓冲区的开始，到数据开始处的偏移量（以字节为单位）。

<a href="" id="sharedmemorylength"></a>**SharedMemoryLength**  
共享内存段的长度（以字节为单位）。

如果过量协议驱动程序设置**ndis\_接收\_队列\_参数\_预测先行**\_在 NDIS\_的**FLAGS**成员中拆分\_必需标志\_[**接收\_QUEUE\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_queue_parameters)结构，每个[**NET 缓冲区**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer)包括：

-   两个 MDLs 和对应的**SharedMemoryInfo**结构。

-   回填空间的后先行预测缓冲区。

如有必要，协议驱动程序会将预测先行缓冲区的内容复制到回填区域。 但是，即使数据包完全在预测先行缓冲区中，回填空间也必须存在。

如果过量驱动程序未将**NDIS\_接收\_队列\_参数\_预测先行\_SPLIT\_必需**标志，则每个[**NET\_缓冲**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer)结构都包括单个 MDL 和**一个SharedMemoryInfo**结构。

MDL 中的字节数和字节偏移量以及[**NET\_\_缓冲区**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_data)中的**DataLength**和**数据偏移量**成员的设置方式与为不使用 VMQ 的驱动程序设置的相同。 在初始化过程中，可以在**SharedMemoryInfo**结构中设置**SharedMemoryLength**和**SharedMemoryOffset**成员。 无需使用微型端口驱动程序来更新收到的每个数据包的**SharedMemoryLength**和**SharedMemoryOffset**成员，因为过量驱动程序和 NDIS 可以使用[**NET\_BUFFER**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer) **DataLength**成员和 MDL 字节计数来确定数据包的开始和大小。

**请注意**，  从 NDIS 6.30 和 Windows Server 2012 开始，不再支持将数据包数据拆分为单独的预测先行缓冲区。 过量协议驱动程序将不会将**NDIS\_接收\_队列\_参数\_预测先行\_SPLIT\_必需**标志。

 

 

 





