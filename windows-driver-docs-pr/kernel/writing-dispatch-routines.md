---
title: 编写 Dispatch 例程
description: 编写 Dispatch 例程
keywords:
- 调度例程 WDK 内核
- 标准驱动程序例程 WDK 内核，调度例程
- 驱动程序例程 WDK 内核，调度例程
- 例程的 WDK 内核，调度例程
- 系统空间内存分配 WDK 内核
- 系统资源存储 WDK 内核
- 存储系统资源
- 调度例程 WDK 内核，关于调度例程
- Irp WDK 内核，调度例程
- 多个 i/o 函数代码 WDK 内核
- IRP 主要功能代码 WDK 内核
- 主要函数代码 WDK 内核
- 函数代码 WDK 内核
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: bad81ce6d7cbfb58a7f6915c7e7eefa01058e3a2
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96782591"
---
# <a name="writing-dispatch-routines"></a>编写 Dispatch 例程





处理 (IRP) 的任何 i/o 请求包都在调度例程中开始，驱动程序将注册该调度例程来处理 [irp 主功能代码](./irp-major-function-codes.md) (<strong>irp \_ MJ \_ * XXX</strong> <em>) 。驱动程序的 [</em> *DriverEntry* <em>](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize) 例程在驱动 [</em> *程序的驱动程序 \_ 对象* * 结构中的调度表中导出调度例程的入口点](/windows-hardware/drivers/ddi/wdm/ns-wdm-_driver_object)。

驱动程序可以为其处理的每个主要 i/o 函数代码提供单独的调度例程。 或者，可以编写调度例程来处理多个 i/o 函数代码。

本节包含下列主题：

[Dispatch 例程的功能](dispatch-routine-functionality.md)

[必需的 Dispatch 例程](required-dispatch-routines.md)

[可选的 Dispatch 例程](optional-dispatch-routines.md)

[Dispatch 例程和于 IRQL](dispatch-routines-and-irqls.md)

[何时检查驱动程序的 I/O 堆栈位置](when-to-check-the-driver-s-i-o-stack-location.md)

[DispatchCreate、DispatchClose 和 DispatchCreateClose 例程](dispatchcreate--dispatchclose--and-dispatchcreateclose-routines.md)

[DispatchCleanup 例程](dispatchcleanup-routines.md)

[DispatchRead、DispatchWrite 和 DispatchReadWrite 例程](dispatchread--dispatchwrite--and-dispatchreadwrite-routines.md)

[DispatchDeviceControl 和 DispatchInternalDeviceControl 例程](dispatchdevicecontrol-and-dispatchinternaldevicecontrol-routines.md)

[DispatchPnP 例程](dispatchpnp-routines.md)

[DispatchPower 例程](dispatchpower-routines.md)

[DispatchQueryInformation 例程](dispatchqueryinformation-routines.md)

[DispatchSetInformation 例程](dispatchsetinformation-routines.md)

[DispatchFlushBuffers 例程](dispatchflushbuffers-routines.md)

[DispatchShutdown 例程](dispatchshutdown-routines.md)

[DispatchSystemControl 例程](dispatchsystemcontrol-routines.md)
