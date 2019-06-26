---
title: 您应该使用哪种类型的 DPC
description: 您应该使用哪种类型的 DPC
ms.assetid: 7a8e6d75-5573-4a94-a895-fa2f70856807
keywords:
- 延迟的过程调用 WDK 内核
- Dpc WDK 内核
- DpcForIsr
- CustomDpc
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 854c21f68a5b4b77893780291f37443b80dc7a75
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67358099"
---
# <a name="which-type-of-dpc-should-you-use"></a>应使用哪种类型的 DPC？





具体取决于驱动程序的设计，它可以具有任何以下值：

-   将单个[ *DpcForIsr* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-io_dpc_routine)完成中断驱动的所有 I/O 操作

-   一个或多个一组[ *CustomDpc* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-kdeferred_routine)例程。

-   这两个*DpcForIsr*和特定于操作的一组*CustomDpc*例程

驱动程序是否包含单个*DpcForIsr*例程、 一组*CustomDpc*例程，或将两者都依赖于其基础设备的性质和它必须支持的一套 I/O 请求。

大多数的最低级别的设备驱动程序具有单个*DpcForIsr*例程，以完成 I/O 处理的每个 IRP，需要在其各自的设备上的一个或多个操作。 使用单个*DpcForIsr*来完成每个请求，请执行一次一个操作的设备上中断驱动 I/O 操作量是相对简单。 只需要调用此类的驱动程序的 ISR [ **IoRequestDpc** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iorequestdpc)为每个中断驱动 I/O 操作。

有几个最低级别驱动程序*CustomDpc*例程除非他们的设备需要多个 DPC 完成一组不同的中断驱动 I/O 操作。

使用单个*DpcForIsr*完成重叠的中断驱动 I/O 操作可以执行并发操作的设备上进行了精心设计，但可以是相对较难。 除了或替代队列*DpcForIsr*，ISR 可以排入队列的特定于操作的驱动程序提供一组*CustomDpc*例程通过调用[ **KeInsertQueueDpc**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-keinsertqueuedpc).

例如，考虑一些设计难题参与编写串行驱动程序。 为全双工设备的驱动程序，串行驱动程序不能依赖于在其中 Irp 排队到顺序之间的一一对应关系*StartIo*例程和从其设备中的多任务，中断的序列多处理器系统。 此外，串行驱动程序必须处理超时请求和通过用户生成的异步请求取消以前请求的操作，以清除缓存的数据，等等。

因此，串行驱动程序可能维护内部队列的读取、 写入、 清除，和等待用户模式 COM 端口的应用程序可以请求的操作。 它还可以维护引用计数或其他跟踪机制，如一组标志，用于在其内部队列 Irp。 将调用其 ISR **KeInsertQueueDpc**使用任何数目的驱动程序分配并初始化 DPC 对象，每个驱动程序提供与相关联*CustomDpc*例程。

 

 




