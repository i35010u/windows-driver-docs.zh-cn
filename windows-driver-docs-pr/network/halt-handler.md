---
title: 微型端口驱动程序停止处理程序
description: 微型端口驱动程序停止处理程序
ms.assetid: 63b0b25e-f52f-4486-a57d-448985207fc8
keywords:
- MiniportHaltEx
- 暂停处理程序 WDK NDIS
- 卸载微型端口驱动程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c4daef1f1cd839ce1e0dea95e0cea9a519ac911a
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840485"
---
# <a name="miniport-driver-halt-handler"></a>微型端口驱动程序停止处理程序





NDIS 微型端口驱动程序必须向[**NdisMRegisterMiniportDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismregisterminiportdriver)提供[*MiniportHaltEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_halt)函数。

*MiniportHaltEx*应撤消[*MiniportInitializeEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)执行的所有操作。 例如，NDIS 微型端口驱动程序可以：

-   可用端口。 （有关详细信息，请参阅[释放 NDIS 端口](freeing-an-ndis-port.md)。）

-   释放[*MiniportInitializeEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)声称的所有硬件资源。

-   通过调用[**NdisMDeregisterInterruptEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismderegisterinterruptex)来释放中断资源。

-   释放[*MiniportInitializeEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)分配的任何内存。

-   停止 NIC，除非[*MiniportShutdownEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_shutdown)函数已将 nic 恢复到其初始状态。

下图说明了如何卸载微型端口驱动程序。

![说明卸载微型端口驱动程序的图示](images/207-11.png)

*MiniportHaltEx*应完成在返回前卸载驱动程序所需的操作。 如果微型端口驱动程序有任何未完成的接收指示（即接收到的网络数据已指明最多 NDIS 但尚未返回），则在将此类数据返回到微型端口驱动程序的[*MiniportHaltEx 之前，不能返回MiniportReturnNetBufferLists*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_return_net_buffer_lists)函数。

上图显示了一组可由*MiniportHaltEx*函数进行的调用。 这些调用只是可以进行的调用的一个子集。 实际的调用集取决于微型端口驱动程序的先前操作。 如果由于硬件问题或无法获取所需资源，微型端口驱动程序可在*MiniportInitializeEx*中进行这些相同的调用。 在这种情况下， *MiniportInitializeEx*应通过撤消其先前的操作来卸载驱动程序。 否则， *MiniportHaltEx*将撤消*MiniportInitializeEx*的操作。

以下列表描述了撤消微型端口驱动程序可能需要执行的某些操作所需的调用：

-   如果微型端口驱动程序已注册中断，则它应调用[**NdisMDeregisterInterruptEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismderegisterinterruptex)。

-   如果微型端口驱动程序设置计时器或计时器，则它应为其创建的每个计时器调用[**NdisCancelTimerObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscanceltimerobject) 。 如果对**NdisCancelTimerObject**的调用失败，则可能已激发计时器。 在这种情况下，微型端口驱动程序应等待计时器处理程序完成，然后从*MiniportHaltEx*中返回。

-   如果微型端口驱动程序向[**NdisAllocateMemoryWithTagPriority**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisallocatememorywithtagpriority)分配了任何内存，则它应调用[**NdisFreeMemory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfreememory)以释放该内存。

-   如果微型端口驱动程序向[**NdisMAllocateSharedMemory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismallocatesharedmemory)或[**NdisMAllocateSharedMemoryAsyncEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismallocatesharedmemoryasyncex)分配了任何内存，则它应调用[**NdisMFreeSharedMemory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismfreesharedmemory)以释放该内存。

-   如果微型端口驱动程序为具有[**NdisAllocateNetBufferPool**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisallocatenetbufferlistpool)的数据包描述符池分配和初始化存储，则它应调用[**NdisFreeNetBufferPool**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfreenetbufferpool)以释放该存储。

-   如果小型小型驱动程序已分配或保留任何硬件资源，则应返回这些资源。 例如，如果微型端口驱动程序映射了 NIC 上的 i/o 端口范围，则应通过调用[**NdisMDeregisterIoPortRange**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismderegisterioportrange)来释放这些端口。

## <a name="related-topics"></a>相关主题


[微型端口驱动程序的适配器状态](adapter-states-of-a-miniport-driver.md)

[释放 NDIS 端口](freeing-an-ndis-port.md)

[停止微型端口适配器](halting-a-miniport-adapter.md)

[微型端口适配器状态和操作](miniport-adapter-states-and-operations.md)

[微型端口驱动程序重置和暂停函数](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff564064(v=vs.85))

 

 






