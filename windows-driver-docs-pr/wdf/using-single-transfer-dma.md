---
title: 使用单一传输 DMA
description: 本主题介绍如何 KMDF 驱动程序请求一个传输 DMA。
ms.assetid: 57bf9988-6eed-42ca-a961-a6d16c5c19c1
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5b239f22e5340a5fefb30964005577e4017c604c
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67372209"
---
# <a name="using-single-transfer-dma"></a>使用单一传输 DMA

默认情况下，WDF 有时会将多个 DMA 传输到单个 DMA 事务。 但是，某些设备无法处理分片的事务，而是必须在单个操作中 DMA 接收的所有数据。  例如，一些 PCI 网络控制器需要一个网络数据包一次因为他们没有硬件缓存，并重组部分数据。

V3 KMDF 版本 1.19，从开始使用 DMA KMDF 驱动程序可以指定它需要单一传输 DMA 事务。  驱动程序可以指定单个 DMA 事务仅为单个传输或者它可以指定单个传输所有 DMA 创建的事务使用指定的 DMA 促成因素。  

## <a name="setting-single-transfer-for-a-specific-dma-transaction"></a>设置单个传输特定的 DMA 事务

若要设置单个事务的单个传输，请按以下顺序：

1. 调用[ **WdfDmaTransactionCreate** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdmatransaction/nf-wdfdmatransaction-wdfdmatransactioncreate)或[ **WdfDmaTransactionRelease**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdmatransaction/nf-wdfdmatransaction-wdfdmatransactionrelease)。
2. 调用[ **WdfDmaTransactionSetSingleTransferRequirement**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdmatransaction/nf-wdfdmatransaction-wdfdmatransactionsetsingletransferrequirement)。
3. 调用[ **WdfDmaTransactionInitialize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdmatransaction/nf-wdfdmatransaction-wdfdmatransactioninitialize)。  
    如果初始化失败由于事务碎片，驱动程序可能会失败的 I/O 请求也可以重新排列该事务的内存缓冲区并重新初始化该事务。
4. 调用[ **WdfDmaTransactionExecute**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdmatransaction/nf-wdfdmatransaction-wdfdmatransactionexecute)。

在调试您的驱动程序时，可以使用[ **！ wdfkd.wdfdmatransaction** ](https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdfdmatransaction)扩展来确定给定的事务对象是否设置了单一的传输。

## <a name="setting-the-single-transfer-requirement-for-all-dma-transactions-created-with-a-particular-dma-enabler"></a>设置使用特定的 DMA 启用程序创建的所有 DMA 事务的单传输要求

若要设置单个传输所有创建的事务与给定的促成因素，指定**WDF_DMA_ENABLER_CONFIG_REQUIRE_SINGLE_TRANSFER**中的标志[ **WDF_DMA_ENABLER_CONFIG_FLAGS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdmaenabler/ne-wdfdmaenabler-_wdf_dma_enabler_config_flags)调用时[ **WdfDmaEnablerCreate**](https://docs.microsoft.com/previous-versions/jj619276(v=technet.10))。  

使用此标志的驱动程序不需要调用[ **WdfDmaTransactionSetSingleTransferRequirement** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdmatransaction/nf-wdfdmatransaction-wdfdmatransactionsetsingletransferrequirement)每次创建或重新使用的事务对象。

如果此设置也仍然存在驱动程序[重复使用的事务对象](reusing-dma-transaction-objects.md)。

调试时，使用[ **！ wdfkd.wdfdmaenabler** ](https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdfdmaenabler)扩展来确定对于给定的 DMA 推动器对象是否设置了单一的传输。

有关在其中 WDF 调用您的驱动程序 DMA 事件回调函数的顺序的信息，请参阅[总线 Master DMA 设备 KMDF 驱动程序中处理 I/O 请求](handling-i-o-requests-in-a-kmdf-driver-for-a-bus-master-dma-device.md)。
