---
title: 接收缓冲区中的共享内存
description: 接收缓冲区中的共享内存
ms.assetid: 3e4d0534-3cbd-40df-b7c1-4f2c15bcd757
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ff6d3aa6ce4f215817a15fe3d6fa7f8ee287999b
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89207791"
---
# <a name="shared-memory-in-receive-buffers"></a>接收缓冲区中的共享内存





本部分介绍 VMQ 接收缓冲区中共享内存的布局。有关使用接收指示中的缓冲区的详细信息，请参阅 [VMQ 接收路径](vmq-receive-path.md)。

如果过量协议驱动程序在 \_ \_ \_ \_ \_ \_ [**ndis \_ 接收 \_ 队列 \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_queue_parameters)结构的**Flags**成员中设置了 "ndis 接收队列参数预测要求" 标记，网络适配器应将接收的数据包拆分为大于或等于请求的预测大小，并使用 DMA 将预测预测数据和后预测后数据传输到单独的共享内存段。

小型端口驱动程序在分配共享内存时，指定 (**NdisSharedMemoryUsageReceiveLookahead**) 或其他共享内存类型的预测先行类型的设置。 例如，微型端口驱动程序调用[**NdisAllocateSharedMemory**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisallocatesharedmemory)函数，并将[**NDIS \_ SHARED \_ MEMORY \_ 参数**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_shared_memory_parameters)结构中的**使用**成员设置为**NdisSharedMemoryUsageReceiveLookahead**。 当队列分配完成时，小型端口驱动程序应为队列分配共享内存。 有关为队列分配和释放共享内存资源的信息，请参阅 [共享内存资源分配](shared-memory-resource-allocation.md)。

下图显示了将传入数据拆分为两个共享内存缓冲区时网络数据的关系。

![说明将传入数据拆分为两个共享内存缓冲区时网络数据的关系的关系图](images/vmqpacket.png)

[**NET \_ BUFFER \_ SHARED \_ memory**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_shared_memory)结构指定共享内存信息。 可以有一个链接列表，其中包含与 [**网络 \_ 缓冲区**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer) 结构关联的共享内存缓冲区。

使用[**网络 \_ 缓冲区 \_ 共享 \_ 内存 \_ 下一 \_ 段**](/windows-hardware/drivers/ddi/ndis/nf-ndis-net_buffer_shared_mem_next_segment)、[**网络 \_ 缓冲区 \_ 共享 \_ 内存 \_ 标志**](/windows-hardware/drivers/ddi/ndis/nf-ndis-net_buffer_shared_mem_flags)、[**网络 \_ 缓冲区共享内存的 \_ \_ \_ 句柄**](/windows-hardware/drivers/ddi/ndis/nf-ndis-net_buffer_shared_mem_handle)、网络缓冲区共享内存的[**长度宏和网络 \_ 缓冲区 \_ 共享内存 \_ \_ 长度**](/windows-hardware/drivers/ddi/ndis/nf-ndis-net_buffer_shared_mem_length)宏来访问[** \_ \_ \_ \_ **](/windows-hardware/drivers/ddi/ndis/nf-ndis-net_buffer_shared_mem_offset) \_ \_ 网络缓冲区中的网络缓冲共享 \_ 内存 \_ 。 NET buffer 结构的 **SharedMemoryInfo** 成员 \_ 包含链接列表中的第一个网络 \_ 缓冲区 \_ 共享 \_ 内存结构。

**注意**   从 NDIS 6.30 开始，不再支持将数据包数据拆分为单独的预测先行缓冲区。 从 Windows Server 2012 开始，过量协议驱动程序将不会在[**ndis \_ 接收 \_ 队列 \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_queue_parameters)结构的**Flags**成员中设置 " **ndis \_ 接收 \_ 队列 \_ 参数 \_ 预测 \_ \_ 要求**" 标志。

 

 

