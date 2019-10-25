---
title: 完成 DMA 传输
description: 完成 DMA 传输
ms.assetid: 86383b9f-9b82-4afa-81ac-2ab09bd8778b
keywords:
- DMA 操作 WDK KMDF，传输
- 总线主控 DMA WDK KMDF，传输
- DMA 传输 WDK KMDF，正在完成
- 完成 DMA 传输 WDK KMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1646d0ab87170f3222adebb45a062ccadff51f58
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844609"
---
# <a name="completing-a-dma-transfer"></a>完成 DMA 传输


\[仅适用于 KMDF\]




通常，驱动程序的[*EvtInterruptDpc*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_dpc)回调函数完成每个 DMA 传输的处理。

首先，因为多个 DMA 事务可以同时进行，所以[*EvtInterruptDpc*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_dpc)回调函数必须确定完成的传输与哪个 dma 事务相关联。 回调函数可以通过检索驱动程序[启动 DMA 事务](starting-a-dma-transaction.md)时存储的事务句柄来实现此目的。 若要检索设备扩展， [PLX9x5x](https://go.microsoft.com/fwlink/p/?linkid=256157)示例在其 Private .h 头文件中定义了一个名为**PLxGetDeviceContext**的函数：

```cpp
WDF_DECLARE_CONTEXT_TYPE_WITH_NAME(DEVICE_EXTENSION, PLxGetDeviceContext)
```

然后，在驱动程序的[*EvtInterruptDpc*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_dpc)回调中执行以下操作：

```cpp
WDFDMATRANSACTION   dmaTransaction;
PDEVICE_EXTENSION   devExt;
...
devExt  = PLxGetDeviceContext(WdfInterruptGetDevice(Interrupt));
...
dmaTransaction = devExt->WriteDmaTransaction;
```

接下来， [*EvtInterruptDpc*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_dpc)回调函数必须通过调用下列传输完成方法之一，通知框架传输已完成：

-   [**WdfDmaTransactionDmaCompleted**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdmatransaction/nf-wdfdmatransaction-wdfdmatransactiondmacompleted)，如果传输已成功完成，并且硬件未报告传输的字节数。

-   [**WdfDmaTransactionDmaCompletedWithLength**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdmatransaction/nf-wdfdmatransaction-wdfdmatransactiondmacompletedwithlength)，如果传输已成功完成，并且硬件报告传输的字节数（或未传输的字节数），或驱动程序检测到错误并指定的传输计数为0到重试传输。 如果驱动程序指定的传输计数为零，则框架将从剩余的字节数中减去零，从而将同一传输发送到[*EvtProgramDma*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdmatransaction/nc-wdfdmatransaction-evt_wdf_program_dma)回调函数。

-   如果硬件报告不足或失败的情况，则为[**WdfDmaTransactionDmaCompletedFinal**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdmatransaction/nf-wdfdmatransaction-wdfdmatransactiondmacompletedfinal)。

你的驱动程序可以调用[**WdfDmaTransactionGetCurrentDmaTransferLength**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdmatransaction/nf-wdfdmatransaction-wdfdmatransactiongetcurrentdmatransferlength)来获取已完成传输的原始长度。 如果设备报告未传输的字节数，则此调用非常有用，因为驱动程序可以将未传输的字节数减去原始传输长度，然后将**WdfDmaTransactionGetCurrentDmaTransferLength**调用到报告实际传输大小。

前面的每个传输完成方法都通知框架单个[DMA 传输](dma-transactions-and-dma-transfers.md)（而非整个[dma 事务](dma-transactions-and-dma-transfers.md)）已完成。 驱动程序调用这些方法之一后，驱动程序将检查该方法的返回值，以查看该事务是否需要更多的传输：

-   如果完成方法的返回值为**FALSE**，则框架确定需要其他 DMA 传输来完成对 dma 事务的处理。

    通常，驱动程序的[*EvtInterruptDpc*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_dpc)回调函数将返回。 该框架将再次调用驱动程序的[*EvtProgramDma*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdmatransaction/nc-wdfdmatransaction-evt_wdf_program_dma)回调函数，并且回调函数可以对硬件进行编程以进行下一次传输。

    传输完成方法提供状态值，该值始终为状态\_更\_处理\_此情况下需要此值。

-   如果返回值为**TRUE**，则不会对 DMA 事务进行更多的传输。

    传输完成方法提供状态值。 如果 status 值为 STATUS\_SUCCESS，则 DMA 事务的所有传输将完成，并且驱动程序必须[完成 dma 事务](completing-a-dma-transaction.md)。 如果 status 值为其他任何值，则会出现错误，并且 DMA 事务可能尚未完成。

如果[*EvtInterruptDpc*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_dpc)回调函数检测到错误，通常是由于计时器过期或硬件中断发出传输错误，驱动程序可以重新启动事务的当前传输。

若要重新启动事务的当前传输，驱动程序的[*EvtInterruptDpc*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_dpc)回调函数可以调用[**WdfDmaTransactionDmaCompletedWithLength**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdmatransaction/nf-wdfdmatransaction-wdfdmatransactiondmacompletedwithlength) ，并将*TransferredLength*参数设置为零。

 

 





