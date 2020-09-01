---
title: 完成 DMA 事务
description: 完成 DMA 事务
ms.assetid: 90531b72-e51d-451e-ae84-a9bbf0245665
keywords:
- DMA 事务 WDK KMDF，完成
- DMA 操作 WDK KMDF，事务
- 总线主控 DMA WDK KMDF，事务
- 完成 DMA 事务 WDK KMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3a820ee580fa7d4797d17fe92c165d00f84cc507
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89184325"
---
# <a name="completing-a-dma-transaction"></a>完成 DMA 事务


\[仅适用于 KMDF\]




每次驱动程序的设备 [完成 DMA 传输](completing-a-dma-transfer.md)时，驱动程序必须调用 [**WdfDmaTransactionDmaCompleted**](/windows-hardware/drivers/ddi/wdfdmatransaction/nf-wdfdmatransaction-wdfdmatransactiondmacompleted)、 [**WdfDmaTransactionDmaCompletedWithLength**](/windows-hardware/drivers/ddi/wdfdmatransaction/nf-wdfdmatransaction-wdfdmatransactiondmacompletedwithlength)或 [**WdfDmaTransactionDmaCompletedFinal**](/windows-hardware/drivers/ddi/wdfdmatransaction/nf-wdfdmatransaction-wdfdmatransactiondmacompletedfinal) ，然后检查返回值。

如果返回值为 **TRUE**，则不需要对 dma 事务进行更多的传输，并且驱动程序必须完成 dma 事务。 通常，驱动程序尚未从其 [*EvtInterruptDpc*](/windows-hardware/drivers/ddi/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_dpc) 回调函数返回。 因此，此回调函数通过以下方式完成 DMA 事务：

1.  调用 [**WdfObjectDelete**](/windows-hardware/drivers/ddi/wdfobject/nf-wdfobject-wdfobjectdelete) 删除 transaction 对象，或调用 [**WdfDmaTransactionRelease**](/windows-hardware/drivers/ddi/wdfdmatransaction/nf-wdfdmatransaction-wdfdmatransactionrelease) （如果驱动程序 [重用 DMA 事务对象](reusing-dma-transaction-objects.md)）。

2.  如果事务与框架请求对象相关联，则调用 [**WdfRequestComplete**](/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestcomplete) 或 [**WdfRequestCompleteWithInformation**](/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestcompletewithinformation)。

如果驱动程序调用 [**WdfRequestCompleteWithInformation**](/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestcompletewithinformation)，则它通常首先调用 [**WdfDmaTransactionGetBytesTransferred**](/windows-hardware/drivers/ddi/wdfdmatransaction/nf-wdfdmatransaction-wdfdmatransactiongetbytestransferred) 来获取事务的所有传输) 的总长度 (字节数。

下面的代码示例阐释了这些步骤，这些步骤取自*Isrdpc*文件中的[PLX9x5x](https://go.microsoft.com/fwlink/p/?linkid=256157)示例的[*EvtInterruptDpc*](/windows-hardware/drivers/ddi/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_dpc)回调函数：

```cpp
if (readComplete) {
    BOOLEAN              transactionComplete;
    WDFDMATRANSACTION    dmaTransaction;
    size_t               bytesTransferred;

    // Get the current Read DmaTransaction.
    dmaTransaction = devExt->CurrentReadDmaTransaction;

    // Indicate that this DMA operation has completed:
    // This may start the transfer on the next packet if 
    // there is still data to be transferred.
    transactionComplete = 
          WdfDmaTransactionDmaCompleted( dmaTransaction, &status ); 
    if (transactionComplete) {
        // Complete the DmaTransaction and the request.
        devExt->CurrentReadDmaTransaction = NULL;
        bytesTransferred =  
               ((NT_SUCCESS(status)) ? 
               WdfDmaTransactionGetBytesTransferred(dmaTransaction): 0 );
        WdfDmaTransactionRelease(dmaTransaction);
        WdfRequestCompleteWithInformation(request, status, bytesTransferred);
    }
}
```