---
title: 将 PnP IRP 处理推迟到较低级驱动程序完成为止
description: 将 PnP IRP 处理推迟到较低级驱动程序完成为止
keywords:
- PnP WDK 内核，延迟 IRP 处理
- 即插即用 WDK 内核，推迟 IRP 处理
- Irp WDK PnP
- I/o 请求数据包 WDK PnP
- 延迟 IRP 处理 WDK PnP
- 延迟 IRP 处理 WDK PnP
- DispatchPnP 例程
- IoCompletion 例程
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0f9d4371552d2cbbdf57ee7ddf1d29ab20681ed1
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96803811"
---
# <a name="postponing-pnp-irp-processing-until-lower-drivers-finish"></a>将 PnP IRP 处理推迟到较低级驱动程序完成为止





某些 PnP 和电源 Irp 必须首先由设备的父总线驱动程序处理，然后再由设备堆栈中的每个下一个更高的驱动程序处理。 例如，父总线驱动程序必须是第一个驱动程序，才能对设备执行启动操作 ([**IRP \_ MN \_ start \_ device**](./irp-mn-start-device.md)) ，然后是每个下一个更高的驱动程序。 对于这种 IRP，函数和筛选器驱动程序必须设置 i/o 完成例程，将 IRP 传递到下一个较低的驱动程序，并推迟任何活动以处理 IRP，直到使用 IRP 完成较低的驱动程序。

[*IoCompletion*](/windows-hardware/drivers/ddi/wdm/nc-wdm-io_completion_routine)例程可以在 irql 调度 \_ 级别调用，但是函数或筛选器驱动程序可能需要在 irql = 被动级别处理 IRP \_ 。 若要 \_ 从 *IoCompletion* 例程返回到被动级别，驱动程序可以使用内核事件。 驱动程序将注册一个 *IoCompletion* 例程，用于设置内核模式事件，然后驱动程序在其 [*DispatchPnP*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch) 例程中等待事件。 设置事件后，较低的驱动程序已经完成 IRP，并允许该驱动程序处理 IRP。

请注意，驱动程序不得使用此方法来等待较低的驱动程序完成 power IRP ([**IRP \_ MJ \_ power**](./irp-mj-power.md)) 。 等待 *IoCompletion* 例程中设置的 [*DispatchPower*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)例程中的事件可能会导致死锁。 有关详细信息，请参阅 [传递 Power irp](passing-power-irps.md) 。

下面两个图显示了驱动程序如何等待较低驱动程序完成 PnP IRP 的示例。 该示例显示了函数和总线驱动程序必须执行的操作，以及它们如何与 PnP 管理器和 i/o 管理器进行交互。

![说明延迟即插即用 irp 处理的示意图，第1部分](images/delay1.png)

以下说明与上图中的带圆圈数字相对应：

1.  PnP 管理器调用 i/o 管理器将 IRP 发送到设备堆栈中的顶层驱动程序。

2.  I/o 管理器调用顶部驱动程序的 *DispatchPnP* 例程。 在此示例中，设备堆栈中只有两个驱动程序， (功能驱动程序和父总线驱动程序) 并且函数驱动程序是顶层驱动程序。

3.  函数驱动程序声明并初始化一个内核模式事件，设置下一个较低驱动程序的堆栈位置，并为此 IRP 设置 *IoCompletion* 例程。

    函数驱动程序可以使用 [**IoCopyCurrentIrpStackLocationToNext**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocopycurrentirpstacklocationtonext) 设置堆栈位置。

    在对 [**IoSetCompletionRoutine**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iosetcompletionroutine)的调用中，函数驱动程序将 *InvokeOnSuccess*、 *InvokeOnError* 和 *InvokeOnCancel* 设置为 **TRUE** ，并将内核模式事件作为上下文参数的一部分传递。

4.  函数驱动程序在执行任何操作来处理 IRP 之前，会将 IRP 向下传递到 [**IoCallDriver**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver) 。

5.  I/o 管理器通过调用该驱动程序的 *DispatchPnP* 例程将 IRP 发送到设备堆栈中的下一个较低的驱动程序。

