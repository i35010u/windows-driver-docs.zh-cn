---
title: 重复使用 DMA 事务对象
description: 重复使用 DMA 事务对象
ms.assetid: 4adb8653-48b6-4e22-aba3-b909c95b8d15
keywords:
- DMA 事务 WDK KMDF，重复使用事务对象
- DMA 操作 WDK KMDF，事务
- 总线主控 DMA WDK KMDF，事务
- 重复使用 DMA 事务对象 WDK KMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e8bdff06d4317661c744770551a642ec86299b60
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842225"
---
# <a name="reusing-dma-transaction-objects"></a>重复使用 DMA 事务对象


\[仅适用于 KMDF\]




驱动程序处理与 DMA 事务关联的所有 DMA 传输后，该驱动程序可以删除或重用该事务对象。 通常，驱动程序的[*EvtInterruptDpc*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_dpc)回调函数会删除 transaction 对象（通过调用[**WdfObjectDelete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfobject/nf-wdfobject-wdfobjectdelete)）。 随后，当驱动程序创建新的 DMA 事务时，它将调用[**WdfDmaTransactionCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdmatransaction/nf-wdfdmatransaction-wdfdmatransactioncreate)来创建新的 transaction 对象。

但是，有时驱动程序重用事务对象是有益的。 在这种情况下，驱动程序将调用[**WdfDmaTransactionRelease**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdmatransaction/nf-wdfdmatransaction-wdfdmatransactionrelease)而不是[**WdfObjectDelete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfobject/nf-wdfobject-wdfobjectdelete)。

例如，假设您的驱动程序和设备必须在计算机内存资源较低时运行。 若要处理此内存问题，你的驱动程序可以使用以下过程：

1.  驱动程序的[*EvtDriverDeviceAdd*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)回调函数可以调用[**WdfDmaTransactionCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdmatransaction/nf-wdfdmatransaction-wdfdmatransactioncreate)来创建一个或多个事务对象。 驱动程序将句柄保存到这些事务对象。

2.  每次驱动程序准备好创建并初始化新的事务时，它都会调用[**WdfDmaTransactionCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdmatransaction/nf-wdfdmatransaction-wdfdmatransactioncreate)。 如果此方法返回状态\_\_资源不足，则驱动程序可以使用其中一个存储的事务对象。

3.  如果驱动程序使用其存储的事务对象之一，则应在事务完成后重新使用事务对象，而不是将其删除。 驱动程序通过调用[**WdfDmaTransactionRelease**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdmatransaction/nf-wdfdmatransaction-wdfdmatransactionrelease)而不是[**WdfObjectDelete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfobject/nf-wdfobject-wdfobjectdelete)，为重复使用设置事务对象。

[PLX9x5x](sample-kmdf-drivers.md)示例重用 DMA 事务对象。

 

 





