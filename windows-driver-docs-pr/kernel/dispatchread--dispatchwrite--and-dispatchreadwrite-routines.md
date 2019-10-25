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
- IRP_MJ_WRITE i/o 函数代码
- IRP_MJ_READ i/o 函数代码
- 数据传输 WDK 内核，读/写调度例程
- 传输数据 WDK 内核，读取/写入调度例程
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: dd34f3de9a4926fb24fce991dcfaefc879616728
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838726"
---
# <a name="dispatchread-dispatchwrite-and-dispatchreadwrite-routines"></a>DispatchRead、DispatchWrite 和 DispatchReadWrite 例程





驱动程序的[*DispatchRead*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)和[*DispatchWrite*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)例程使用 irp 的 i/o 函数代码来处理 IRP [ **\_mj\_READ**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-read)和[**irp\_mj\_WRITE**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-write)。 此外，组合的[*DispatchReadWrite*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)例程还可以处理这两个 i/o 函数代码的 irp。

可以将数据传输到系统的设备的每个驱动程序都必须具有*DispatchRead*例程。 可将数据从系统传输到的设备的每个驱动程序都必须具有*DispatchWrite*例程。 传输双向数据的任何驱动程序都可以有合并的*DispatchReadWrite*例程。

较低级别的驱动程序将**IRP\_mj\_READ**和**IRP\_\_mj 异步写入**请求。 因此，在高级驱动程序中的*DispatchRead*和/或*DispatchWrite*例程必须将这些请求传递给，以便进行进一步处理，前提是该请求在该驱动程序的 i/o 堆栈位置中具有有效的参数。

驱动程序是否为缓冲或直接 i/o 设置其设备对象会影响其处理传输请求的方式。 具体而言，使用直接 i/o 执行 DMA 操作的驱动程序可能需要将大型传输请求拆分为一系列较小的传输操作，以便满足**IRP\_MJ\_读取**或**IRP\_mj\_写入**请求。 有关详细信息，请参阅[输入/输出技术](i-o-programming-techniques.md)。

以下小节讨论了使用缓冲 i/o 和直接 i/o 的最低级别设备驱动程序中的*DispatchReadWrite*例程的一些设计和实现注意事项，以及上面分层的更高级别的驱动程序：

[异步处理传输](handling-transfers-asynchronously.md)

[使用缓冲 i/o 的 DispatchReadWrite](dispatchreadwrite-using-buffered-i-o.md)

[使用直接 i/o 的 DispatchReadWrite](dispatchreadwrite-using-direct-i-o.md)

[更高级的驱动程序中的 DispatchReadWrite](dispatchreadwrite-in-higher-level-drivers.md)

[读/写调度例程摘要](summary-of-read-write-dispatch-routines.md)

 

 




