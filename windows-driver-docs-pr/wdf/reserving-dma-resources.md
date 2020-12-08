---
title: 保留 DMA 资源
description: 保留 DMA 资源
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 84accc8d4ec7c14347917c1056c2a2fcc84c8446
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96819923"
---
# <a name="reserving-dma-resources"></a>保留 DMA 资源


\[仅适用于 KMDF\]

通常，基于框架的驱动程序不会提前保留映射寄存器。 但是，在某些情况下，驱动程序可能需要预先保留这些资源。

在 Windows 8 或更高版本上运行的基于框架的驱动程序可以为指定数据包或系统配置文件的 DMA 启用码保留指定数量的映射寄存器。 为此，驱动程序将调用 [**WdfDmaTransactionAllocateResources**](/windows-hardware/drivers/ddi/wdfdmatransaction/nf-wdfdmatransaction-wdfdmatransactionallocateresources) 并注册 [*EvtReserveDma*](/windows-hardware/drivers/ddi/wdfdmatransaction/nc-wdfdmatransaction-evt_wdf_reserve_dma) 回调函数。

当驱动程序已保留映射寄存器和 WDM DMA 适配器的锁时，框架将调用该驱动程序的 [*EvtReserveDma*](/windows-hardware/drivers/ddi/wdfdmatransaction/nc-wdfdmatransaction-evt_wdf_reserve_dma) 函数。 然后，该驱动程序可以在最后释放事务对象之前，使用同一个事务对象多次初始化和启动该事务。 若要将 DMA 资源释放回系统，驱动程序将调用 [**WdfDmaTransactionFreeResources**](/windows-hardware/drivers/ddi/wdfdmatransaction/nf-wdfdmatransaction-wdfdmatransactionfreeresources)。

若要确定事务所需的映射寄存器数量，驱动程序可以在调用 [**WdfDmaTransactionAllocateResources**](/windows-hardware/drivers/ddi/wdfdmatransaction/nf-wdfdmatransaction-wdfdmatransactionallocateresources)之前调用 [**WdfDmaTransactionGetTransferInfo**](/windows-hardware/drivers/ddi/wdfdmatransaction/nf-wdfdmatransaction-wdfdmatransactiongettransferinfo) 。 在调用 **WdfDmaTransactionGetTransferInfo** 之前，驱动程序必须初始化事务。

以下步骤演示了驱动程序如何可以保留和发布 DMA 启用码，以便与指定的事务独占使用：

1.  驱动程序接收 i/o 请求。

2.  驱动程序的 [请求处理程序](request-handlers.md) 调用 [**WdfDmaTransactionCreate**](/windows-hardware/drivers/ddi/wdfdmatransaction/nf-wdfdmatransaction-wdfdmatransactioncreate) 为请求创建 DMA 事务对象。

3.  驱动程序的 [请求处理程序](request-handlers.md) 调用 [**WdfDmaTransactionAllocateResources**](/windows-hardware/drivers/ddi/wdfdmatransaction/nf-wdfdmatransaction-wdfdmatransactionallocateresources) 以保留资源。

4.  当框架已保留请求的资源时，它将调用 [*EvtReserveDma*](/windows-hardware/drivers/ddi/wdfdmatransaction/nc-wdfdmatransaction-evt_wdf_reserve_dma) 。

5.  在 [*EvtReserveDma*](/windows-hardware/drivers/ddi/wdfdmatransaction/nc-wdfdmatransaction-evt_wdf_reserve_dma)中，驱动程序调用 [**WdfDmaTransactionInitializeUsingRequest**](/windows-hardware/drivers/ddi/wdfdmatransaction/nf-wdfdmatransaction-wdfdmatransactioninitializeusingrequest) 或 [**WdfDmaTransactionInitialize**](/windows-hardware/drivers/ddi/wdfdmatransaction/nf-wdfdmatransaction-wdfdmatransactioninitialize) 来初始化事务对象。

6.  在 [*EvtReserveDma*](/windows-hardware/drivers/ddi/wdfdmatransaction/nc-wdfdmatransaction-evt_wdf_reserve_dma)中，驱动程序调用 [**WdfDmaTransactionExecute**](/windows-hardware/drivers/ddi/wdfdmatransaction/nf-wdfdmatransaction-wdfdmatransactionexecute) 方法来启动该事务。 由于事务具有保留的资源，因此框架会立即调用驱动程序的 [*EvtProgramDma*](/windows-hardware/drivers/ddi/wdfdmatransaction/nc-wdfdmatransaction-evt_wdf_program_dma) 回调函数。

7.  从 [*EvtInterruptDpc*](/windows-hardware/drivers/ddi/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_dpc) 或 [*EvtDmaTransactionDmaTransferComplete*](/windows-hardware/drivers/ddi/wdfdmatransaction/nc-wdfdmatransaction-evt_wdf_dma_transaction_dma_transfer_complete)中，驱动程序调用 [**WdfDmaTransactionDmaCompleted**](/windows-hardware/drivers/ddi/wdfdmatransaction/nf-wdfdmatransaction-wdfdmatransactiondmacompleted)、 [**WdfDmaTransactionDmaCompletedWithLength**](/windows-hardware/drivers/ddi/wdfdmatransaction/nf-wdfdmatransaction-wdfdmatransactiondmacompletedwithlength)或 [**WdfDmaTransactionDmaCompletedFinal**](/windows-hardware/drivers/ddi/wdfdmatransaction/nf-wdfdmatransaction-wdfdmatransactiondmacompletedfinal)，后跟 [**WdfObjectDelete**](/windows-hardware/drivers/ddi/wdfobject/nf-wdfobject-wdfobjectdelete) 或 [**WdfDmaTransactionRelease**](/windows-hardware/drivers/ddi/wdfdmatransaction/nf-wdfdmatransaction-wdfdmatransactionrelease)。 在事务完成或取消之前，驱动程序不能删除或释放事务。 完成此步骤后，映射寄存器仍保留。

8.  驱动程序可以根据需要重复执行步骤5–7次。

    当驱动程序不再需要保留时，驱动程序从 [*EvtInterruptDpc*](/windows-hardware/drivers/ddi/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_dpc)或 [*EvtDmaTransactionDmaTransferComplete*](/windows-hardware/drivers/ddi/wdfdmatransaction/nc-wdfdmatransaction-evt_wdf_dma_transaction_dma_transfer_complete)调用 [**WdfDmaTransactionFreeResources**](/windows-hardware/drivers/ddi/wdfdmatransaction/nf-wdfdmatransaction-wdfdmatransactionfreeresources) 。 或者，驱动程序可以从其 [*EvtReserveDma*](/windows-hardware/drivers/ddi/wdfdmatransaction/nc-wdfdmatransaction-evt_wdf_reserve_dma)事件回调函数调用 **WdfDmaTransactionFreeResources** 。

 

