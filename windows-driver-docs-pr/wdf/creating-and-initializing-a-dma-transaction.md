---
title: 创建并初始化 DMA 事务
description: 创建并初始化 DMA 事务
ms.assetid: 1982c3fa-9e4a-4b26-8902-321223d9159f
keywords:
- DMA 事务 WDK KMDF，初始化
- DMA 操作 WDK KMDF，事务
- 总线主控 DMA WDK KMDF，事务
- DMA 事务 WDK KMDF，创建
- 初始化 DMA 事务 WDK KMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 034ea43bae1ea671486518355782cb4458315689
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89193111"
---
# <a name="creating-and-initializing-a-dma-transaction"></a>创建并初始化 DMA 事务


\[仅适用于 KMDF\]




在您的驱动程序可以向 DMA 设备发送 i/o 请求之前，驱动程序必须：

1.  调用 [**WdfDmaTransactionCreate**](/windows-hardware/drivers/ddi/wdfdmatransaction/nf-wdfdmatransaction-wdfdmatransactioncreate) 为请求创建 DMA 事务对象。

2.  调用 [**WdfDmaTransactionInitializeUsingRequest**](/windows-hardware/drivers/ddi/wdfdmatransaction/nf-wdfdmatransaction-wdfdmatransactioninitializeusingrequest)、 [**WdfDmaTransactionInitialize**](/windows-hardware/drivers/ddi/wdfdmatransaction/nf-wdfdmatransaction-wdfdmatransactioninitialize)或 [**WdfDmaTransactionInitializeUsingOffset**](/windows-hardware/drivers/ddi/wdfdmatransaction/nf-wdfdmatransaction-wdfdmatransactioninitializeusingoffset) 以初始化事务对象。

通常，驱动程序会创建 [DMA 事务](dma-transactions-and-dma-transfers.md) ，因为 [请求处理程序](request-handlers.md) 已收到 [框架请求对象](framework-request-objects.md) 并且必须将该请求传递到硬件。 在这种情况下，驱动程序应调用 [**WdfDmaTransactionInitializeUsingRequest**](/windows-hardware/drivers/ddi/wdfdmatransaction/nf-wdfdmatransaction-wdfdmatransactioninitializeusingrequest)，它接受请求对象句柄作为输入，并从 request 对象中提取请求的地址参数。

如果驱动程序必须创建 *不* 基于驱动程序收到的框架请求对象的 DMA 事务，则驱动程序可以调用 [**WdfDmaTransactionInitialize**](/windows-hardware/drivers/ddi/wdfdmatransaction/nf-wdfdmatransaction-wdfdmatransactioninitialize) 或 [**WdfDmaTransactionInitializeUsingOffset**](/windows-hardware/drivers/ddi/wdfdmatransaction/nf-wdfdmatransaction-wdfdmatransactioninitializeusingoffset)。 这两种方法都接受驱动程序提供的地址参数。

所有三个初始化方法都需要 [*EvtProgramDma*](/windows-hardware/drivers/ddi/wdfdmatransaction/nc-wdfdmatransaction-evt_wdf_program_dma) 事件回调函数的地址作为输入参数。 此回调函数在每次提供 [DMA 传输](dma-transactions-and-dma-transfers.md) 时，对设备和框架调用回调函数。

当驱动程序调用 [**WdfDmaEnablerCreate**](/windows-hardware/drivers/ddi/wdfdmaenabler/nf-wdfdmaenabler-wdfdmaenablercreate) 来创建 DMA 启用码对象时，驱动程序会提供一个 [**WDF \_ DMA \_ 启用码 \_ 配置**](/windows-hardware/drivers/ddi/wdfdmaenabler/ns-wdfdmaenabler-_wdf_dma_enabler_config) 结构，其中包含设备的最大传输长度。 框架使用此值作为所有 DMA 传输的默认最大长度。

对于某些类型的 DMA 事务，你可能需要指定与设备的默认最大长度不同的最大传输长度。 可以使用 [**WdfDmaTransactionSetMaximumLength**](/windows-hardware/drivers/ddi/wdfdmatransaction/nf-wdfdmatransaction-wdfdmatransactionsetmaximumlength) 设置单个事务的最大传输长度。 框架仅在处理指定的事务时使用指定的最大传输长度。

请注意，最大传输长度受操作系统为 DMA 启用程序对象提供的 [映射寄存器](../kernel/map-registers.md) 数量的限制。 若要确定可用的最大传输长度，驱动程序可以调用 [**WdfDmaEnablerGetFragmentLength**](/windows-hardware/drivers/ddi/wdfdmaenabler/nf-wdfdmaenabler-wdfdmaenablergetfragmentlength)。 如果 **WdfDmaEnablerGetFragmentLength** 返回的值小于驱动程序提供给 [**WdfDmaEnablerCreate**](/windows-hardware/drivers/ddi/wdfdmaenabler/nf-wdfdmaenabler-wdfdmaenablercreate)的最大传输长度，则框架将使用较小的值。

在您的驱动程序创建并初始化 DMA 事务之后，驱动程序必须 [启动该事务](starting-a-dma-transaction.md)。

 