6.  在此示例中，下一个较低的驱动程序是设备堆栈（父总线驱动程序）中的最低驱动程序。 总线驱动程序执行其操作来启动设备。 如果与此 IRP 相关，则总线驱动程序将 **&gt; IoStatus** 设置为 irp **- &gt; IoStatus** ，并通过调用 [**IoCompleteRequest**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocompleterequest)来完成 irp。

    如果总线驱动程序调用其他驱动程序例程或将 i/o 发送到设备以便启动，则总线驱动程序不会在其 *DispatchPnP* 例程中完成 PnP IRP。 相反，它必须将 IRP 标记为 " [**也**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iomarkirppending) "，并在 \_ 其 *DispatchPnP* 例程中返回 "挂起" 状态。 稍后，驱动程序从另一个驱动程序例程（可能是 DPC 例程）调用 **IoCompleteRequest** 。

下图显示了示例的第二部分，在此示例中，设备堆栈中的更高驱动程序将恢复其延迟的 IRP 处理。

![说明推迟即插即用 irp 处理的关系图，第2部分](images/delay2.png)

以下说明与上图中的带圆圈数字相对应：

1.  当总线驱动程序调用 **IoCompleteRequest** 时，i/o 管理器会检查更高驱动程序的堆栈位置，并调用它找到的任何 *IoCompletion* 例程。 在此示例中，i/o 管理器查找并调用下一个更高版本的驱动程序（函数驱动程序）的 *IoCompletion* 例程。

2.  函数驱动程序的 *IoCompletion* 例程设置上下文参数中提供的内核模式事件，并返回 \_ 所需的状态更多 \_ 处理 \_ 。

    IoCompletion 例程必须返回状态 \_ \_ \_ ，以便阻止 i/o 管理器在此时调用由较高驱动程序设置的 *IoCompletion* 例程所需的状态。 *IoCompletion* 例程使用此状态来 forestall 完成，因此其驱动程序的 *DispatchPnP* 例程可以重新获得控制权。 当此驱动程序的 *DispatchPnP* 例程完成 irp 时，i/o 管理器将继续为此 irp 调用更高的驱动程序 *IoCompletion* 例程。

3.  I/o 管理器停止完成 IRP 并将控制返回到调用 **IoCompleteRequest** 的例程，在此示例中为总线驱动程序的 *DispatchPnP* 例程。

4.  总线驱动程序从其 *DispatchPnP* 例程返回，状态指示其 IRP 处理的结果：状态为 \_ 成功或错误状态。

5.  **IoCallDriver** 将控制权返回给其调用方，在本例中为函数驱动程序的 *DispatchPnP* 例程。

6.  函数驱动程序的 *DispatchPnP* 例程将继续处理 IRP。

    如果 **IoCallDriver** 返回状态 \_ "挂起"，则 *DispatchPnP* 例程在调用其 *IoCompletion* 例程之前恢复了执行。 因此， *DispatchPnP* 例程必须等待内核事件发出 *IoCompletion* 例程的信号。 这可确保 *DispatchPnP* 例程不会继续处理 IRP，直到所有较低版本的驱动程序都已完成。

    如果 **irp- &gt; IoStatus** 设置为错误，则低级驱动程序已失败 irp，并且函数驱动程序不得继续处理 irp (除了任何必要的清理) 。

7.  在较低的驱动程序成功完成 IRP 后，函数驱动程序将处理 IRP。

    对于首先由父总线驱动程序处理的 Irp，总线驱动程序通常会在 **&gt; IoStatus** 中设置成功状态，还可以选择在 **irp- &gt; IoStatus** 中设置一个值。 函数和筛选器驱动程序将 **IoStatus** 中的值保留原样，除非它们失败。

    函数驱动程序的 *DispatchPnP* 例程调用 **IOCOMPLETEREQUEST** 来完成 IRP。 I/o 管理器恢复 i/o 完成处理。 在此示例中，函数驱动程序之上没有筛选器驱动程序，因此没有其他要调用的 *IoCompletion* 例程。 当 **IoCompleteRequest** 将控制权返回给函数驱动程序 *DispatchPnP* 例程时， *DispatchPnP* 例程返回状态。

对于某些 Irp，如果某个函数或筛选器驱动程序失败了 IRP 备份设备堆栈的方式，则 PnP 管理器会通知较低的驱动程序。 例如，如果某个函数或筛选器驱动程序失败了 [**IRP \_ MN \_ 启动 \_ 设备**](./irp-mn-start-device.md)，则 PnP 管理器会将 [**irp \_ MN \_ 删除 \_ 设备**](./irp-mn-remove-device.md) 发送到设备堆栈。

 

