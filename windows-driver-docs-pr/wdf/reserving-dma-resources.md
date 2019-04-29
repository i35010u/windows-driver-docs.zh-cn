---
title: 保留 DMA 资源
description: 保留 DMA 资源
ms.assetid: 8C5FF779-8D54-47D9-8EC6-7D4921F8F697
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d76698c0c8b89b907354e1f06bb30730d277d8fb
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63325171"
---
# <a name="reserving-dma-resources"></a>保留 DMA 资源


\[仅适用于 KMDF\]

通常情况下，基于框架的驱动程序不会保留提前映射寄存器。 但是，在某些情况下，驱动程序可能需要提前保留这些资源。

基于框架的驱动程序运行在 Windows 8 或更高版本可以为指定的数据包或系统配置文件的 DMA 启用码保留指定的数目的映射寄存器。 若要执行此操作，驱动程序调用[ **WdfDmaTransactionAllocateResources** ](https://msdn.microsoft.com/library/windows/hardware/hh451123) ，并将注册[ *EvtReserveDma* ](https://msdn.microsoft.com/library/windows/hardware/hh406425)回调函数。

框架将调用的驱动程序[ *EvtReserveDma* ](https://msdn.microsoft.com/library/windows/hardware/hh406425)函数时它已经预留映射寄存器和 WDM DMA 适配器的锁。 该驱动程序然后可以初始化并启动多个时间最后释放事务对象前使用相同的事务对象的事务。 若要释放 DMA 资源返回到系统中，驱动程序调用[ **WdfDmaTransactionFreeResources**](https://msdn.microsoft.com/library/windows/hardware/hh451177)。

若要确定所需的事务的映射寄存器编号，该驱动程序可以调用[ **WdfDmaTransactionGetTransferInfo** ](https://msdn.microsoft.com/library/windows/hardware/hh451179)之前调用[ **WdfDmaTransactionAllocateResources**](https://msdn.microsoft.com/library/windows/hardware/hh451123)。 该驱动程序必须初始化之前调用事务**WdfDmaTransactionGetTransferInfo**。

以下步骤演示如何将驱动程序可以保留和发布与指定的事务的独占使用 DMA 促成因素：

1.  该驱动程序接收的 I/O 请求。

2.  在驱动程序[请求处理程序](request-handlers.md)调用[ **WdfDmaTransactionCreate** ](https://msdn.microsoft.com/library/windows/hardware/ff547027)创建请求的 DMA 事务对象。

3.  在驱动程序[请求处理程序](request-handlers.md)调用[ **WdfDmaTransactionAllocateResources** ](https://msdn.microsoft.com/library/windows/hardware/hh451123)预留资源。

4.  框架将调用[ *EvtReserveDma* ](https://msdn.microsoft.com/library/windows/hardware/hh406425)时它是否有保留的请求的资源。

5.  在中[ *EvtReserveDma*](https://msdn.microsoft.com/library/windows/hardware/hh406425)，驱动程序调用[ **WdfDmaTransactionInitializeUsingRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff547107)或[ **WdfDmaTransactionInitialize** ](https://msdn.microsoft.com/library/windows/hardware/ff547099)来初始化事务对象。

6.  在中[ *EvtReserveDma*](https://msdn.microsoft.com/library/windows/hardware/hh406425)，驱动程序调用[ **WdfDmaTransactionExecute** ](https://msdn.microsoft.com/library/windows/hardware/ff547062)方法来启动事务。 由于该事务已保留资源，框架将立即调用的驱动程序[ *EvtProgramDma* ](https://msdn.microsoft.com/library/windows/hardware/ff541816)回调函数。

7.  从[ *EvtInterruptDpc* ](https://msdn.microsoft.com/library/windows/hardware/ff541721)或[ *EvtDmaTransactionDmaTransferComplete*](https://msdn.microsoft.com/library/windows/hardware/hh406418)，驱动程序调用[ **WdfDmaTransactionDmaCompleted**](https://msdn.microsoft.com/library/windows/hardware/ff547039)， [ **WdfDmaTransactionDmaCompletedWithLength**](https://msdn.microsoft.com/library/windows/hardware/ff547052)，或[ **WdfDmaTransactionDmaCompletedFinal**](https://msdn.microsoft.com/library/windows/hardware/ff547049)后, 跟[ **WdfObjectDelete** ](https://msdn.microsoft.com/library/windows/hardware/ff548734)或者[ **WdfDmaTransactionRelease**](https://msdn.microsoft.com/library/windows/hardware/ff547114). 该驱动程序必须删除或释放事务，直到该事务已完成或已取消。 在此步骤完成时后, 继续保留映射寄存器。

8.  该驱动程序可以重复步骤 5 – 7 为根据需要多次。

    当驱动程序不再需要时保留时，驱动程序调用[ **WdfDmaTransactionFreeResources** ](https://msdn.microsoft.com/library/windows/hardware/hh451177)从[ *EvtInterruptDpc* ](https://msdn.microsoft.com/library/windows/hardware/ff541721)或[ *EvtDmaTransactionDmaTransferComplete*](https://msdn.microsoft.com/library/windows/hardware/hh406418)。 或者，驱动程序可以调用**WdfDmaTransactionFreeResources**从其[ *EvtReserveDma* ](https://msdn.microsoft.com/library/windows/hardware/hh406425)事件回调函数。

 

 





