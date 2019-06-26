---
title: 对 DMA 硬件编程
description: 本主题介绍总线 master DMA 设备的 KMDF 驱动程序通常在其 EvtProgramDma 事件的回调函数中提供的功能。
ms.assetid: 5e74fe74-d38f-4cca-b0cf-8a6f170c4dc5
keywords:
- DMA 操作 WDK KMDF 传输
- 主总线 DMA WDK KMDF 传输
- DMA 传输 WDK KMDF，硬件
- DMA 传输 WDK KMDF，启动
- 启动 DMA 传输 WDK KMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2c2e6461297a8e59b158ca10b7591bbb63d8de99
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67376308"
---
# <a name="programming-dma-hardware"></a>对 DMA 硬件编程


\[仅适用于 KMDF\]

本主题介绍总线 master DMA 设备的 KMDF 驱动程序通常在提供的功能及其[ *EvtProgramDma* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdmatransaction/nc-wdfdmatransaction-evt_wdf_program_dma)事件回调函数。 如果您的驱动程序使用了框架的 DMA 支持，该驱动程序必须提供此回调。 此信息也适用于 KMDF 驱动程序[系统模式 DMA 设备](supporting-system-mode-dma.md)具有的硬件中断。




[ *EvtProgramDma* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdmatransaction/nc-wdfdmatransaction-evt_wdf_program_dma)回调函数的调用在 IRQL = 调度\_级别，程序设备开始[DMA 传输](dma-transactions-and-dma-transfers.md)。 此回调函数的输入的参数提供的传输方向 （输入或输出） 和分散/集中列表。 如果传输包括单个数据包，散播-聚集列表将包含单个元素。

[ *EvtProgramDma* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdmatransaction/nc-wdfdmatransaction-evt_wdf_program_dma)回调函数程序使用的硬件资源的设备的驱动程序[ *EvtDevicePrepareHardware* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_prepare_hardware)收到的回调函数。 如果*EvtProgramDma*回调函数已成功计划硬件，它将返回**TRUE**。

硬件已完成 DMA 传输，通常在硬件发出中断，并且系统调用驱动程序的后[ *EvtInterruptIsr* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_isr)回调函数。 在驱动程序*EvtInterruptIsr*通常回调函数：

-   清除硬件中断。

-   如果需要将保存中断的上下文信息。 回调函数返回后系统会降低 IRQL （因为降低 IRQL 允许其他中断的发生），此信息可能会丢失。

-   调用[ **WdfInterruptQueueDpcForIsr** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfinterrupt/nf-wdfinterrupt-wdfinterruptqueuedpcforisr)计划[ *EvtInterruptDpc* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_dpc)回调函数。

[ *EvtInterruptDpc* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_dpc)回调函数[完成 DMA 传输](completing-a-dma-transfer.md)使用的上下文信息的[ *EvtInterruptIsr* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_isr)保存的回调函数。

如果[ *EvtProgramDma* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdmatransaction/nc-wdfdmatransaction-evt_wdf_program_dma)回调函数检测到错误，该驱动程序可以停止该事务。

驱动程序检测到错误时停止事务[ *EvtProgramDma* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdmatransaction/nc-wdfdmatransaction-evt_wdf_program_dma)回调函数必须：

1.  调用[ **WdfDmaTransactionDmaCompletedFinal**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdmatransaction/nf-wdfdmatransaction-wdfdmatransactiondmacompletedfinal)。

2.  调用[ **WdfObjectDelete** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfobject/nf-wdfobject-wdfobjectdelete) delete DMA 事务对象，或调用[ **WdfDmaTransactionRelease** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdmatransaction/nf-wdfdmatransaction-wdfdmatransactionrelease)发布和重复使用 DMA事务对象。

3.  [对 I/O 请求重新排队](requeuing-i-o-requests.md)或[完成 I/O 请求](completing-i-o-requests.md)，如果该事务与 framework 请求对象相关联。 若要检索请求的句柄，该驱动程序可以调用[ **WdfDmaTransactionGetRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdmatransaction/nf-wdfdmatransaction-wdfdmatransactiongetrequest)。

4.  返回**FALSE**。

步骤 1 和 4 所示下面的代码示例摘自[PLX9x5x](https://go.microsoft.com/fwlink/p/?linkid=256157)示例的[ *EvtProgramDma* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdmatransaction/nc-wdfdmatransaction-evt_wdf_program_dma) 中读取请求的回调函数*Read.c*文件。

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

此示例调用**PLxReadRequestComplete**函数来执行步骤 2 和 3:

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









