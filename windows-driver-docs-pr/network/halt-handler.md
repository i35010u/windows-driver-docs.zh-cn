---
title: 微型端口驱动程序停止处理程序
description: 微型端口驱动程序停止处理程序
keywords:
- MiniportHaltEx
- 暂停处理程序 WDK NDIS
- 卸载微型端口驱动程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cb5723058e082891d6dd12ca49be48830f602791
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96840025"
---
# <a name="miniport-driver-halt-handler"></a>微型端口驱动程序停止处理程序





NDIS 微型端口驱动程序必须向 [**NdisMRegisterMiniportDriver**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismregisterminiportdriver)提供 [*MiniportHaltEx*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_halt)函数。

*MiniportHaltEx* 应撤消 [*MiniportInitializeEx*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize) 执行的所有操作。 例如，NDIS 微型端口驱动程序可以：

-   可用端口。  (有关详细信息，请参阅 [释放 NDIS 端口](freeing-an-ndis-port.md)。 ) 

-   释放 [*MiniportInitializeEx*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize) 声称的所有硬件资源。

-   通过调用 [**NdisMDeregisterInterruptEx**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismderegisterinterruptex)来释放中断资源。

-   释放 [*MiniportInitializeEx*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize) 分配的任何内存。

-   停止 NIC，除非 [*MiniportShutdownEx*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_shutdown) 函数已将 nic 恢复到其初始状态。

下图说明了如何卸载微型端口驱动程序。

![说明卸载微型端口驱动程序的图示](images/207-11.png)

*MiniportHaltEx* 应完成在返回前卸载驱动程序所需的操作。 如果微型端口驱动程序具有任何未完成的接收指示 (即，接收到的网络数据已指明最多 NDIS 但尚未返回) ，则在将此类数据返回到微型端口驱动程序的 [*MiniportReturnNetBufferLists*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_return_net_buffer_lists)函数之前， *MiniportHaltEx* 不得返回。

上图显示了一组可由 *MiniportHaltEx* 函数进行的调用。 这些调用只是可以进行的调用的一个子集。 实际的调用集取决于微型端口驱动程序的先前操作。 如果由于硬件问题或无法获取所需资源，微型端口驱动程序可在 *MiniportInitializeEx* 中进行这些相同的调用。 在这种情况下， *MiniportInitializeEx* 应通过撤消其先前的操作来卸载驱动程序。 否则， *MiniportHaltEx* 将撤消 *MiniportInitializeEx* 的操作。

以下列表描述了撤消微型端口驱动程序可能需要执行的某些操作所需的调用：

-   如果微型端口驱动程序已注册中断，则它应调用 [**NdisMDeregisterInterruptEx**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismderegisterinterruptex)。

-   如果微型端口驱动程序设置计时器或计时器，则它应为其创建的每个计时器调用 [**NdisCancelTimerObject**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscanceltimerobject) 。 如果对 **NdisCancelTimerObject** 的调用失败，则可能已激发计时器。 在这种情况下，微型端口驱动程序应等待计时器处理程序完成，然后从 *MiniportHaltEx* 中返回。

-   如果微型端口驱动程序向 [**NdisAllocateMemoryWithTagPriority**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisallocatememorywithtagpriority)分配了任何内存，则它应调用 [**NdisFreeMemory**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfreememory) 以释放该内存。

-   如果微型端口驱动程序向 [**NdisMAllocateSharedMemory**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismallocatesharedmemory)或 [**NdisMAllocateSharedMemoryAsyncEx**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismallocatesharedmemoryasyncex)分配了任何内存，则它应调用 [**NdisMFreeSharedMemory**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismfreesharedmemory) 以释放该内存。

-   如果微型端口驱动程序为具有 [**NdisAllocateNetBufferPool**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisallocatenetbufferlistpool)的数据包描述符池分配和初始化存储，则它应调用 [**NdisFreeNetBufferPool**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfreenetbufferpool) 以释放该存储。

-   如果小型小型驱动程序已分配或保留任何硬件资源，则应返回这些资源。 例如，如果微型端口驱动程序映射了 NIC 上的 i/o 端口范围，则应通过调用 [**NdisMDeregisterIoPortRange**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismderegisterioportrange)来释放这些端口。

## <a name="related-topics"></a>相关主题


[微型端口驱动程序的适配器状态](adapter-states-of-a-miniport-driver.md)

[释放 NDIS 端口](freeing-an-ndis-port.md)

[停止微型端口适配器](halting-a-miniport-adapter.md)

[微型端口适配器状态和操作](miniport-adapter-states-and-operations.md)

[微型端口驱动程序重置和停止函数](/previous-versions/windows/hardware/network/ff564064(v=vs.85))

 

