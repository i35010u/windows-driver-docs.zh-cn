---
title: 正在启动 DMA 事务
description: 正在启动 DMA 事务
ms.assetid: fa26ef08-01c0-4502-9cb3-865000242e4a
keywords:
- DMA 事务 WDK KMDF，启动
- DMA 操作 WDK KMDF，事务
- 主总线 DMA WDK KMDF 事务
- 启动 DMA 事务 WDK KMDF
- 散播-聚集 DMA WDK KMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 68c7a60344d3a9f86d034b679d9b10fb04f87cea
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56547827"
---
# <a name="starting-a-dma-transaction"></a>正在启动 DMA 事务


\[仅适用于 KMDF\]




您的驱动程序后[创建并初始化 DMA 事务](creating-and-initializing-a-dma-transaction.md)，该驱动程序可以调用[ **WdfDmaTransactionExecute** ](https://msdn.microsoft.com/library/windows/hardware/ff547062)方法来启动事务。 此方法生成散播-聚集列表的前[DMA 传输](dma-transactions-and-dma-transfers.md)与事务相关联。 接下来，该方法会调用[ *EvtProgramDma* ](https://msdn.microsoft.com/library/windows/hardware/ff541816)驱动程序的事务已注册的回调函数。 回调函数[程序 DMA 硬件](programming-dma-hardware.md)启动传输。

之前驱动程序调用**WdfDmaTransactionExecute**，驱动程序必须存储 DMA 事务句柄，以便其在驱动程序完成与事务相关联的每个 DMA 传输时可以更高版本进行检索。 存储事务句柄的好时机是在 framework 对象，通常在设备的 framework 设备对象的上下文内存中。 有关使用对象上下文内存的详细信息，请参阅[框架对象上下文空间](framework-object-context-space.md)。

下面的代码示例摘自[PLX9x5x](https://go.microsoft.com/fwlink/p/?linkid=256157)示例演示如何初始化并执行 DMA 事务。 此代码中出现*Read.c*文件。

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









