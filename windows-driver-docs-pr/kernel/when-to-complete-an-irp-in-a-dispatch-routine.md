---
title: 何时在 Dispatch 例程中完成 IRP
description: 何时在 Dispatch 例程中完成 IRP
ms.assetid: 24159535-927f-490c-9472-05ea565b7ae5
keywords:
- 完成 Irp WDK 内核，调度例程
- 调度例程 WDK 内核，完成 Irp
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 014d94c0ede2febda5559fe0a5d9739a768ee49a
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838317"
---
# <a name="when-to-complete-an-irp-in-a-dispatch-routine"></a>何时在 Dispatch 例程中完成 IRP





通常情况下，驱动程序不会在其调度例程中完成 Irp，除非给定请求的参数无效，或者在设备驱动程序中，除非特定**IRP\_MJ\_<em>XXX</em>** 不需要设备 i/o 操作。

分层驱动程序链中的每个驱动程序都可以在其自己的 i/o 堆栈位置中检查该驱动程序的调度例程收到的每个 IRP 的参数有效性。 在最高可能的驱动程序的调度例程中完成具有无效参数的 Irp 可提高任何驱动程序链和整个系统的 i/o 吞吐量。

在较高级别的驱动程序中，调度例程应完成 IRP，或将其传递给更低版本的驱动程序，根据以下准则进行处理：

-   如果调度例程确定了其自己的 i/o 堆栈位置中的任何参数无效，则它应立即用适当的错误状态（如状态\_无效\_参数）完成该 IRP。

-   如果 IRP 包含函数代码[**IRP\_MJ\_清除**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-cleanup)，则对于驱动程序的 i/o 堆栈位置中指定的文件对象， [*DispatchCleanup*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)例程必须完成当前排队到目标设备对象的每个 IRP，并完成清除 IRP。

    清除请求指示正在终止应用程序，或已关闭表示该驱动程序的设备对象的文件对象的文件句柄。 当*DispatchCleanup*例程返回时，通常会调用驱动程序的[*DispatchClose*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)例程。

-   否则，更高级别的驱动程序只能通过将请求传递到下一个较低的驱动程序来满足该请求。

最低级别的驱动程序中的调度例程应按照以下准则完成 IRP：

-   如果调度例程确定了其自己的 i/o 堆栈位置中的任何参数无效，或者该驱动程序不支持 IRP，则应该立即用适当的错误状态完成该 IRP。 在这种情况下，驱动程序不能完成 IRP，状态值为 "状态"\_"成功"。

    通常，任何更高级别的驱动程序已经为请求的操作检查参数，但最低级别的设备驱动程序也应执行其自身的参数检查。

-   如果 IRP 包含函数代码**IRP\_MJ\_清除**，则对于驱动程序的 i/o 堆栈位置中的给定文件对象， *DispatchCleanup*例程必须完成当前排队到目标设备对象的每个 IRP，然后完成清除 IRP。

    清除请求指示正在终止应用程序，或已关闭表示该驱动程序的设备对象的文件对象的文件句柄。 当*DispatchCleanup*例程返回时，通常会调用驱动程序的*DispatchClose*例程。

-   如果请求不需要设备 i/o 操作，则调度例程应满足请求并完成 IRP。

    例如，驱动程序可以在设备扩展中保存其设备的当前模式，尤其是在初始化后极少更改设备模式。 然后，它的[*DispatchDeviceControl*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)例程可以通过返回此存储的信息来满足查询当前设备模式的请求。

否则，调度例程必须调用[**也**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iomarkirppending)，将 IRP 排队给其他驱动程序例程进行进一步处理，并返回状态\_"挂起"。

 

 




