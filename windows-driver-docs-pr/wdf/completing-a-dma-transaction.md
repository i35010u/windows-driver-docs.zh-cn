---
title: 完成 DMA 事务
description: 完成 DMA 事务
ms.assetid: 90531b72-e51d-451e-ae84-a9bbf0245665
keywords:
- DMA 事务 WDK KMDF，完成
- DMA 操作 WDK KMDF，事务
- 主总线 DMA WDK KMDF 事务
- 完成 DMA 事务 WDK KMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1956df42c795feeb8da6794f1b5b939544b20934
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56547054"
---
# <a name="completing-a-dma-transaction"></a>完成 DMA 事务


\[仅适用于 KMDF\]




每次驱动程序的设备[完成 DMA 传输](completing-a-dma-transfer.md)，该驱动程序必须调用[ **WdfDmaTransactionDmaCompleted**](https://msdn.microsoft.com/library/windows/hardware/ff547039)， [ **WdfDmaTransactionDmaCompletedWithLength**](https://msdn.microsoft.com/library/windows/hardware/ff547052)，或[ **WdfDmaTransactionDmaCompletedFinal** ](https://msdn.microsoft.com/library/windows/hardware/ff547049) ，然后检查返回值。

当返回值是 **，则返回 TRUE**、 没有更多传输所需的 DMA 事务和驱动程序必须完成 DMA 事务。 通常情况下，该驱动程序尚未返回从其[ *EvtInterruptDpc* ](https://msdn.microsoft.com/library/windows/hardware/ff541721)回调函数。 因此，此回调函数完成通过 DMA 事务：

1.  调用[ **WdfObjectDelete** ](https://msdn.microsoft.com/library/windows/hardware/ff548734)到删除的事务对象或调用[ **WdfDmaTransactionRelease** ](https://msdn.microsoft.com/library/windows/hardware/ff547114)如果驱动程序[重用 DMA 事务对象](reusing-dma-transaction-objects.md)。

2.  调用[ **WdfRequestComplete** ](https://msdn.microsoft.com/library/windows/hardware/ff549945)或[ **WdfRequestCompleteWithInformation**](https://msdn.microsoft.com/library/windows/hardware/ff549948)，如果事务是一种框架与相关联请求对象。

如果该驱动程序调用[ **WdfRequestCompleteWithInformation**](https://msdn.microsoft.com/library/windows/hardware/ff549948)，它通常第一个调用[ **WdfDmaTransactionGetBytesTransferred** ](https://msdn.microsoft.com/library/windows/hardware/ff547072)若要获取的所有事务的传输的总长度 （字节数）。

在下面的代码示例中，来自说明了这些步骤[PLX9x5x](https://go.microsoft.com/fwlink/p/?linkid=256157)示例的[ *EvtInterruptDpc* ](https://msdn.microsoft.com/library/windows/hardware/ff541721)中的回调函数*Isrdpc.c*文件：

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









