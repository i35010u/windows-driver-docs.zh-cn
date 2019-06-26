---
title: 编写 Dispatch 例程
description: 编写 Dispatch 例程
ms.assetid: 84eb9372-2ef7-4cc2-94af-97e3399e69e0
keywords:
- 调度例程 WDK 内核
- 标准驱动程序例程 WDK 内核，调度例程
- 驱动程序例程 WDK 内核，调度例程
- 例程 WDK 内核，调度例程
- 系统空间内存分配 WDK 内核
- 系统资源存储 WDK 内核
- 存储系统资源
- 调度例程 WDK 内核，有关调度例程
- Irp WDK 内核，调度例程
- 多个 I/O 函数代码 WDK 内核
- IRP 主要函数代码 WDK 内核
- 主要函数代码 WDK 内核
- 函数代码 WDK 内核
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 09de7bb9b754ab73e264c7a1f0bafff75df7f076
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67374113"
---
# <a name="writing-dispatch-routines"></a>编写 Dispatch 例程





该驱动程序将注册要处理的调度例程中处理所有 I/O 请求数据包 (IRP) 开始[IRP 主要函数代码](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-major-function-codes)(<strong>IRP\_MJ\_* XXX</strong><em>).在驱动程序[ </em> *DriverEntry* <em> ](<https://msdn.microsoft.com/library/windows/hardware/ff544113>)例程将导出一个调度表中的驱动程序中的调度例程的入口点[ </em> *驱动程序\_对象** ](<https://msdn.microsoft.com/library/windows/hardware/ff544174>)结构。

驱动程序可以为每个主要的 I/O 函数代码，它处理提供单独的调度例程。 或者，可以编写调度例程来处理多个 I/O 函数代码。

本部分包含以下主题：

[调度例程功能](dispatch-routine-functionality.md)

[所需的调度例程](required-dispatch-routines.md)

[可选的调度例程](optional-dispatch-routines.md)

[调度例程和于 Irql](dispatch-routines-and-irqls.md)

[何时检查驱动程序的 I/O 堆栈位置](when-to-check-the-driver-s-i-o-stack-location.md)

[DispatchCreate、 DispatchClose 和 DispatchCreateClose 例程](dispatchcreate--dispatchclose--and-dispatchcreateclose-routines.md)

[DispatchCleanup 例程](dispatchcleanup-routines.md)

[DispatchRead、 DispatchWrite 和 DispatchReadWrite 例程](dispatchread--dispatchwrite--and-dispatchreadwrite-routines.md)

[DispatchDeviceControl 和 DispatchInternalDeviceControl 例程](dispatchdevicecontrol-and-dispatchinternaldevicecontrol-routines.md)

[DispatchPnP 例程](dispatchpnp-routines.md)

[DispatchPower 例程](dispatchpower-routines.md)

[DispatchQueryInformation 例程](dispatchqueryinformation-routines.md)

[DispatchSetInformation Routines](dispatchsetinformation-routines.md)

[DispatchFlushBuffers 例程](dispatchflushbuffers-routines.md)

[DispatchShutdown 例程](dispatchshutdown-routines.md)

[DispatchSystemControl 例程](dispatchsystemcontrol-routines.md)

 

 




