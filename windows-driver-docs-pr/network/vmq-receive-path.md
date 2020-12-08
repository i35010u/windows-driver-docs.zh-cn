---
title: VMQ 接收路径
description: VMQ 接收路径
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6b52e9d244755ac6c2edb3417e317ea0eb85e27c
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96786709"
---
# <a name="vmq-receive-path"></a>VMQ 接收路径





仅当网络适配器传递了在队列中设置的筛选器的所有筛选器字段测试时，它才会指示已接收的数据包。 有关筛选器测试的详细信息，请参阅 [VMQ 筛选器操作](vmq-filter-operations.md)。

如果过量协议驱动程序在 [**ndis \_ 接收 \_ 队列 \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_queue_parameters)结构的 **Flags** 成员中对 **\_ \_ \_ \_ 每个 \_ 队列 \_ 接收 \_ 指示标志的 ndis 接收队列参数** 进行了设置，则微型端口驱动程序不得为具有此队列的 **网络 \_ 缓冲区 \_ 列表** 结构的其他接收队列混合 [**网络 \_ 缓冲区 \_ 列表**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)结构，只需调用 [**NdisMIndicateReceiveNetBufferLists**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismindicatereceivenetbufferlists)函数。 此外，驱动程序必须在 **NdisMIndicateReceiveNetBufferLists** 函数的 *ReceiveFlags* 参数中设置 **NDIS \_ 接收 \_ 标志 \_ 单一 \_ 队列** 标志。

如果未设置 **\_ \_ \_ \_ 每个 \_ 队列接收 \_ \_ 的 NDIS 接收队列参数接收指示** ，微型端口驱动程序可以将来自不同 VM 队列的帧的 [**网络 \_ 缓冲区 \_ 列表**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list) 结构进行链接，并在对 [**NdisMIndicateReceiveNetBufferLists**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismindicatereceivenetbufferlists)的单个调用中指示它们。 在这种情况下，不需要按队列号对所指示的 **网络 \_ 缓冲区 \_ 列表** 结构的链接列表进行排序。 **NET \_不同队列的缓冲区 \_ 列表** 结构不需要组合在一起。

当协议驱动程序将 **NDIS \_ 返回 \_ 标志设置为 \_ 单一 \_ 队列** 并返回接收缓冲区时， [**NdisReturnNetBufferLists**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisreturnnetbufferlists)函数的 *NetBufferLists* 参数中的所有 [**网络 \_ 缓冲区 \_ 列表**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)结构都必须属于同一个 VM 队列。 但是，不要求协议驱动程序返回通过对 **NdisReturnNetBufferLists** 的单个调用 [**中的单个**](/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_receive_net_buffer_lists)调用中指定的所有 **网络 \_ 缓冲区 \_ 列表** 结构。 此外，如果返回的列表属于同一 VM 队列，则可以包含来自多个接收指示的 **网络 \_ 缓冲区 \_ 列表** 结构。

协议驱动程序在 [**NdisReturnNetBufferLists**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisreturnnetbufferlists)的 *ReturnFlags* 参数上设置 **NDIS \_ 返回 \_ 标志 \_ 单一 \_ 队列** 位，以指示所有返回的 [**网络 \_ 缓冲区 \_ 列表**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)结构都属于同一 VM 队列。

VMQ 接收指示必须在 [**网络 \_ 缓冲区 \_ 列表**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)结构的 **NetBufferListInfo** 成员中包括以下带外 (OOB) 信息。

-   在 **NetBufferListFilteringInfo** 信息中指定队列标识符。

-   将 **NetBufferListFilteringInfo** 信息中的筛选器标识符设置为零。

**NetBufferListFilteringInfo** 信息是在 [**NDIS \_ 网络 \_ 缓冲区 \_ 列表 \_ 筛选 \_ 信息**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_net_buffer_list_filtering_info)结构中指定的。 若要访问 \_ \_ 网络缓冲区中的 ndis 网络缓冲区 \_ 列表 \_ 筛选 \_ 信息结构，请使用 ndis 驱动程序调用 [**net \_ buffer \_ list \_ INFO**](/windows-hardware/drivers/ddi/ndis/nf-ndis-net_buffer_list_info)宏并指定 **NetBufferListFilteringInfo** 信息类型。 [**\_ \_**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)

若要直接访问筛选器标识符和队列标识符，请使用 [**网络 \_ 缓冲区 \_ 列表 \_ 接收 \_ 筛选器 \_ id**](/windows-hardware/drivers/ddi/ndis/nf-ndis-net_buffer_list_receive_filter_id) 和 [**网络 \_ 缓冲区 \_ 列表 \_ 接收 \_ 队列 \_ ID**](/windows-hardware/drivers/ddi/ndis/nf-ndis-net_buffer_list_receive_queue_id) 宏。

