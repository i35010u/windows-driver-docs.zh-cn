---
title: 独立的 DispatchCreate 和 DispatchClose 例程
description: 独立的 DispatchCreate 和 DispatchClose 例程
keywords:
- 调度例程 WDK 内核，DispatchCreate 例程
- 调度例程 WDK 内核，DispatchClose 例程
- DispatchClose 例程
- DispatchCreate 例程
- IRP_MJ_CREATE i/o 函数代码
- IRP_MJ_CLOSE i/o 函数代码
- 创建调度例程 WDK 内核
- 关闭调度例程 WDK 内核
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: b9a7b2978d4edb1334e3067bc8a051abbea14d86
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96822267"
---
# <a name="separate-dispatchcreate-and-dispatchclose-routines"></a>独立的 DispatchCreate 和 DispatchClose 例程





对于 [**IRP \_ mj \_ CREATE**](./irp-mj-create.md)和 [**irp \_ mj \_ 关闭**](./irp-mj-close.md)请求，驱动程序的 *调度* 例程只需完成输入 IRP，状态为 " \_ 成功"。 有关详细信息，请参阅 [完成 irp](completing-irps.md)。

用于 **IRP \_ mj \_ CREATE** 和 **irp \_ mj \_ 关闭** 请求的另一个驱动程序 *调度* 例程可能会执行更多操作，具体取决于基础设备驱动程序或基础设备。 请考虑以下方案：

- 收到 create 请求后，类驱动程序可以初始化内部队列并将 [**IRP \_ MJ \_ 内部 \_ 设备 \_ 控制**](./irp-mj-internal-device-control.md) 请求发送到相应的端口驱动程序，该驱动程序请求设备配置信息或独占访问控制器端口。

- 如果收到 **IRP \_ MJ \_ 关闭** ，则表明已删除对与目标设备对象相关联的文件对象的最后一个引用。 这意味着，已关闭文件对象的所有句柄，并已完成或取消所有未完成的 i/o 请求。

- 收到 create 请求后，不常使用的设备的驱动程序可能会调用 [**MmLockPagableCodeSection**](/windows-hardware/drivers/ddi/wdm/nf-wdm-mmlockpagablecodesection) ，使其成为一些处理其他 **IRP \_ MJ \_ * XXX*** 请求的驱动程序例程。 收到倒数 close 请求时，驱动程序可能会调用 [**MmUnlockPagableImageSection**](/windows-hardware/drivers/ddi/wdm/nf-wdm-mmunlockpagableimagesection) ，通过使此类驱动程序的设备 (对象的所有文件对象句柄都已关闭) 关闭，来节省系统内存。

某些驱动程序只为对称处理 **IRP \_ MJ \_ 关闭** 请求，因为在受保护的子系统或更高级别的驱动程序打开其设备对象之后，较低级别的驱动程序的设备对象将不会关闭，直到系统自行关闭。 例如，键盘和鼠标驱动程序设置设备对象，这些对象表示在系统运行时必须正常运行的物理设备，因此，这些驱动程序可能具有用于对称的最小 [*DispatchClose*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch) 例程，也可能是 [*DispatchCreateClose*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch) 例程的组合。

如果由较低级别驱动程序控制的设备必须可供系统继续运行，则通常不会调用驱动程序的 *DispatchClose* 例程。 例如，某些系统磁盘驱动程序没有 *DispatchClose* 例程，但这些驱动程序通常具有 [*DispatchFlushBuffers*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch) 和 [*DispatchShutdown*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch) 例程，用于在系统关闭之前完成任何未完成的文件 i/o 操作。

尽管可以实现单独的 [*DRIVER_DISPATCH*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch) 和 *DispatchClose* 例程，但驱动程序有时会使用 [单个 DispatchCreateClose 例程](a-single-dispatchcreateclose-routine.md) 来处理创建和关闭请求。

 

