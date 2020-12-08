---
title: 对 DMA 硬件编程
description: 本主题介绍了 KMDF 驱动程序的总线主控 DMA 设备的 EvtProgramDma 事件回调函数中通常提供的功能。
keywords:
- DMA 操作 WDK KMDF，传输
- 总线主控 DMA WDK KMDF，传输
- DMA 传输 WDK KMDF，硬件
- DMA 传输 WDK KMDF，开始
- 启动 DMA 传输 WDK KMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 20065dc1e897c3e2be468258f53950938816ff11
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96828309"
---
# <a name="programming-dma-hardware"></a>对 DMA 硬件编程


\[仅适用于 KMDF\]

本主题介绍了 KMDF 驱动程序的总线主控 DMA 设备的 [*EvtProgramDma*](/windows-hardware/drivers/ddi/wdfdmatransaction/nc-wdfdmatransaction-evt_wdf_program_dma) 事件回调函数中通常提供的功能。 如果驱动程序使用框架的 DMA 支持，则驱动程序必须提供此回调。 此信息也适用于具有硬件中断的 [系统模式 DMA 设备](supporting-system-mode-dma.md) 的 KMDF 驱动程序。




在 IRQL = 调度级别调用的 [*EvtProgramDma*](/windows-hardware/drivers/ddi/wdfdmatransaction/nc-wdfdmatransaction-evt_wdf_program_dma) 回调函数会使 \_ 设备启动 [DMA 传输](dma-transactions-and-dma-transfers.md)。 此回调函数的输入参数提供了传输方向 (输入或输出) 和散点/集合列表。 如果传输包含单个数据包，则散点/集合列表包含单个元素。

[*EvtProgramDma*](/windows-hardware/drivers/ddi/wdfdmatransaction/nc-wdfdmatransaction-evt_wdf_program_dma)回调函数使用驱动程序的 [*EvtDevicePrepareHardware*](/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_prepare_hardware)回调函数接收的硬件资源来对设备进行计划。 如果 *EvtProgramDma* 回调函数成功对硬件进行了计划，它将返回 **TRUE**。

在硬件完成 DMA 传输后，通常情况下，硬件会发出中断，系统会调用驱动程序的 [*EvtInterruptIsr*](/windows-hardware/drivers/ddi/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_isr) 回调函数。 驱动程序的 *EvtInterruptIsr* 回调函数通常是：

-   清除硬件中断。

-   如果需要，保存中断的上下文信息。 此信息可能会在回调函数返回之后丢失，并且系统降低了 IRQL (因为降低 IRQL 会允许) 发生额外的中断。

-   调用 [**WdfInterruptQueueDpcForIsr**](/windows-hardware/drivers/ddi/wdfinterrupt/nf-wdfinterrupt-wdfinterruptqueuedpcforisr) 来计划 [*EvtInterruptDpc*](/windows-hardware/drivers/ddi/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_dpc) 回调函数。

[*EvtInterruptDpc*](/windows-hardware/drivers/ddi/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_dpc)回调函数通过使用 [*EvtInterruptIsr*](/windows-hardware/drivers/ddi/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_isr)回调函数保存的上下文信息 [完成 DMA 传输](completing-a-dma-transfer.md)。

如果 [*EvtProgramDma*](/windows-hardware/drivers/ddi/wdfdmatransaction/nc-wdfdmatransaction-evt_wdf_program_dma) 回调函数检测到错误，则驱动程序可以停止事务。

若要在驱动程序检测到错误时停止事务， [*EvtProgramDma*](/windows-hardware/drivers/ddi/wdfdmatransaction/nc-wdfdmatransaction-evt_wdf_program_dma) 回调函数必须：

1.  调用 [**WdfDmaTransactionDmaCompletedFinal**](/windows-hardware/drivers/ddi/wdfdmatransaction/nf-wdfdmatransaction-wdfdmatransactiondmacompletedfinal)。

2.  调用 [**WdfObjectDelete**](/windows-hardware/drivers/ddi/wdfobject/nf-wdfobject-wdfobjectdelete) 以删除 dma 事务对象，或调用 [**WdfDmaTransactionRelease**](/windows-hardware/drivers/ddi/wdfdmatransaction/nf-wdfdmatransaction-wdfdmatransactionrelease) 以释放并重复使用 dma 事务对象。

3.  如果事务与框架请求对象关联，则[重新排队 i/o 请求](requeuing-i-o-requests.md)或[完成 i/o 请求](completing-i-o-requests.md)。 若要检索请求的句柄，驱动程序可以调用 [**WdfDmaTransactionGetRequest**](/windows-hardware/drivers/ddi/wdfdmatransaction/nf-wdfdmatransaction-wdfdmatransactiongetrequest)。

4.  返回 **FALSE**。

下面的代码示例演示了步骤1和步骤4，这些代码示例摘自 *读取 .c* 文件中读取请求的 [PLX9x5x](/samples/browse/)示例的 [*EvtProgramDma*](/windows-hardware/drivers/ddi/wdfdmatransaction/nc-wdfdmatransaction-evt_wdf_program_dma)回调函数。

```cpp
    // If errors occur in the EvtProgramDma callback,
    // release the DMA transaction object and complete the request.

    if (errors) {
        NTSTATUS status;

        //
        // Must abort the transaction before deleting.
        //
        (VOID) WdfDmaTransactionDmaCompletedFinal(Transaction, 0, &status);
        ASSERT(NT_SUCCESS(status));

        PLxReadRequestComplete( Transaction, STATUS_INVALID_DEVICE_STATE );
        TraceEvents(TRACE_LEVEL_ERROR, DBG_READ,
                    "<-- PLxEvtProgramReadDma: errors ****");
        return FALSE;
    }
```

该示例调用 **PLxReadRequestComplete** 函数来执行步骤2和3：

```cpp
VOID
PLxReadRequestComplete(
    IN WDFDMATRANSACTION  DmaTransaction,
    IN NTSTATUS           Status
    )
/*++

Routine Description:

Arguments:

Return Value:

--*/
{
    WDFREQUEST         request;
    size_t             bytesTransferred;

    //
    // Get the associated request from the transaction.
    //
    request = WdfDmaTransactionGetRequest(DmaTransaction);

    ASSERT(request);

    //
    // Get the final bytes transferred count.
    //
    bytesTransferred =  WdfDmaTransactionGetBytesTransferred( DmaTransaction );

    TraceEvents(TRACE_LEVEL_INFORMATION, DBG_DPC,
                "PLxReadRequestComplete:  Request %p, Status %!STATUS!, "
                "bytes transferred %d\n",
                 request, Status, (int) bytesTransferred );

    WdfDmaTransactionRelease(DmaTransaction);

    //
    // Complete this Request.
    //
    WdfRequestCompleteWithInformation( request, Status, bytesTransferred);

}
```