VMQ 接收指示必须定义 [**网络 \_ 缓冲区**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer)结构的 **SharedMemoryInfo** 成员的共享内存信息。

**注意**  删除 VMQ 后 (例如，在 VM 实时迁移期间) ，微型端口驱动程序可以接收包含无效 **QueueId** 值的 NBL。 如果发生这种情况，微型端口应忽略无效的队列 ID 并使用 0 (默认队列) 。 **QueueId** 在 NBL 的 OOB 数据的 **NetBufferListFilteringInfo** 部分中找到，并使用 [**NET \_ BUFFER \_ LIST \_ RECEIVE \_ QUEUE \_ ID**](/windows-hardware/drivers/ddi/ndis/nf-ndis-net_buffer_list_receive_queue_id)宏检索。

 

若要指示 **SharedMemoryInfo** 的 [**网络 \_ 缓冲区 \_ 共享 \_ 内存**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_shared_memory)指针有效，微型端口驱动程序必须 \_ \_ \_ \_ \_ \_ 在 [**NdisMIndicateReceiveNetBufferLists**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismindicatereceivenetbufferlists)函数的 *ReceiveFlags* 参数中设置 "NDIS 接收标志共享内存信息" 有效标志。 有关 VMQ 接收缓冲区中共享内存缓冲区布局的详细信息，请参阅 [接收缓冲区中的共享内存](shared-memory-in-receive-buffers.md)。

接收指示必须在 [**网络 \_ 缓冲区 \_ 共享 \_ 内存**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_shared_memory) 结构中包含以下信息。

<a href="" id="nextsharedmemorysegment"></a>**NextSharedMemorySegment**  
一个指针，指向此类结构的以 **NULL** 结尾的链接列表中的下一个 [**网络 \_ 缓冲区 \_ 共享 \_ 内存**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_shared_memory)结构。

<a href="" id="sharedmemoryhandle"></a>**SharedMemoryHandle**  
[**NdisAllocateSharedMemory**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisallocatesharedmemory)返回的 NDIS 共享内存句柄。

<a href="" id="sharedmemoryoffset"></a>**SharedMemoryOffset**  
从共享内存缓冲区的开始，到数据开始处的偏移量（以字节为单位）。

<a href="" id="sharedmemorylength"></a>**SharedMemoryLength**  
共享内存段的长度（以字节为单位）。

如果过量协议驱动程序在 [**ndis \_ 接收 \_ 队列 \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_queue_parameters)结构的 **Flags** 成员中设置了 " **ndis \_ 接收 \_ 队列 \_ 参数 \_ 预测 \_ \_ 要求**" 标志，则每个 [**网络 \_ 缓冲区**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer)包括：

-   两个 MDLs 和对应的 **SharedMemoryInfo** 结构。

-   回填空间的后先行预测缓冲区。

如有必要，协议驱动程序会将预测先行缓冲区的内容复制到回填区域。 但是，即使数据包完全在预测先行缓冲区中，回填空间也必须存在。

如果过量驱动程序未设置 **NDIS \_ 接收 \_ 队列参数 " \_ \_ 预测 \_ 请求拆分 \_ 所需** " 标志，则每个 [**网络 \_ 缓冲区**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer) 结构都包括单个 MDL 和单个 **SharedMemoryInfo** 结构。

MDL 中的字节数和字节偏移量以及 [**NET \_ BUFFER \_ 数据**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_data)结构中的 **DataLength** 和 **数据偏移量** 成员的设置方式与为不使用 VMQ 的驱动程序设置的相同。 在初始化过程中，可以在 **SharedMemoryInfo** 结构中设置 **SharedMemoryLength** 和 **SharedMemoryOffset** 成员。 无需使用微型端口驱动程序来更新收到的每个数据包的 **SharedMemoryLength** 和 **SharedMemoryOffset** 成员，因为过量驱动程序和 NDIS 可以使用 [**NET \_ BUFFER**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer) **DataLength** 成员和 MDL 字节计数来确定数据包的开始和大小。

**注意**  从 NDIS 6.30 和 Windows Server 2012 开始，不再支持将数据包数据拆分为单独的预测先行缓冲区。 过量协议驱动程序将不设置 **NDIS \_ 接收 \_ 队列参数 " \_ \_ 预测 \_ \_ 要求拆分** " 标记。

 

 

