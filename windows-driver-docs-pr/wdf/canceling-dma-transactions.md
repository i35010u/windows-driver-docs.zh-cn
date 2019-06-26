---
title: 取消 DMA 事务
description: 取消 DMA 事务
ms.assetid: 1E1D659D-80C9-45B1-B96F-78E5A1EE4F6B
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8893f534b05f289bf994ae2091c14464542c693d
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67374622"
---
# <a name="canceling-dma-transactions"></a>取消 DMA 事务


\[仅适用于 KMDF\]

如果您的驱动程序已生成了具有版本 1.11 或更高版本的 KMDF 和 Windows 8 上运行或更高版本使用直接内存访问 (DMA) 版本 3，则驱动程序可以尝试通过调用取消挂起的 DMA 事务[ **WdfDmaTransactionCancel** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdmatransaction/nf-wdfdmatransaction-wdfdmatransactioncancel)方法。

调用时[ **WdfDmaTransactionCancel**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdmatransaction/nf-wdfdmatransaction-wdfdmatransactioncancel)，驱动程序必须确保在调用期间未完成指定的 DMA 事务。 该驱动程序可以使用以下技术来安全地取消事务，DMA 通道分配之前或之后一定数量的传输操作已完成：

1.  中的驱动程序之一[请求处理程序](request-handlers.md)，驱动程序调用[ **WdfRequestMarkCancelableEx** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestmarkcancelableex) ，并提供[ *EvtRequestCancel* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nc-wdfrequest-evt_wdf_request_cancel) I/O 请求的回调函数。 然后，请求处理程序调用[ **WdfDmaTransactionExecute**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdmatransaction/nf-wdfdmatransaction-wdfdmatransactionexecute)。
2.  在驱动程序[ *EvtRequestCancel* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nc-wdfrequest-evt_wdf_request_cancel)回调函数 (这可能会开始在一个单独的线程中运行到调用后面紧接着[ **WdfRequestMarkCancelableEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestmarkcancelableex)) 调用[ **WdfDmaTransactionCancel**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdmatransaction/nf-wdfdmatransaction-wdfdmatransactioncancel)。
3.  如果在调用[ **WdfDmaTransactionCancel** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdmatransaction/nf-wdfdmatransaction-wdfdmatransactioncancel)发生在调用后[ **WdfDmaTransactionExecute**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdmatransaction/nf-wdfdmatransaction-wdfdmatransactionexecute)，但之前**WdfDmaTransactionExecute**方法已启动 DMA 分配、 事务取消成功并**WdfDmaTransactionCancel** ，则返回 TRUE。 在此情况下，该驱动程序的[ *EvtRequestCancel* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nc-wdfrequest-evt_wdf_request_cancel)回调函数必须[完成 DMA 事务](completing-a-dma-transaction.md)。 **WdfDmaTransactionExecute**返回一个错误值。
4.  如果该驱动程序调用[ **WdfDmaTransactionCancel** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdmatransaction/nf-wdfdmatransaction-wdfdmatransactioncancel)后[ **WdfDmaTransactionExecute** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdmatransaction/nf-wdfdmatransaction-wdfdmatransactionexecute)方法已启动 DMA 分配尝试取消该事务会失败并**WdfDmaTransactionCancel**返回 FALSE。 在这种情况下， **WdfDmaTransactionExecute**将返回状态\_成功和驱动程序的请求处理程序必须[完成 DMA 事务](completing-a-dma-transaction.md)。

    此时，如果该驱动程序使用系统模式 DMA [ *EvtRequestCancel* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nc-wdfrequest-evt_wdf_request_cancel)回调函数可能会调用[ **WdfDmaTransactionStopSystemTransfer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdmatransaction/nf-wdfdmatransaction-wdfdmatransactionstopsystemtransfer)尝试停止正在进行系统模式 DMA 传输。 有关代码示例演示如何执行此操作，请参阅[ **WdfDmaTransactionStopSystemTransfer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdmatransaction/nf-wdfdmatransaction-wdfdmatransactionstopsystemtransfer)。

5.  之后[ **WdfDmaTransactionExecute** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdmatransaction/nf-wdfdmatransaction-wdfdmatransactionexecute)方法完成后 DMA 分配，框架将调用的驱动程序[ *EvtProgramDma* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdmatransaction/nc-wdfdmatransaction-evt_wdf_program_dma)回调函数 (这可能会开始在一个单独的线程中运行到调用后面紧接着**WdfDmaTransactionExecute**)。 此时，调用[ **WdfDmaTransactionCancel** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdmatransaction/nf-wdfdmatransaction-wdfdmatransactioncancel)方法将返回 FALSE。

    在中[ *EvtProgramDma*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdmatransaction/nc-wdfdmatransaction-evt_wdf_program_dma)，该驱动程序可以调用[ **WdfRequestUnmarkCancelable** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestunmarkcancelable)结束请求取消的可能性。 如果**WdfRequestUnmarkCancelable**将返回状态\_成功后，回调函数必须进行编程的硬件开始传输。 如果**WdfRequestUnmarkCancelable**将返回状态\_取消，请求已被取消。 在这种情况下， *EvtProgramDma*必须调用[ **WdfDmaTransactionDmaCompletedFinal** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdmatransaction/nf-wdfdmatransaction-wdfdmatransactiondmacompletedfinal)到[完成 DMA 事务](completing-a-dma-transaction.md)。

    该驱动程序可以使用相同技术来取消 DMA 事务之后一定数量的传输操作已完成。 在这种情况下，驱动程序调用[ **WdfDmaTransactionCancel** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdmatransaction/nf-wdfdmatransaction-wdfdmatransactioncancel)它将调用后[ **WdfDmaTransactionDmaCompleted**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdmatransaction/nf-wdfdmatransaction-wdfdmatransactiondmacompleted)，之前框架将调用[ *EvtProgramDma* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdmatransaction/nc-wdfdmatransaction-evt_wdf_program_dma)进行编程在下一步的传输操作。 如果该驱动程序调用恰好**WdfDmaTransactionCancel**调用之前**WdfDmaTransactionDmaCompleted**， **WdfDmaTransactionDmaCompleted**返回 **，则返回 TRUE**，表明 DMA 事务已完成。

 

 





