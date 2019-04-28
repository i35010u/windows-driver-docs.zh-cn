---
title: 较高级驱动程序中的 StartIo 例程
description: 较高级驱动程序中的 StartIo 例程
ms.assetid: 8b0e3bef-4a73-4cf8-b71a-6aedf451d648
keywords:
- StartIo 例程，更高级别的驱动程序
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: c99d78155f63908c02cda53caa444f887170b535
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63331953"
---
# <a name="startio-routines-in-higher-level-drivers"></a>较高级驱动程序中的 StartIo 例程





任何更高级别的驱动程序可以具有[ *StartIo* ](https://msdn.microsoft.com/library/windows/hardware/ff563858)例程。 但是，此类驱动程序不太可能与现有的较低级驱动程序进行互操作，并且可能会表现出较差的性能特征。

一个*StartIo*更高级别的驱动程序中的例程将产生以下影响：

-   可以通过调用排队传入 Irp [ **IoStartPacket** ](https://msdn.microsoft.com/library/windows/hardware/ff550370)来自驱动程序的*调度*Xxx routine(s) 和[ **IoStartNextPacket** ](https://msdn.microsoft.com/library/windows/hardware/ff550358)从其[ *IoCompletion* ](https://msdn.microsoft.com/library/windows/hardware/ff548354) routine(s)，从而导致 Irp 为处理通过一次一个地*StartIo*例程。

-   驱动程序的 I/O 吞吐量可能会变得明显慢期间的大量 I/O 需求，因为其*StartIo*例程可能成为瓶颈。

-   在驱动程序*StartIo*例程调用[ **IoCallDriver** ](https://msdn.microsoft.com/library/windows/hardware/ff548336) IRQL 在每个 IRP = 调度\_级别，从而导致所有较低级别驱动程序的调度例程还可以运行在 IRQL = 调度\_级别。 这会限制较低的驱动程序可以调用在其调度例程的支持例程的集。 因为大多数驱动程序编写者都认为其驱动程序的调度例程将运行，在 IRQL&lt;调度\_级别，更高级别的驱动程序不太可能与很多现有的较低级驱动程序进行互操作。

-   *StartIo*例程会降低整体系统的吞吐量，因为在 IRQL 运行它，并在其链中的所有低级驱动程序的调度例程 = 调度\_级别。

    有关标准驱动程序例程将于 Irql 详细信息，请参阅[管理硬件优先级](managing-hardware-priorities.md)。

所有的系统提供的更高级别的驱动程序都不包含*StartIo*例程，因为这会降低 IRP 处理驱动程序本身，上述所有驱动程序和它下面和整体系统。

最更高级别的驱动程序只需从其调度例程将 Irp 发送到较低级别的驱动程序和任何必需执行的清理操作中处理其*IoCompletion*例程。

但是，更高级别的驱动程序可以设置内部队列的请求特定类型的操作，或设置内部队列来保存为一组异类基础设备，如 SCSI 端口驱动程序绑定的 Irp 的 Irp。 有关详细信息，请参阅[队列和取消排队 Irp](queuing-and-dequeuing-irps.md)。

 

 




