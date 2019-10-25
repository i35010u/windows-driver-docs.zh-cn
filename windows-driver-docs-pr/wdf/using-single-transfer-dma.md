---
title: 使用单一传输 DMA
description: 本主题介绍 KMDF 驱动程序如何请求单一传输 DMA。
ms.assetid: 57bf9988-6eed-42ca-a961-a6d16c5c19c1
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3c5988c3966a8d795ad2f9a6afcba1bc7fd270ed
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845438"
---
# <a name="using-single-transfer-dma"></a>使用单一传输 DMA

默认情况下，WDF 有时将单个 DMA 事务拆分为多个 DMA 传输。 但是，某些设备不能处理碎片事务，而是必须在单个 DMA 操作中接收全部数据。  例如，某些 PCI 网络控制器每次需要一个网络数据包，因为它们不具有用于缓存和重新组装部分数据的硬件。

从 KMDF 版本1.19 开始，使用 DMA v3 的 KMDF 驱动程序可以指定它需要单个传输 DMA 事务。  驱动程序只能为单个 DMA 事务指定单一传输，也可以为使用指定 DMA 启用程序创建的所有 DMA 事务指定单一传输。  

## <a name="setting-single-transfer-for-a-specific-dma-transaction"></a>为特定 DMA 事务设置单个传输

若要为单个事务设置单个传输，请使用以下顺序：

1. 调用[**WdfDmaTransactionCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdmatransaction/nf-wdfdmatransaction-wdfdmatransactioncreate)或[**WdfDmaTransactionRelease**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdmatransaction/nf-wdfdmatransaction-wdfdmatransactionrelease)。
2. 调用[**WdfDmaTransactionSetSingleTransferRequirement**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdmatransaction/nf-wdfdmatransaction-wdfdmatransactionsetsingletransferrequirement)。
3. 调用[**WdfDmaTransactionInitialize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdmatransaction/nf-wdfdmatransaction-wdfdmatransactioninitialize)。  
    如果初始化由于事务碎片而失败，驱动程序可能会导致 i/o 请求失败，或者可以重新排列事务的内存缓冲区并重新初始化事务。
4. 调用[**WdfDmaTransactionExecute**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdmatransaction/nf-wdfdmatransaction-wdfdmatransactionexecute)。

调试驱动程序时，可以使用[ **！ wdfdmatransaction**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdfdmatransaction)扩展来确定是否为给定的 transaction 对象设置了单一传输 wdfkd。

## <a name="setting-the-single-transfer-requirement-for-all-dma-transactions-created-with-a-particular-dma-enabler"></a>为使用特定 DMA 启用程序创建的所有 DMA 事务设置单一传输要求

若要为使用给定启用程序创建的所有事务设置单个传输，请在调用[**WdfDmaEnablerCreate**](https://docs.microsoft.com/previous-versions/jj619276(v=technet.10))时，在[**WDF_DMA_ENABLER_CONFIG_FLAGS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdmaenabler/ne-wdfdmaenabler-_wdf_dma_enabler_config_flags)中指定**WDF_DMA_ENABLER_CONFIG_REQUIRE_SINGLE_TRANSFER**标志。  

使用此标志的驱动程序不需要在每次创建或重新使用事务对象时调用[**WdfDmaTransactionSetSingleTransferRequirement**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdmatransaction/nf-wdfdmatransaction-wdfdmatransactionsetsingletransferrequirement) 。

如果驱动程序[重用事务对象](reusing-dma-transaction-objects.md)，此设置也会保留。

调试时，请使用[ **！ wdfkd. wdfdmaenabler**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdfdmaenabler)扩展来确定是否为给定 DMA 启用程序对象设置了单个传输。

有关 WDF 调用驱动程序的 DMA 事件回调函数的顺序的信息，请参阅[在 KMDF 驱动程序中处理 I/o 请求，获取总线主控计算机 DMA 设备](handling-i-o-requests-in-a-kmdf-driver-for-a-bus-master-dma-device.md)。
