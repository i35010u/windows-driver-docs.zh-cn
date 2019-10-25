---
title: 独立的 DispatchCreate 和 DispatchClose 例程
description: 独立的 DispatchCreate 和 DispatchClose 例程
ms.assetid: b2e05555-c70d-4293-8622-51eea92091b1
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
ms.openlocfilehash: d5ccca63f626ea18473555e8154f9de9a630c4df
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72836362"
---
# <a name="separate-dispatchcreate-and-dispatchclose-routines"></a>独立的 DispatchCreate 和 DispatchClose 例程





用于[**IRP\_mj**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-create)的驱动程序*调度*例程\_CREATE 和[**IRP\_MJ\_关闭**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-close)请求的执行操作可能不只是完成\_状态为 "成功" 的输入 IRP。 有关详细信息，请参阅[完成 irp](completing-irps.md)。

用于**IRP\_mj**的另一个驱动程序*调度*例程\_创建和**IRP\_MJ\_关闭**请求可能会执行更多操作，具体取决于基础设备驱动程序或基础设备。 请考虑以下方案：

- 收到 create 请求后，类驱动程序可以初始化内部队列，并将[**IRP\_MJ 发送\_内部\_设备\_控制**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-internal-device-control)请求向下发送到请求设备配置的相应端口驱动程序对控制器端口的信息或独占访问权限。

- **\_MJ\_"关闭**" 时，将显示对与目标设备对象相关联的文件对象的最后引用是否已被删除。 这意味着，已关闭文件对象的所有句柄，并已完成或取消所有未完成的 i/o 请求。

- 收到 create 请求后，不常使用的设备的驱动程序可能会调用[**MmLockPagableCodeSection**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-mmlockpagablecodesection) ，使其成为处理其他**IRP\_MJ\_* XXX*** 请求的一些驱动程序例程。 收到倒数 close 请求时，驱动程序可能会通过使此类驱动程序的设备对象的所有文件对象句柄都关闭后，使其可分页图像部分分页出去，来调用[**MmUnlockPagableImageSection**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-mmunlockpagableimagesection)以节省系统内存。

某些驱动程序只为对称处理**IRP\_MJ\_关闭**请求，因为在受保护的子系统或更高级别的驱动程序打开其设备对象之后，较低级别的驱动程序的设备对象将不会关闭，直到系统本身将关闭。 例如，键盘和鼠标驱动程序设置的设备对象表示在系统运行时必须正常运行的物理设备，因此，这些驱动程序可能具有最小的对称[*DispatchClose*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)例程，也可能已合并[*DispatchCreateClose*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)例程。

如果由较低级别驱动程序控制的设备必须可供系统继续运行，则通常不会调用驱动程序的*DispatchClose*例程。 例如，某些系统磁盘驱动程序没有*DispatchClose*例程，但这些驱动程序通常具有[*DispatchFlushBuffers*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)和[*DispatchShutdown*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)例程，用于完成系统之前的任何未完成的文件 i/o 操作关闭。

尽管可以实现单独的[*DRIVER_DISPATCH*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)和*DispatchClose*例程，但驱动程序有时会使用[单个 DispatchCreateClose 例程](a-single-dispatchcreateclose-routine.md)来处理创建和关闭请求。

 

 




