---
title: DispatchRead、DispatchWrite 和 DispatchReadWrite 例程
description: DispatchRead、DispatchWrite 和 DispatchReadWrite 例程
ms.assetid: 2982939a-4afb-4b21-9a96-0ac758f0fb6c
keywords:
- DispatchRead 例程
- DispatchWrite 例程
- DispatchReadWrite 例程
- 调度例程 WDK 内核，DispatchReadWrite 例程
- 调度例程 WDK 内核，DispatchWrite 例程
- 调度例程 WDK 内核，DispatchRead 例程
- 读/写调度例程 WDK 内核
- IRP_MJ_WRITE I/O 函数代码
- IRP_MJ_READ I/O 函数代码
- 数据传输 WDK 内核，读/写调度例程
- 传输数据 WDK 内核，读/写调度例程
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 12500961b4e637857e934b225c3ac850e420303c
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384979"
---
# <a name="dispatchread-dispatchwrite-and-dispatchreadwrite-routines"></a>DispatchRead、DispatchWrite 和 DispatchReadWrite 例程





驱动程序的[ *DispatchRead* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)并[ *DispatchWrite* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)例程使用的 I/O 函数代码来处理 Irp [ **IRP\_MJ\_读取**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-read)并[ **IRP\_MJ\_编写**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-write)分别。 或者，组合[ *DispatchReadWrite* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)例程可以处理 Irp 为这两个这些 I/O 函数代码。

设备将从其数据可以传输到系统的每个驱动程序必须具有*DispatchRead*例程。 设备向其可以从系统传输数据的每个驱动程序必须具有*DispatchWrite*例程。 将两个方向中的数据传输任何驱动程序可以有组合*DispatchReadWrite*例程。

较低级别的驱动程序处理**IRP\_MJ\_读取**并**IRP\_MJ\_编写**异步请求。 因此， *DispatchRead*和/或*DispatchWrite*最高级别的驱动程序中的例程必须传递这些请求进行进一步处理，前提是请求该驱动程序中具有有效的参数IRP 的 I/O 堆栈位置。

是否一个驱动程序设置了其设备对象为缓冲或直接 I/O 会影响它如何处理传输请求。 具体而言，使用直接 I/O 执行 DMA 操作的驱动程序可能需要拆分成较小的传输操作的序列才能符合要求的大型传输请求**IRP\_MJ\_读取**或**IRP\_MJ\_编写**请求。 有关详细信息，请参阅[输入/输出技术](i-o-programming-techniques.md)。

以下各小节讨论一些设计和实现注意事项*DispatchReadWrite*例程以及更高级别的驱动程序中使用缓冲的 I/O 和直接 I/O 的最低级别的设备驱动程序上面它们：

[以异步方式处理传输](handling-transfers-asynchronously.md)

[DispatchReadWrite 使用缓冲的 I/O](dispatchreadwrite-using-buffered-i-o.md)

[使用直接 I/O DispatchReadWrite](dispatchreadwrite-using-direct-i-o.md)

[在更高级别的驱动程序中的 DispatchReadWrite](dispatchreadwrite-in-higher-level-drivers.md)

[读/写调度例程的摘要](summary-of-read-write-dispatch-routines.md)

 

 




