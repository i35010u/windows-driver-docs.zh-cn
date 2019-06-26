---
title: VMQ 接收路径
description: VMQ 接收路径
ms.assetid: e59907fc-94dc-45c4-943d-1628c63961dc
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ca63b811e512e002e6146920d0c608d6082f25e2
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384354"
---
# <a name="vmq-receive-path"></a>VMQ 接收路径





网络适配器仅在通过的筛选器，该队列上设置的所有筛选器字段测试指示队列上接收的数据包。 有关筛选器测试的详细信息，请参阅[VMQ 筛选器操作](vmq-filter-operations.md)。

如果基础协议驱动程序设置**NDIS\_接收\_队列\_参数\_每\_队列\_接收\_指示**中的标志**标志**的成员[ **NDIS\_接收\_队列\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_receive_queue_parameters)结构，微型端口驱动程序必须将混合[ **NET\_缓冲区\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list)结构适用于其他接收队列**NET\_缓冲区\_列表**结构中调用一次此队列[ **NdisMIndicateReceiveNetBufferLists** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismindicatereceivenetbufferlists)函数。 此外，驱动程序必须设置**NDIS\_接收\_标志\_单个\_队列**标志中*ReceiveFlags*参数**NdisMIndicateReceiveNetBufferLists**函数。

如果**NDIS\_接收\_队列\_参数\_每\_队列\_接收\_指示**不可设置，可以将链接微型端口驱动程序[ **NET\_缓冲区\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list)结构不同的虚拟机队列中的帧，并指示它们对单个调用中[ **NdisMIndicateReceiveNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismindicatereceivenetbufferlists)。 在这种情况下，所指示链接的列表**NET\_缓冲区\_列表**结构不需要队列编号进行排序。 **NET\_缓冲区\_列表**结构的不同队列不需要组合在一起。

当协议驱动程序集**NDIS\_返回\_标志\_单个\_队列**和它返回接收缓冲区中的所有[ **NET\_缓冲区\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list)中结构*NetBufferLists*参数[ **NdisReturnNetBufferLists** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisreturnnetbufferlists)函数必须属于同一个虚拟机队列。 但是，协议驱动程序不需要返回所有**NET\_缓冲区\_列表**对单个调用中所指示的结构[ **ProtocolReceiveNetBufferLists** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-protocol_receive_net_buffer_lists)函数中调用一次**NdisReturnNetBufferLists**。 此外，返回的列表可以包括**NET\_缓冲区\_列表**结构从多个接收的指示，如果它们属于同一个虚拟机队列。

协议驱动程序集**NDIS\_返回\_标志\_单个\_队列**位*ReturnFlags*参数[ **NdisReturnNetBufferLists** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisreturnnetbufferlists)以指示所返回的所有[ **NET\_缓冲区\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list)结构属于同一个虚拟机队列。

VMQ 接收指示必须包括以下带外 (OOB) 中的信息**NetBufferListInfo**的成员[ **NET\_缓冲区\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list)结构。

-   指定在队列标识符**NetBufferListFilteringInfo**信息。

-   在中设置筛选器标识符**NetBufferListFilteringInfo**为零的信息。

