---
title: 较高级驱动程序中的 StartIo 例程
description: 较高级驱动程序中的 StartIo 例程
ms.assetid: 8b0e3bef-4a73-4cf8-b71a-6aedf451d648
keywords:
- StartIo 例程，更高级别的驱动程序
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: bea19bcbe9d06991ba212fe61b66945dfbc40a04
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67382990"
---
# <a name="startio-routines-in-higher-level-drivers"></a>较高级驱动程序中的 StartIo 例程





任何更高级别的驱动程序可以具有[ *StartIo* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_startio)例程。 但是，此类驱动程序不太可能与现有的较低级驱动程序进行互操作，并且可能会表现出较差的性能特征。

一个*StartIo*更高级别的驱动程序中的例程将产生以下影响：

-   可以通过调用排队传入 Irp [ **IoStartPacket** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-iostartpacket)来自驱动程序的*调度*Xxx routine(s) 和[ **IoStartNextPacket** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-iostartnextpacket)从其[ *IoCompletion* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-io_completion_routine) routine(s)，从而导致 Irp 为处理通过一次一个地*StartIo*例程。

-   驱动程序的 I/O 吞吐量可能会变得明显慢期间的大量 I/O 需求，因为其*StartIo*例程可能成为瓶颈。

-   在驱动程序*StartIo*例程调用[ **IoCallDriver** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocalldriver) IRQL 在每个 IRP = 调度\_级别，从而导致所有较低级别驱动程序的调度例程还可以运行在 IRQL = 调度\_级别。 这会限制较低的驱动程序可以调用在其调度例程的支持例程的集。 因为大多数驱动程序编写者都认为其驱动程序的调度例程将运行，在 IRQL&lt;调度\_级别，更高级别的驱动程序不太可能与很多现有的较低级驱动程序进行互操作。

-   *StartIo*例程会降低整体系统的吞吐量，因为在 IRQL 运行它，并在其链中的所有低级驱动程序的调度例程 = 调度\_级别。

    有关标准驱动程序例程将于 Irql 详细信息，请参阅[管理硬件优先级](managing-hardware-priorities.md)。

所有的系统提供的更高级别的驱动程序都不包含*StartIo*例程，因为这会降低 IRP 处理驱动程序本身，上述所有驱动程序和它下面和整体系统。

最更高级别的驱动程序只需从其调度例程将 Irp 发送到较低级别的驱动程序和任何必需执行的清理操作中处理其*IoCompletion*例程。

但是，更高级别的驱动程序可以设置内部队列的请求特定类型的操作，或设置内部队列来保存为一组异类基础设备，如 SCSI 端口驱动程序绑定的 Irp 的 Irp。 有关详细信息，请参阅[队列和取消排队 Irp](queuing-and-dequeuing-irps.md)。

 

 




