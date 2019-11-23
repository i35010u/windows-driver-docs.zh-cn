---
title: 接收缓冲区中的共享内存
description: 接收缓冲区中的共享内存
ms.assetid: 3e4d0534-3cbd-40df-b7c1-4f2c15bcd757
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b5d917d8e0397f3ebddd0537ec1d30b6ed1936ef
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841927"
---
# <a name="shared-memory-in-receive-buffers"></a>接收缓冲区中的共享内存





本部分介绍 VMQ 接收缓冲区中共享内存的布局。有关使用接收指示中的缓冲区的详细信息，请参阅[VMQ 接收路径](vmq-receive-path.md)。

如果过量协议驱动程序设置 NDIS\_接收\_队列\_参数\_预测先行\_在[**NDIS\_接收\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_queue_parameters)的**Flags**成员中\_所需的标志，则该网络适配器应将接收的数据包拆分为大于或等于请求的预测值大小，并使用 DMA 将预测数据和后期预测数据传输到单独的共享内存段。\_

小型端口驱动程序在分配共享内存时指定预测先行类型（**NdisSharedMemoryUsageReceiveLookahead**）或其他共享内存类型的设置。 例如，微型端口驱动程序调用[**NdisAllocateSharedMemory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisallocatesharedmemory)函数，并将[**NDIS\_共享\_内存\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_shared_memory_parameters)结构中的**使用**成员设置为**NdisSharedMemoryUsageReceiveLookahead**。 当队列分配完成时，小型端口驱动程序应为队列分配共享内存。 有关为队列分配和释放共享内存资源的信息，请参阅[共享内存资源分配](shared-memory-resource-allocation.md)。

下图显示了将传入数据拆分为两个共享内存缓冲区时网络数据的关系。

![说明将传入数据拆分为两个共享内存缓冲区时网络数据的关系的关系图](images/vmqpacket.png)

[**NET\_缓冲区\_shared\_内存**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_shared_memory)结构指定共享内存信息。 可以有与[**NET\_缓冲区**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer)结构关联的此类共享内存缓冲区的链接列表。

使用[**net\_buffer\_shared\_MEM\_接下来\_段**](https://docs.microsoft.com/windows-hardware/drivers/network/net-buffer-shared-mem-next-segment)， [**net\_buffer\_shared\_mem\_标志**](https://docs.microsoft.com/windows-hardware/drivers/network/net-buffer-shared-mem-flags)， [**net\_buffer**](https://docs.microsoft.com/windows-hardware/drivers/network/net-buffer-shared-mem-handle)\_shared\_mem\_句柄， [**net\_buffer\_Shared**](https://docs.microsoft.com/windows-hardware/drivers/network/net-buffer-shared-mem-offset)\_mem\_偏移量， [**net\_buffer**](https://docs.microsoft.com/windows-hardware/drivers/network/net-buffer-shared-mem-length)\_共享\_mem\_\_\_NET\_BUFFER 结构中的 _33_ 内存。\_ NET\_缓冲区结构的**SharedMemoryInfo**成员包含链接列表中的第一个网络\_缓冲区\_共享\_内存结构。

**请注意**  从 NDIS 6.30 开始，不再支持将数据包数据拆分为单独的预测先行缓冲区。 从 Windows Server 2012 开始，过量协议驱动程序将不会将**ndis\_接收\_队列\_参数\_预测**\_\_\_\_[**参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_queue_parameters)结构的**FLAGS**成员中的 "需要预测先行\_拆分" 标记。

 

 

 