**NetBufferListFilteringInfo**中指定的信息[ **NDIS\_NET\_缓冲区\_列表\_筛选\_信息** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_net_buffer_list_filtering_info)结构。 若要访问 NDIS\_NET\_缓冲区\_列表\_筛选\_中的信息结构[ **NET\_缓冲区\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list) OOB 数据的 NDIS 驱动程序调用[ **NET\_缓冲区\_列表\_信息**](https://docs.microsoft.com/windows-hardware/drivers/network/net-buffer-list-info)宏，并指定**NetBufferListFilteringInfo**信息类型。

若要直接访问筛选器标识符和队列标识符，请使用[ **NET\_缓冲区\_列表\_接收\_筛选器\_ID** ](https://docs.microsoft.com/windows-hardware/drivers/network/net-buffer-list-receive-filter-id)并[ **NET\_缓冲区\_列表\_接收\_队列\_ID** ](https://docs.microsoft.com/windows-hardware/drivers/network/net-buffer-list-receive-queue-id)宏。

VMQ 接收指示必须定义上的共享的内存信息**SharedMemoryInfo**的成员[ **NET\_缓冲区**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer)结构。

**请注意**  时 VMQ 删除 （例如，在虚拟机实时迁移），则可以为微型端口驱动程序以接收包含一个无效的 NBL **QueueId**值。 如果发生这种情况，应忽略无效的队列 ID 微型端口并将其改为使用 0 （默认队列）。 **QueueId**中找到**NetBufferListFilteringInfo** NBL 部分的 OOB 数据，并通过使用检索[ **NET\_缓冲区\_列表\_接收\_队列\_ID** ](https://docs.microsoft.com/windows-hardware/drivers/network/net-buffer-list-receive-queue-id)宏。

 

若要指示[ **NET\_缓冲区\_共享\_内存**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_shared_memory)指针位于**SharedMemoryInfo**有效，微型端口驱动程序必须设置 NDIS\_接收\_标志\_共享\_内存\_信息\_有效标志中*ReceiveFlags*参数[ **NdisMIndicateReceiveNetBufferLists** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismindicatereceivenetbufferlists)函数。 有关布局的共享内存的详细信息中 VMQ 的缓冲区接收缓冲区，请参阅[接收缓冲区中的共享内存](shared-memory-in-receive-buffers.md)。

接收指示必须包括中的以下信息[ **NET\_缓冲区\_共享\_内存**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_shared_memory)结构。

<a href="" id="nextsharedmemorysegment"></a>**NextSharedMemorySegment**  
指向下一步[ **NET\_缓冲区\_共享\_内存**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_shared_memory)结构**NULL**-终止此类链接的列表结构。

<a href="" id="sharedmemoryhandle"></a>**SharedMemoryHandle**  
NDIS 共享内存处理[ **NdisAllocateSharedMemory** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisallocatesharedmemory)返回。

<a href="" id="sharedmemoryoffset"></a>**SharedMemoryOffset**  
偏移量，以字节为单位，到起始位置的数据从共享的内存缓冲区的开头。

<a href="" id="sharedmemorylength"></a>**SharedMemoryLength**  
共享的内存段长度 （字节）。

如果基础协议驱动程序设置**NDIS\_接收\_队列\_参数\_预测先行\_拆分\_必需**中标志**标志**的成员[ **NDIS\_接收\_队列\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_receive_queue_parameters)结构，每个[ **NET\_缓冲区**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer)包括：

-   两个 MDLs 和相应**SharedMemoryInfo**结构。

-   具有回填空间的 post 预测先行缓冲区。

如有必要，协议驱动程序将预期缓冲区的内容复制到回填区域。 但是，即使该数据包是完全在预期缓冲区中必须存在回填空间。

如果基础驱动程序不会设置**NDIS\_接收\_队列\_参数\_预测先行\_拆分\_必需**标志，每个[ **NET\_缓冲区**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer)结构包含单个 MDL 和单个**SharedMemoryInfo**结构。

MDL 中的字节计数和字节偏移量和**DataLength**并**DataOffset**中的成员[ **NET\_缓冲区\_数据**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_data)结构设置相同的方式，因为设置的驱动程序，请不要使用 VMQ。 **SharedMemoryLength**并**SharedMemoryOffset**中的成员**SharedMemoryInfo**结构可以设置一次在初始化过程。 微型端口驱动程序不需要更新**SharedMemoryLength**并**SharedMemoryOffset**因过量的驱动程序和 NDIS 可以使用收到的每个数据包的成员[ **NET\_缓冲区**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer) **DataLength**成员和 MDL 字节计数以确定数据包开始和大小。

**请注意**  从 NDIS 6.30 和 Windows Server 2012 开始，将数据包数据拆分为单独的预测先行缓冲区不再受支持。 基础协议驱动程序不会设置**NDIS\_接收\_队列\_参数\_预测先行\_拆分\_必需**标志。

 

 

 





