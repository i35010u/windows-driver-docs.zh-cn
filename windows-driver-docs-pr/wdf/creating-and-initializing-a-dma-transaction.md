---
title: 创建并初始化 DMA 事务
description: 创建并初始化 DMA 事务
ms.assetid: 1982c3fa-9e4a-4b26-8902-321223d9159f
keywords:
- DMA 事务 WDK KMDF，初始化
- DMA 操作 WDK KMDF，事务
- 主总线 DMA WDK KMDF 事务
- DMA 事务 WDK KMDF，创建
- 初始化 DMA 事务 WDK KMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ef4e5b19acb4c005e2280d2eb234969df171b0a8
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56523398"
---
# <a name="creating-and-initializing-a-dma-transaction"></a>创建并初始化 DMA 事务


\[仅适用于 KMDF\]




您的驱动程序可以将 I/O 请求发送到 DMA 设备之前，该驱动程序，必须：

1.  调用[ **WdfDmaTransactionCreate** ](https://msdn.microsoft.com/library/windows/hardware/ff547027)创建请求的 DMA 事务对象。

2.  调用[ **WdfDmaTransactionInitializeUsingRequest**](https://msdn.microsoft.com/library/windows/hardware/ff547107)， [ **WdfDmaTransactionInitialize**](https://msdn.microsoft.com/library/windows/hardware/ff547099)，或[ **WdfDmaTransactionInitializeUsingOffset** ](https://msdn.microsoft.com/library/windows/hardware/hh451182)来初始化事务对象。

通常情况下，您的驱动程序创建[DMA 事务](dma-transactions-and-dma-transfers.md)因为[请求处理程序](request-handlers.md)已收到[framework 请求对象](framework-request-objects.md)并必须将请求传递给硬件。 在这种情况下，该驱动程序应调用[ **WdfDmaTransactionInitializeUsingRequest**](https://msdn.microsoft.com/library/windows/hardware/ff547107)，它接受请求对象句柄作为输入并从请求对象中提取请求的地址参数.

如果您的驱动程序必须创建的 DMA 事务*不*根据驱动程序收到一个框架请求对象，该驱动程序可以调用[ **WdfDmaTransactionInitialize** ](https://msdn.microsoft.com/library/windows/hardware/ff547099)或[ **WdfDmaTransactionInitializeUsingOffset**](https://msdn.microsoft.com/library/windows/hardware/hh451182)。 这两种方法接受该驱动程序提供的地址参数。

所有三种初始化方法要求的地址[ *EvtProgramDma* ](https://msdn.microsoft.com/library/windows/hardware/ff541816)事件作为输入参数的回调函数。 此回调函数程序设备，和框架将调用的回调函数每次[DMA 传输](dma-transactions-and-dma-transfers.md)可用。

当您的驱动程序调用[ **WdfDmaEnablerCreate** ](https://msdn.microsoft.com/library/windows/hardware/ff546983)来创建 DMA 推动器对象，驱动程序提供[ **WDF\_DMA\_促成因素\_CONFIG** ](https://msdn.microsoft.com/library/windows/hardware/ff551290)结构，其中包含设备的最大传输长度。 该框架使用此值作为默认最大长度对所有的 DMA 传输。

对于某些类型的 DMA 事务，可能需要指定不同于设备的默认最大长度的最大传输长度。 可以使用[ **WdfDmaTransactionSetMaximumLength** ](https://msdn.microsoft.com/library/windows/hardware/ff547127)若要设置的单个事务的最大传输长度。 仅在它可以处理指定的事务时，框架将使用指定的最大传输长度。

请注意，通过数限制的最大传输长度[映射寄存器](https://msdn.microsoft.com/library/windows/hardware/ff554406)DMA 启用程序对象向操作系统提供。 若要确定可用的最大传输长度，您的驱动程序可以调用[ **WdfDmaEnablerGetFragmentLength**](https://msdn.microsoft.com/library/windows/hardware/ff546986)。 如果值的**WdfDmaEnablerGetFragmentLength**返回小于该驱动程序提供给最大传输长度[ **WdfDmaEnablerCreate**](https://msdn.microsoft.com/library/windows/hardware/ff546983)、框架使用的较小值。

您的驱动程序创建并初始化 DMA 事务后，该驱动程序必须[启动事务](starting-a-dma-transaction.md)。

 

 





