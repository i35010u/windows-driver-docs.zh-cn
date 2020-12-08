---
title: 启动 DMA 事务
description: 启动 DMA 事务
keywords:
- DMA 事务 WDK KMDF，开始
- DMA 操作 WDK KMDF，事务
- 总线主控 DMA WDK KMDF，事务
- 启动 DMA 事务 WDK KMDF
- 散播/聚集 DMA WDK KMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7406d50df24ebeaa0ee4387c34c257bb12cee816
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96821133"
---
# <a name="starting-a-dma-transaction"></a>启动 DMA 事务


\[仅适用于 KMDF\]




在您的驱动程序 [创建并初始化 DMA 事务](creating-and-initializing-a-dma-transaction.md)之后，驱动程序可以调用 [**WdfDmaTransactionExecute**](/windows-hardware/drivers/ddi/wdfdmatransaction/nf-wdfdmatransaction-wdfdmatransactionexecute) 方法来启动该事务。 此方法为与事务关联的第一个 [DMA 传输](dma-transactions-and-dma-transfers.md) 生成一个散点/集合列表。 接下来，该方法调用为事务注册的驱动程序的 [*EvtProgramDma*](/windows-hardware/drivers/ddi/wdfdmatransaction/nc-wdfdmatransaction-evt_wdf_program_dma) 回调函数。 回调函数会 [程序 DMA 硬件](programming-dma-hardware.md) 开始传输。

在您的驱动程序调用 **WdfDmaTransactionExecute** 之前，驱动程序必须存储 DMA 事务句柄，以便以后当驱动程序完成与该事务关联的每个 DMA 传输时可以检索该句柄。 存储事务句柄的好位置是框架对象的上下文内存，通常是设备的框架设备对象。 有关使用对象上下文内存的详细信息，请参阅 [框架对象上下文空间](framework-object-context-space.md)。

[PLX9x5x](/samples/browse/)示例中的以下代码示例演示如何初始化并执行 DMA 事务。 此代码将出现在 *Read .c* 文件中。

```cpp
VOID PLxEvtIoRead(
    IN WDFQUEUE         Queue,
    IN WDFREQUEST       Request,
    IN size_t           Length
    )
{
    NTSTATUS            status = STATUS_UNSUCCESSFUL;
    PDEVICE_EXTENSION   devExt;
    // Get the DevExt from the queue handle
    devExt = PLxGetDeviceContext(WdfIoQueueGetDevice(Queue));
    do {
        // Validate the Length parameter.
        if (Length > PCI9656_SRAM_SIZE)  {
            status = STATUS_INVALID_BUFFER_SIZE;
            break;
        }
        // Initialize the DmaTransaction.
        status = 
           WdfDmaTransactionInitializeUsingRequest(
                 devExt->ReadDmaTransaction,
                 Request, 
                 PLxEvtProgramReadDma, 
                 WdfDmaDirectionReadFromDevice 
           );
        if(!NT_SUCCESS(status)) {
            . . . //Error-handling code omitted
            break; 
        }
        // Execute this DmaTransaction.
        status = WdfDmaTransactionExecute( devExt->ReadDmaTransaction, 
                                           WDF_NO_CONTEXT);
        if(!NT_SUCCESS(status)) {
            . . . //Error-handling code omitted
            break; 
        }
        // Indicate that the DMA transaction started successfully.
        // The DPC routine will complete the request when the DMA
        // transaction is complete.
        status = STATUS_SUCCESS;
    } while (0);
    // If there are errors, clean up and complete the request.
    if (!NT_SUCCESS(status )) {
        WdfDmaTransactionRelease(devExt->ReadDmaTransaction); 
        WdfRequestComplete(Request, status);
    }
    return;
}
```
