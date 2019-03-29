---
title: 重复使用 DMA 事务对象
description: 重复使用 DMA 事务对象
ms.assetid: 4adb8653-48b6-4e22-aba3-b909c95b8d15
keywords:
- DMA 事务 WDK KMDF，重用事务对象
- DMA 操作 WDK KMDF，事务
- 主总线 DMA WDK KMDF 事务
- 重复使用 DMA 事务对象 WDK KMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9d1192296f31c275ac4552498e99f3120a77579d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56567905"
---
# <a name="reusing-dma-transaction-objects"></a>重复使用 DMA 事务对象


\[仅适用于 KMDF\]




驱动程序处理所有与 DMA 事务相关联的 DMA 传输后，该驱动程序可以删除或重复使用的事务对象。 通常情况下，驱动程序[ *EvtInterruptDpc* ](https://msdn.microsoft.com/library/windows/hardware/ff541721)回调函数将删除的事务对象 (通过调用[ **WdfObjectDelete** ](https://msdn.microsoft.com/library/windows/hardware/ff548734)). 随后，当驱动程序创建新的 DMA 事务，它将调用[ **WdfDmaTransactionCreate** ](https://msdn.microsoft.com/library/windows/hardware/ff547027)以创建新的事务对象。

但是，有时是有益的驱动程序以重新使用事务对象。 在这种情况下，该驱动程序将调用[ **WdfDmaTransactionRelease** ](https://msdn.microsoft.com/library/windows/hardware/ff547114)而不是[ **WdfObjectDelete**](https://msdn.microsoft.com/library/windows/hardware/ff548734)。

例如，假设您的驱动程序和设备必须运行在计算机内存资源较低。 若要处理此内存问题，您的驱动程序可以使用以下过程：

1.  在驱动程序[ *EvtDriverDeviceAdd* ](https://msdn.microsoft.com/library/windows/hardware/ff541693)回调函数可以调用[ **WdfDmaTransactionCreate** ](https://msdn.microsoft.com/library/windows/hardware/ff547027)若要创建一个或多个事务对象。 该驱动程序将保存到这些事务对象的句柄。

2.  它将调用该驱动程序已准备好创建和初始化一个新的事务，每次[ **WdfDmaTransactionCreate**](https://msdn.microsoft.com/library/windows/hardware/ff547027)。 如果此方法返回状态\_不足\_资源，该驱动程序可以使用存储的事务对象之一。

3.  如果驱动程序使用的一个存储的事务对象，它应重复使用的事务对象，而不是删除它，当事务完成。 该驱动程序设置以便重复使用的事务对象通过调用[ **WdfDmaTransactionRelease** ](https://msdn.microsoft.com/library/windows/hardware/ff547114)而不是[ **WdfObjectDelete**](https://msdn.microsoft.com/library/windows/hardware/ff548734)。

[PLX9x5x](sample-kmdf-drivers.md)示例重复使用 DMA 事务对象。

 

 





