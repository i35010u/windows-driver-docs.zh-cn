---
title: 处理重叠的 I/O 操作
description: 处理重叠的 I/O 操作
ms.assetid: d13a9fa2-9f68-4c35-af79-dd3f8cec2805
keywords:
- 延迟的过程调用 WDK 内核
- Dpc WDK 内核
- DpcForIsr
- CustomDpc
- 重叠 i/o WDK 内核
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0472de766928ce711d81b98c2731281621e4c2df
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838657"
---
# <a name="handling-overlapped-io-operations"></a>处理重叠的 I/O 操作





与设备上的操作重叠的驱动程序的[*DpcForIsr*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-io_dpc_routine)或[*CustomDpc*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-kdeferred_routine)例程不能依赖于[*StartIo*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_startio)例程的请求输入与 ISR 对[**IoRequestDpc**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iorequestdpc)的调用或[**KeInsertQueueDpc**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-keinsertqueuedpc)。 此类驱动程序的*DpcForIsr*或*CustomDpc*不一定要使用指向 irp 和 ISR 提供的上下文的输入指针，或目标设备对象中的**CURRENTIRP**指针来仅完成 irp。

在任意给定时刻，同一个 DPC 对象不能排队两次。 如果某个 ISR 多次调用**IoRequestDpc**或**KeInsertQueueDpc** ，则在执行相应的*DpcForIsr*或*CustomDpc*之前，仅当处理器上的 IRQL 低于\_级别时，DPC 例程才会运行一次。 另一方面，如果 ISR 调用**IoRequestDpc**或**KeInsertQueueDpc** ，而相应的*DpcForIsr*或*CustomDpc*在其他处理器上运行，则 DPC 例程可以同时在两个处理器上运行。

因此，在其设备上与中断驱动的 i/o 操作重叠的任何驱动程序必须具有以下各项：

-   一个*DpcForIsr*或*CustomDpc*例程，每次调用时都可以完成某个驱动程序维护的未处理请求计数

-   永远不会覆盖传递到*DpcForIsr*或*CustomDpc*例程的上下文信息的 ISR，直到该例程使用上下文信息并完成了上下文信息所属的 IRP

-   *SynchCritSection*例程，它代表*DpcForIsr*或*CustomDpc*例程访问 ISR 的上下文区域

 

 




