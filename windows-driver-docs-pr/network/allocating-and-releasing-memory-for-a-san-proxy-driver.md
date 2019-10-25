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
ms.openlocfilehash: 377cf022ed73ffbae8a4809cbe44457d6dad0d40
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838232"
---
# <a name="allocating-and-releasing-memory-for-a-san-proxy-driver"></a>为 SAN 代理驱动程序分配和释放内存





代理驱动程序必须设置对用户缓冲区的访问权限，以便 Windows 套接交换机可以传输控制消息和执行 RDMA 操作。 若要请求此类型的缓冲区访问，代理驱动程序会在其设备对象的**Flags**成员中设置一个位，以\_直接\_IO。 代理驱动程序还必须分配或释放用于消息传输和 RDMA 的内存，并在每次请求时使用。 当 Windows 套接交换机请求 SAN 服务提供商注册或释放内存时，SAN 服务提供程序会请求其代理驱动程序分别分配或释放物理内存。 有关设置缓冲区访问和分配和释放内存的详细信息，请参阅[内存管理](https://docs.microsoft.com/windows-hardware/drivers/kernel/managing-memory-for-drivers)和[缓冲区管理](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)。

### <a name="allocating-low-memory-for-rdma"></a>为 RDMA 分配低内存

代理驱动程序必须分配可为 RDMA 操作访问的内存。 代理驱动程序可以为 RDMA 操作分配低内存，即使在配置的系统上，也不能分配低于 4 GB 的物理内存。 （这称为 NOLOWMEM 配置。）代理驱动程序调用[**MmAllocateContiguousMemorySpecifyCache**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-mmallocatecontiguousmemoryspecifycache)函数或其自己的 DMA [**AllocateCommonBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-pallocate_common_buffer)函数来检索内存不足的情况。

若要检索指向其 DMA **AllocateCommonBuffer**函数的指针，代理驱动程序将执行以下步骤：

1.  零-初始化[**设备\_说明**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_device_description)结构，然后将其 SAN NIC 的相关信息写入到此结构中。

2.  调用[**IoGetDmaAdapter**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetdmaadapter)为其 SAN NIC 检索指向 DMA 适配器结构的指针。 在此调用中，驱动程序将指针传递到已填充设备\_说明结构。 **IoGetDmaAdapter**返回一个指向 dma 适配器结构的指针，该结构包含指向[**dma\_操作**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_dma_operations)结构的指针。 DMA\_操作包含指向系统定义的 DMA 函数集的指针。 其中一个函数为**AllocateCommonBuffer**，它分配一个物理上连续的 DMA 缓冲区。

 

 





