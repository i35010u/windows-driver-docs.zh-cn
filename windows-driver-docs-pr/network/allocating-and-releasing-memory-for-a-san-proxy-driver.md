---
title: 为 SAN 代理驱动程序分配和释放内存
description: 为 SAN 代理驱动程序分配和释放内存
ms.assetid: c196f202-159c-4296-9888-818eaeaada73
keywords:
- 代理驱动程序 WDK San，内存分配
- SAN 代理驱动程序 WDK，内存分配
- 内存分配 WDK San
- 释放 SAN 代理驱动程序的内存
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6afe869b18a427857fc372726671e70221ddd940
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89206515"
---
# <a name="allocating-and-releasing-memory-for-a-san-proxy-driver"></a>为 SAN 代理驱动程序分配和释放内存





代理驱动程序必须设置对用户缓冲区的访问权限，以便 Windows 套接交换机可以传输控制消息和执行 RDMA 操作。 若要请求此类型的缓冲区访问，代理驱动程序会在其设备对象的 **Flags** 成员中设置一个位来执行 \_ 直接 \_ IO。 代理驱动程序还必须分配或释放用于消息传输和 RDMA 的内存，并在每次请求时使用。 当 Windows 套接交换机请求 SAN 服务提供商注册或释放内存时，SAN 服务提供程序会请求其代理驱动程序分别分配或释放物理内存。 有关设置缓冲区访问和分配和释放内存的详细信息，请参阅 [内存管理](../kernel/managing-memory-for-drivers.md) 和 [缓冲区管理](/windows-hardware/drivers/ddi/index)。

### <a name="allocating-low-memory-for-rdma"></a>为 RDMA 分配低内存

代理驱动程序必须分配可为 RDMA 操作访问的内存。 代理驱动程序可以为 RDMA 操作分配低内存，即使在配置的系统上，也不能分配低于 4 GB 的物理内存。  (这称为 NOLOWMEM 配置。 ) 代理驱动程序调用 [**MmAllocateContiguousMemorySpecifyCache**](/windows-hardware/drivers/ddi/wdm/nf-wdm-mmallocatecontiguousmemoryspecifycache) 函数或其自己的 DMA [**AllocateCommonBuffer**](/windows-hardware/drivers/ddi/wdm/nc-wdm-pallocate_common_buffer) 函数来检索内存不足的情况。

若要检索指向其 DMA **AllocateCommonBuffer** 函数的指针，代理驱动程序将执行以下步骤：

1.  0-初始化 [**设备 \_ 描述**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_device_description) 结构，然后将其 SAN NIC 的相关信息写入此结构。

2.  调用 [**IoGetDmaAdapter**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetdmaadapter) 为其 SAN NIC 检索指向 DMA 适配器结构的指针。 在此调用中，驱动程序将指针传递到已填充的设备 \_ 说明结构。 **IoGetDmaAdapter** 返回一个指针，该指针指向 dma 适配器结构，该结构包含指向 [**dma \_ 操作**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_dma_operations) 结构的指针。 DMA \_ 操作包含指向系统定义的 DMA 函数集的指针。 其中一个函数为 **AllocateCommonBuffer**，它分配一个物理上连续的 DMA 缓冲区。

 

