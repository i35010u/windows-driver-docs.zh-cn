---
title: 完成 DMA 传输
description: 完成 DMA 传输
ms.assetid: 86383b9f-9b82-4afa-81ac-2ab09bd8778b
keywords:
- DMA 操作 WDK KMDF 传输
- 主总线 DMA WDK KMDF 传输
- DMA 传输 WDK KMDF，完成
- 完成 DMA 传输 WDK KMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8a81150c78514ea0ad46487480120fce46d6add9
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67382890"
---
# <a name="completing-a-dma-transfer"></a>完成 DMA 传输


\[仅适用于 KMDF\]




通常情况下，您的驱动程序的[ *EvtInterruptDpc* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_dpc)回调函数完成的每个 DMA 传输处理。

第一个，因为多个 DMA 事务可以是正在进行中同时[ *EvtInterruptDpc* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_dpc)回调函数必须确定哪个 DMA 事务已完成的传输是与相关联。 回调函数可以执行此操作通过检索驱动程序存储时的事务句柄它[启动 DMA 事务](starting-a-dma-transaction.md)。 若要检索的设备扩展[PLX9x5x](https://go.microsoft.com/fwlink/p/?linkid=256157)示例定义一个名为函数**PLxGetDeviceContext** Private.h 标头文件中：

```cpp
WDF_DECLARE_CONTEXT_TYPE_WITH_NAME(DEVICE_EXTENSION, PLxGetDeviceContext)
```

然后，在驱动程序的[ *EvtInterruptDpc* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_dpc)回调中，执行以下操作：

```cpp
WDFDMATRANSACTION   dmaTransaction;
PDEVICE_EXTENSION   devExt;
...
devExt  = PLxGetDeviceContext(WdfInterruptGetDevice(Interrupt));
...
dmaTransaction = devExt->WriteDmaTransaction;
```

下一步， [ *EvtInterruptDpc* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_dpc)回调函数必须告知框架，已完成传输，通过调用以下传输完成方法之一：

-   [**WdfDmaTransactionDmaCompleted**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdmatransaction/nf-wdfdmatransaction-wdfdmatransactiondmacompleted)，如果已成功完成的传输和硬件不会报告传输的字节数的计数。

-   [**WdfDmaTransactionDmaCompletedWithLength**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdmatransaction/nf-wdfdmatransaction-wdfdmatransactiondmacompletedwithlength)，如果已成功完成的传输和硬件报告计数的传输的字节数 （或不传输的字节数的计数），或如果该驱动程序检测到错误，并指定传输计数为零，则重试传输。 如果该驱动程序指定传输计数为零，框架中减去从保持并因此将发送到的同一个传输的字节数为零[ *EvtProgramDma* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdmatransaction/nc-wdfdmatransaction-evt_wdf_program_dma)回调函数。

-   [**WdfDmaTransactionDmaCompletedFinal**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdmatransaction/nf-wdfdmatransaction-wdfdmatransactiondmacompletedfinal)，如果硬件报告不足或失败条件。

您的驱动程序可以调用[ **WdfDmaTransactionGetCurrentDmaTransferLength** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdmatransaction/nf-wdfdmatransaction-wdfdmatransactiongetcurrentdmatransferlength)若要获取已完成传输原始长度。 此调用是你的设备将报告不传输的字节数的情况下很有用，因为该驱动程序可以减少非传输数量从原始字节传输长度，然后调用**WdfDmaTransactionGetCurrentDmaTransferLength**报告实际传输大小。

每个前面的传输完成方法会通知框架的单个[DMA 传输](dma-transactions-and-dma-transfers.md)(不是全部[DMA 事务](dma-transactions-and-dma-transfers.md)) 完成。 您的驱动程序调用下列方法之一后，该驱动程序将检查方法的返回值来确定事务是否需要更多传输：

-   如果完成方法的返回值是**FALSE**，该框架已确定其他 DMA 传输所需完成的处理的 DMA 事务。

    通常情况下，驱动程序[ *EvtInterruptDpc* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_dpc)回调函数只返回。 框架将调用的驱动程序[ *EvtProgramDma* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdmatransaction/nc-wdfdmatransaction-evt_wdf_program_dma)同样，回调函数和回调函数可以进行下一步传输程序硬件。

    传输完成方法提供了一个状态的值，该值始终是状态\_更多\_处理\_这种情况下需要。

-   如果返回值是 **，则返回 TRUE**、 没有更多传输，则 DMA 事务会发生。

    传输完成方法提供状态的值。 如果状态值为状态\_成功，DMA 事务的所有传输都已完成，该驱动程序必须[完成 DMA 事务](completing-a-dma-transaction.md)。 如果任何其他操作的状态值，出现错误，DMA 事务可能未完成。

如果[ *EvtInterruptDpc* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_dpc)回调函数检测到错误，通常由于计时器过期或信号传输错误的硬件中断，该驱动程序可以重新启动该事务的当前传输。

若要重新启动该事务的当前传输，该驱动程序的[ *EvtInterruptDpc* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_dpc)回调函数可以调用[ **WdfDmaTransactionDmaCompletedWithLength**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdmatransaction/nf-wdfdmatransaction-wdfdmatransactiondmacompletedwithlength)与*TransferredLength*参数设置为零。

 

 





