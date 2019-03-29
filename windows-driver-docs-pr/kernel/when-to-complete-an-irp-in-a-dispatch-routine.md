---
title: 何时在 Dispatch 例程中完成 IRP
description: 何时在 Dispatch 例程中完成 IRP
ms.assetid: 24159535-927f-490c-9472-05ea565b7ae5
keywords:
- 完成 Irp WDK 内核，调度例程
- 完成 Irp 的调度例程 WDK 内核
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7067367e6fa74cc1fd2da8140b3b1d7080db8c3b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56566538"
---
# <a name="when-to-complete-an-irp-in-a-dispatch-routine"></a>何时在 Dispatch 例程中完成 IRP





通常情况下，驱动程序执行不在其调度例程完成 Irp，除非给定请求的参数无效，或者在设备驱动程序，除非特定**IRP\_MJ\_* XXX*** 不要求任何设备 I/O操作。

分层驱动程序的链中每个驱动程序可以检查的每个 IRP 由驱动程序的调度例程接收到其自身 I/O 堆栈位置中的参数的有效性。 完成并返回最可能的驱动程序的调度例程中的参数无效的 Irp 提高 I/O 吞吐量驱动程序的任何链和整体系统。

更高级别的驱动程序中的调度例程应完成 IRP，或将它传递进行处理的低级驱动程序，按照以下原则：

-   如果调度例程确定其自己的 I/O 堆栈位置中的任何参数无效，则应完成立即具有相应的错误状态，如状态该 IRP\_无效\_参数。

-   如果 IRP 包含函数代码[ **IRP\_MJ\_清理**](https://msdn.microsoft.com/library/windows/hardware/ff550718)，则[ *DispatchCleanup* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)例程必须完成每个 IRP 当前排队到目标设备对象，指定驱动程序的 I/O 中的文件对象堆栈的位置，并完成清理 IRP。

    清除请求指示应用程序，正在终止或已关闭该文件对象，表示驱动程序的设备对象的文件句柄。 当*DispatchCleanup*例程返回时，通常在驱动程序[ *DispatchClose* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)接下来调用例程。

-   否则，更高级别的驱动程序可以仅通过将它传递到下一步低驱动程序来满足该请求。

最低级别驱动程序中的调度例程应完成 IRP 按照以下原则：

-   如果调度例程确定其自己的 I/O 堆栈位置中的任何参数无效，或如果该驱动程序不支持 IRP，它应完成该 IRP 立即与相应的错误状态。 在这种情况下，驱动程序必须完成状态将 status 值 IRP\_成功。

    通常情况下，任何更高级别的驱动程序已检查的参数请求的操作，但最低级别的设备驱动程序应执行其自己的参数检查。

-   如果 IRP 包含函数代码**IRP\_MJ\_清理**，则*DispatchCleanup*例程必须完成每个 IRP 当前排队到目标设备对象，用于给定的文件对象中的驱动程序的 I/O 堆栈位置，然后完成清理 IRP。

    清除请求指示应用程序，正在终止或已关闭该文件对象，表示驱动程序的设备对象的文件句柄。 当*DispatchCleanup*例程返回时，通常在驱动程序*DispatchClose*接下来调用例程。

-   如果该请求不要求任何设备 I/O 操作，调度例程应满足请求，并完成 IRP。

    例如，驱动程序可能将保存其设备的当前模式在设备扩展中，尤其是当它很少在初始化之后更改设备模式。 其[ *DispatchDeviceControl* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)例程则无法满足查询当前的设备模式通过返回此存储的信息的请求。

否则，必须调用的调度例程[ **IoMarkIrpPending**](https://msdn.microsoft.com/library/windows/hardware/ff549422)、 队列继续处理其他驱动程序例程 IRP 和返回状态\_PENDING。

 

 




