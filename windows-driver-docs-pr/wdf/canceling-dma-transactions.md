---
title: 取消 DMA 事务
description: 取消 DMA 事务
ms.assetid: 1E1D659D-80C9-45B1-B96F-78E5A1EE4F6B
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f7bc96743a2c550e498d976a02418765f3ef4238
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845506"
---
# <a name="canceling-dma-transactions"></a>取消 DMA 事务


\[仅适用于 KMDF\]

如果你的驱动程序是使用版本1.11 或更高版本的 KMDF 生成的，并且在 Windows 8 或更高版本上使用直接内存访问（DMA）版本3运行，则驱动程序可以通过调用[**WdfDmaTransactionCancel**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdmatransaction/nf-wdfdmatransaction-wdfdmatransactioncancel)方法来尝试取消挂起的 DMA 事务.

调用[**WdfDmaTransactionCancel**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdmatransaction/nf-wdfdmatransaction-wdfdmatransactioncancel)时，驱动程序必须确保在调用期间指定的 DMA 事务未完成。 驱动程序可以使用以下技术在 DMA 通道分配之前或在已经完成一些传输操作后安全取消事务：

1.  在其中一个驱动程序的[请求处理](request-handlers.md)程序中，驱动程序调用[**WdfRequestMarkCancelableEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestmarkcancelableex)并为 i/o 请求提供[*EvtRequestCancel*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nc-wdfrequest-evt_wdf_request_cancel)回调函数。 然后，请求处理程序调用[**WdfDmaTransactionExecute**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdmatransaction/nf-wdfdmatransaction-wdfdmatransactionexecute)。
2.  驱动程序的[*EvtRequestCancel*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nc-wdfrequest-evt_wdf_request_cancel)回调函数（可在调用[**WdfRequestMarkCancelableEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestmarkcancelableex)后立即在单独的线程中运行）调用[**WdfDmaTransactionCancel**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdmatransaction/nf-wdfdmatransaction-wdfdmatransactioncancel)。
3.  如果对[**WdfDmaTransactionCancel**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdmatransaction/nf-wdfdmatransaction-wdfdmatransactioncancel)的调用在调用[**WdfDmaTransactionExecute**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdmatransaction/nf-wdfdmatransaction-wdfdmatransactionexecute)后发生，但在**WdfDmaTransactionExecute**方法开始执行 DMA 分配之前，事务取消将成功 **，WdfDmaTransactionCancel**返回 TRUE。 在这种情况下，驱动程序的[*EvtRequestCancel*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nc-wdfrequest-evt_wdf_request_cancel)回调函数必须[完成 DMA 事务](completing-a-dma-transaction.md)。 **WdfDmaTransactionExecute**返回错误值。
4.  如果驱动程序在[**WdfDmaTransactionExecute**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdmatransaction/nf-wdfdmatransaction-wdfdmatransactionexecute)方法启动 DMA 分配后调用[**WdfDmaTransactionCancel**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdmatransaction/nf-wdfdmatransaction-wdfdmatransactioncancel) ，则取消事务的尝试将失败， **WdfDmaTransactionCancel**将返回 FALSE。 在这种情况下， **WdfDmaTransactionExecute**将返回状态\_SUCCESS，驱动程序的请求处理程序必须[完成 DMA 事务](completing-a-dma-transaction.md)。

    此时，如果驱动程序使用系统模式 DMA， [*EvtRequestCancel*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nc-wdfrequest-evt_wdf_request_cancel)回调函数可能会调用[**WdfDmaTransactionStopSystemTransfer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdmatransaction/nf-wdfdmatransaction-wdfdmatransactionstopsystemtransfer)来尝试停止正在进行的系统模式 DMA 传输。 有关演示如何执行此操作的代码示例，请参阅[**WdfDmaTransactionStopSystemTransfer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdmatransaction/nf-wdfdmatransaction-wdfdmatransactionstopsystemtransfer)。

5.  [**WdfDmaTransactionExecute**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdmatransaction/nf-wdfdmatransaction-wdfdmatransactionexecute)方法完成 DMA 分配后，框架将调用驱动程序的[*EvtProgramDma*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdmatransaction/nc-wdfdmatransaction-evt_wdf_program_dma)回调函数（该函数可能会在调用**后立即在单独的线程中运行WdfDmaTransactionExecute**）。 此时，对[**WdfDmaTransactionCancel**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdmatransaction/nf-wdfdmatransaction-wdfdmatransactioncancel)方法的调用将返回 FALSE。

    在[*EvtProgramDma*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdmatransaction/nc-wdfdmatransaction-evt_wdf_program_dma)中，驱动程序可以调用[**WdfRequestUnmarkCancelable**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestunmarkcancelable)以结束可能的请求取消。 如果**WdfRequestUnmarkCancelable**返回 STATUS\_SUCCESS，则回调函数必须对硬件进行编程才能开始传输。 如果**WdfRequestUnmarkCancelable**返回状态\_"已取消"，则该请求已取消。 在这种情况下， *EvtProgramDma*必须调用[**WDFDMATRANSACTIONDMACOMPLETEDFINAL**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdmatransaction/nf-wdfdmatransaction-wdfdmatransactiondmacompletedfinal)来[完成 DMA 事务](completing-a-dma-transaction.md)。

    在已经完成若干个传输操作之后，驱动程序可以使用相同的技术来取消 DMA 事务。 在这种情况下，驱动程序会在调用[**WdfDmaTransactionDmaCompleted**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdmatransaction/nf-wdfdmatransaction-wdfdmatransactiondmacompleted)后调用[**WdfDmaTransactionCancel**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdmatransaction/nf-wdfdmatransaction-wdfdmatransactioncancel) ，但在框架调用[*EvtProgramDma*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdmatransaction/nc-wdfdmatransaction-evt_wdf_program_dma)之前，将对下一次传输操作进行编程。 如果在调用**WdfDmaTransactionDmaCompleted**之前驱动程序调用**WdfDmaTransactionCancel** ，则**WdfDmaTransactionDmaCompleted**将返回**TRUE**，指示 DMA 事务已完成。

 

 





