---
title: 何时在 Dispatch 例程中完成 IRP
description: 何时在 Dispatch 例程中完成 IRP
keywords:
- 完成 Irp WDK 内核，调度例程
- 调度例程 WDK 内核，完成 Irp
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6453f8e84b28855b1074d0b1cd9ab4a17e45d854
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96832285"
---
# <a name="when-to-complete-an-irp-in-a-dispatch-routine"></a>何时在 Dispatch 例程中完成 IRP





通常，驱动程序不会在其调度例程中完成 Irp，除非给定请求的参数无效，或者在设备驱动程序中，除非特定 **IRP \_ MJ \_ <em>XXX</em>** 不需要设备 i/o 操作。

分层驱动程序链中的每个驱动程序都可以在其自己的 i/o 堆栈位置中检查该驱动程序的调度例程收到的每个 IRP 的参数有效性。 在最高可能的驱动程序的调度例程中完成具有无效参数的 Irp 可提高任何驱动程序链和整个系统的 i/o 吞吐量。

在较高级别的驱动程序中，调度例程应完成 IRP，或将其传递给更低版本的驱动程序，根据以下准则进行处理：

-   如果调度例程确定其自己的 i/o 堆栈位置中的任何参数无效，则应使用适当的错误状态（如 STATUS 无效参数）立即完成 IRP \_ \_ 。

-   如果 IRP 包含函数代码 [**IRP \_ MJ \_ 清除**](./irp-mj-cleanup.md)，则 [*DispatchCleanup*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch) 例程必须将当前排队的每个 IRP 都完成为驱动程序的 i/o 堆栈位置中指定的文件对象，并完成清除 IRP。

    清除请求指示正在终止应用程序，或已关闭表示该驱动程序的设备对象的文件对象的文件句柄。 当 *DispatchCleanup* 例程返回时，通常会调用驱动程序的 [*DispatchClose*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch) 例程。

-   否则，更高级别的驱动程序只能通过将请求传递到下一个较低的驱动程序来满足该请求。

最低级别的驱动程序中的调度例程应按照以下准则完成 IRP：

-   如果调度例程确定了其自己的 i/o 堆栈位置中的任何参数无效，或者该驱动程序不支持 IRP，则应该立即用适当的错误状态完成该 IRP。 在这种情况下，驱动程序不能完成 IRP，状态值为 " \_ 成功"。

    通常，任何更高级别的驱动程序已经为请求的操作检查参数，但最低级别的设备驱动程序也应执行其自身的参数检查。

-   如果 IRP 包含函数代码 **IRP \_ MJ \_ 清除**，则 *DispatchCleanup* 例程必须将当前排队的每个 IRP 都完成为驱动程序的 i/o 堆栈位置中给定文件对象的目标设备对象，然后完成清除 IRP。

    清除请求指示正在终止应用程序，或已关闭表示该驱动程序的设备对象的文件对象的文件句柄。 当 *DispatchCleanup* 例程返回时，通常会调用驱动程序的 *DispatchClose* 例程。

-   如果请求不需要设备 i/o 操作，则调度例程应满足请求并完成 IRP。

    例如，驱动程序可以在设备扩展中保存其设备的当前模式，尤其是在初始化后极少更改设备模式。 然后，它的 [*DispatchDeviceControl*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch) 例程可以通过返回此存储的信息来满足查询当前设备模式的请求。

否则，调度例程必须调用 [**也**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iomarkirppending)，将 IRP 排队给其他驱动程序例程以进行进一步处理，并返回 "挂起" 状态 \_ 。

 

