---
title: 微型端口驱动程序停止处理程序
description: 微型端口驱动程序停止处理程序
ms.assetid: 63b0b25e-f52f-4486-a57d-448985207fc8
keywords:
- MiniportHaltEx
- 停止处理程序 WDK NDIS
- 正在卸载的微型端口驱动程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6dc013a34451cff8c9f193cb1cfcaecf7b9ea892
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67374083"
---
# <a name="miniport-driver-halt-handler"></a>微型端口驱动程序停止处理程序





NDIS 微型端口驱动程序必须提供[ *MiniportHaltEx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_halt)函数来[ **NdisMRegisterMiniportDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismregisterminiportdriver)。

*MiniportHaltEx*应撤消所有内容， [ *MiniportInitializeEx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_initialize)未。 例如，可能会 NDIS 微型端口驱动程序：

-   可用端口。 (有关详细信息，请参阅[释放 NDIS 端口](freeing-an-ndis-port.md)。)

-   释放所有硬件资源的[ *MiniportInitializeEx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_initialize)声明。

-   通过调用释放中断资源[ **NdisMDeregisterInterruptEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismderegisterinterruptex)。

-   释放任何内存， [ *MiniportInitializeEx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_initialize)分配。

-   停止 NIC，除非[ *MiniportShutdownEx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_shutdown)函数都还原到其初始状态 NIC。

下图说明了卸载微型端口驱动程序。

![说明卸载微型端口驱动程序的关系图](images/207-11.png)

*MiniportHaltEx*应完成所需卸载该驱动程序返回之前的操作。 如果具有所有未完成的微型端口驱动程序收到指示 （也就是说，它已指明最多的 NDIS 但 NDIS 接收的网络数据尚未返回）， *MiniportHaltEx*不能返回直到此类数据返回到微型端口驱动程序[ *MiniportReturnNetBufferLists* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_return_net_buffer_lists)函数。

上图显示了一组可以通过调用*MiniportHaltEx*函数。 这些调用将无法进行的调用的一个子集。 实际组调用取决于以前的微型端口驱动程序的操作。 微型端口驱动程序可以使这些调用中的相同*MiniportInitializeEx*如果它无法成功初始化的网络适配器，由于硬件问题或因为它无法获取其所需的资源。 在这种情况下， *MiniportInitializeEx*应卸载该驱动程序通过撤消其以前的操作。 否则为*MiniportHaltEx*将撤消的操作*MiniportInitializeEx*。

以下列表描述反向微型端口驱动程序可能需要某些操作所需的调用：

-   如果微型端口驱动程序已注册中断，则应调用[ **NdisMDeregisterInterruptEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismderegisterinterruptex)。

-   如果微型端口驱动程序设置了一个计时器或计时器，则应调用[ **NdisCancelTimerObject** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndiscanceltimerobject)为它创建的每个计时器。 如果调用**NdisCancelTimerObject**失败，计时器可能具有已激发。 在这种情况下，微型端口驱动程序应等待计时器处理程序，若要完成从返回前*MiniportHaltEx*。

-   如果微型端口驱动程序分配任何内存以及[ **NdisAllocateMemoryWithTagPriority**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisallocatememorywithtagpriority)，则应调用[ **NdisFreeMemory** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisfreememory)到释放该内存。

-   如果微型端口驱动程序分配任何内存以及[ **NdisMAllocateSharedMemory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismallocatesharedmemory)，或[ **NdisMAllocateSharedMemoryAsyncEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismallocatesharedmemoryasyncex)，它应调用[ **NdisMFreeSharedMemory** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismfreesharedmemory)来释放该内存。

-   如果微型端口驱动程序分配并初始化存储池使用的数据包描述符[ **NdisAllocateNetBufferPool**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisallocatenetbufferlistpool)，则应调用[ **NdisFreeNetBufferPool** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisfreenetbufferpool)来释放该存储。

-   如果微型端口驱动程序分配或保留的任何硬件资源，这些应返回。 例如，如果微型端口驱动程序映射 NIC 上的 I/O 端口范围，它应释放端口通过调用[ **NdisMDeregisterIoPortRange**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismderegisterioportrange)。

## <a name="related-topics"></a>相关主题


[适配器状态的微型端口驱动程序](adapter-states-of-a-miniport-driver.md)

[释放 NDIS 端口](freeing-an-ndis-port.md)

[正在停止微型端口适配器](halting-a-miniport-adapter.md)

[微型端口适配器状态和操作](miniport-adapter-states-and-operations.md)

[微型端口驱动程序重置和 Halt 函数](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff564064(v=vs.85))

 

 






