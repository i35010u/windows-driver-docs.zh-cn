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
ms.openlocfilehash: 8f2a46b8a2dc07bdecc5bee981ffc5e68b370447
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89186731"
---
# <a name="dispatchread-dispatchwrite-and-dispatchreadwrite-routines"></a>DispatchRead、DispatchWrite 和 DispatchReadWrite 例程





驱动程序的 [*DispatchRead*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch) 和 [*DispatchWrite*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch) 例程分别处理 irp，其中每个 I/o 函数代码为 [**irp \_ mj \_ READ**](./irp-mj-read.md) 和 [**IRP \_ mj \_ WRITE**](./irp-mj-write.md)。 此外，组合的 [*DispatchReadWrite*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch) 例程还可以处理这两个 i/o 函数代码的 irp。

可以将数据传输到系统的设备的每个驱动程序都必须具有 *DispatchRead* 例程。 可将数据从系统传输到的设备的每个驱动程序都必须具有 *DispatchWrite* 例程。 传输双向数据的任何驱动程序都可以有合并的 *DispatchReadWrite* 例程。

较低级别的驱动程序以异步方式处理 **IRP \_ mj \_ 读取** 和 **irp \_ mj \_ 写入** 请求。 因此，在高级驱动程序中的 *DispatchRead* 和/或 *DispatchWrite* 例程必须将这些请求传递给，以便进行进一步处理，前提是该请求在该驱动程序的 i/o 堆栈位置中具有有效的参数。

驱动程序是否为缓冲或直接 i/o 设置其设备对象会影响其处理传输请求的方式。 具体而言，使用直接 i/o 执行 DMA 操作的驱动程序可能需要将大型传输请求拆分为较小的传输操作序列，以便满足 **IRP \_ mj \_ 读取** 或 **IRP \_ mj \_ 写入** 请求。 有关详细信息，请参阅 [输入/输出技术](i-o-programming-techniques.md)。

以下小节讨论了使用缓冲 i/o 和直接 i/o 的最低级别设备驱动程序中的 *DispatchReadWrite* 例程的一些设计和实现注意事项，以及上面分层的更高级别的驱动程序：

[以异步方式处理传输](handling-transfers-asynchronously.md)

[使用缓冲 I/O 执行 DispatchReadWrite](dispatchreadwrite-using-buffered-i-o.md)

[使用直接 I/O 执行 DispatchReadWrite](dispatchreadwrite-using-direct-i-o.md)

[较高级驱动程序中的 DispatchReadWrite](dispatchreadwrite-in-higher-level-drivers.md)

[读/写 Dispatch 例程摘要](summary-of-read-write-dispatch-routines.md)

 

