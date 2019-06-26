---
title: 为 SAN 代理驱动程序分配和释放内存
description: 为 SAN 代理驱动程序分配和释放内存
ms.assetid: c196f202-159c-4296-9888-818eaeaada73
keywords:
- 代理驱动程序 WDK San、 内存分配
- SAN 代理驱动程序 WDK，内存分配
- 内存分配 WDK San
- 释放 SAN 代理驱动程序的内存
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5b83da9ffb5ffd48c0a05f3dfa72237f5ba3eed8
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67382916"
---
# <a name="allocating-and-releasing-memory-for-a-san-proxy-driver"></a>为 SAN 代理驱动程序分配和释放内存





代理驱动程序必须设置对用户缓冲区的访问，以便 Windows 套接字开关可以传输控制消息并执行 RDMA 操作。 若要请求的缓冲区访问此类型，代理驱动程序中设置了位**标志**应执行的操作的设备对象的成员\_直接\_IO。 代理驱动程序还必须分配或释放内存，以便消息传送和 RDMA 请求时用于执行此操作。 当 Windows 套接字交换机请求 SAN 服务提供商，以注册或释放内存时，SAN 服务提供程序请求其代理驱动程序，分别分配或释放物理内存。 有关如何设置缓冲区的访问和分配和释放内存的详细信息，请参阅[内存管理](https://docs.microsoft.com/windows-hardware/drivers/kernel/managing-memory-for-drivers)并[缓冲区管理](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)。

### <a name="allocating-low-memory-for-rdma"></a>分配用于 RDMA 的内存不足

代理驱动程序必须为 RDMA 操作分配可访问的内存。 代理驱动程序可以为即使在已配置，以便可以分配任何低于 4GB 的物理内存的系统上的 RDMA 操作不分配内存不足。 （这被称为 NOLOWMEM 配置）。代理驱动程序拨打[ **MmAllocateContiguousMemorySpecifyCache** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-mmallocatecontiguousmemoryspecifycache)函数或其自身 DMA [ **AllocateCommonBuffer** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-pallocate_common_buffer)函数来检索内存不足。

若要检索一个指向其 DMA **AllocateCommonBuffer**函数，该代理驱动程序将执行以下步骤：

1.  零初始化[**设备\_说明**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_device_description)结构，然后将其 SAN NIC 的相关信息写入此结构。

2.  调用[ **IoGetDmaAdapter** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iogetdmaadapter)要检索其 SAN nic 指向 DMA 适配器结构的指针 在此调用中，该驱动程序将指针传递到填入设备\_描述结构。 **IoGetDmaAdapter**返回指向包含指向指针的 DMA 适配器结构的指针[ **DMA\_OPERATIONS** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_dma_operations)结构。 DMA\_操作包含一组系统定义 DMA 函数的指针。 这些函数之一是**AllocateCommonBuffer**，可分配的物理上连续的 DMA 缓冲区。

 

 





