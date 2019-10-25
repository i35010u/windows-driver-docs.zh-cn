---
title: 将 PnP IRP 处理推迟到较低级驱动程序完成为止
description: 将 PnP IRP 处理推迟到较低级驱动程序完成为止
ms.assetid: 5bd9f3aa-30d5-4c45-afec-3e5ae0264f4a
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
ms.openlocfilehash: 48245dcd7d57681299e91b1ccc094592d062eea6
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72827655"
---
# <a name="postponing-pnp-irp-processing-until-lower-drivers-finish"></a>将 PnP IRP 处理推迟到较低级驱动程序完成为止





某些 PnP 和电源 Irp 必须首先由设备的父总线驱动程序处理，然后再由设备堆栈中的每个下一个更高的驱动程序处理。 例如，父总线驱动程序必须是第一个用于对设备执行启动操作的驱动程序（[**IRP\_MN\_start\_设备**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-start-device)），后跟每个下一个较高版本的驱动程序。 对于这种 IRP，函数和筛选器驱动程序必须设置 i/o 完成例程，将 IRP 传递到下一个较低的驱动程序，并推迟任何活动以处理 IRP，直到使用 IRP 完成较低的驱动程序。

[*IoCompletion*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-io_completion_routine)例程可以在 irql 调度\_级别调用，但是函数或筛选器驱动程序可能需要以 IRQL = 被动\_级别处理 IRP。 若要从*IoCompletion*例程返回到被动\_级别，驱动程序可以使用内核事件。 驱动程序将注册一个*IoCompletion*例程，用于设置内核模式事件，然后驱动程序在其[*DispatchPnP*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)例程中等待事件。 设置事件后，较低的驱动程序已经完成 IRP，并允许该驱动程序处理 IRP。

请注意，驱动程序不得使用此方法来等待较低的驱动程序完成 power IRP （[**IRP\_MJ\_power**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-power)）。 等待*IoCompletion*例程中设置的[*DispatchPower*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)例程中的事件可能会导致死锁。 有关详细信息，请参阅[传递 Power irp](passing-power-irps.md) 。

下面两个图显示了驱动程序如何等待较低驱动程序完成 PnP IRP 的示例。 该示例显示了函数和总线驱动程序必须执行的操作，以及它们如何与 PnP 管理器和 i/o 管理器进行交互。

![说明延迟即插即用 irp 处理的示意图，第1部分](images/delay1.png)

以下说明与上图中的带圆圈数字相对应：

1.  PnP 管理器调用 i/o 管理器将 IRP 发送到设备堆栈中的顶层驱动程序。

2.  I/o 管理器调用顶部驱动程序的*DispatchPnP*例程。 在此示例中，设备堆栈中只有两个驱动程序（函数驱动程序和父总线驱动程序），并且函数驱动程序是顶级驱动程序。

3.  函数驱动程序声明并初始化一个内核模式事件，设置下一个较低驱动程序的堆栈位置，并为此 IRP 设置*IoCompletion*例程。

    函数驱动程序可以使用[**IoCopyCurrentIrpStackLocationToNext**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocopycurrentirpstacklocationtonext)设置堆栈位置。

    在对[**IoSetCompletionRoutine**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iosetcompletionroutine)的调用中，函数驱动程序将*InvokeOnSuccess*、 *InvokeOnError*和*InvokeOnCancel*设置为**TRUE** ，并将内核模式事件作为上下文参数的一部分传递。

4.  函数驱动程序在执行任何操作来处理 IRP 之前，会将 IRP 向下传递到[**IoCallDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver) 。

5.  I/o 管理器通过调用该驱动程序的*DispatchPnP*例程将 IRP 发送到设备堆栈中的下一个较低的驱动程序。

6.  在此示例中，下一个较低的驱动程序是设备堆栈（父总线驱动程序）中的最低驱动程序。 总线驱动程序执行其操作来启动设备。 总线驱动程序将**irp&gt;** 设置为：如果与此 Irp 相关，则设置**irp&gt;IoStatus** ，并通过调用[**IoCompleteRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocompleterequest)完成 irp。

    如果总线驱动程序调用其他驱动程序例程或将 i/o 发送到设备以便启动，则总线驱动程序不会在其*DispatchPnP*例程中完成 PnP IRP。 相反，它必须将 IRP 标记为 "挂起"，并将 "[**也**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iomarkirppending)"返回状态\_"挂起"。 稍后，驱动程序从另一个驱动程序例程（可能是 DPC 例程）调用**IoCompleteRequest** 。

下图显示了示例的第二部分，在此示例中，设备堆栈中的更高驱动程序将恢复其延迟的 IRP 处理。

![说明推迟即插即用 irp 处理的关系图，第2部分](images/delay2.png)

以下说明与上图中的带圆圈数字相对应：

1.  当总线驱动程序调用**IoCompleteRequest**时，i/o 管理器会检查更高驱动程序的堆栈位置，并调用它找到的任何*IoCompletion*例程。 在此示例中，i/o 管理器查找并调用下一个更高版本的驱动程序（函数驱动程序）的*IoCompletion*例程。

2.  函数驱动程序的*IoCompletion*例程设置上下文参数中提供的内核模式事件，并返回状态\_\_需要更多的\_处理。

    IoCompletion 例程必须返回状态\_更多的\_处理\_需要此方法来阻止 i/o 管理器调用由较高驱动程序设置的*IoCompletion*例程。 *IoCompletion*例程使用此状态来 forestall 完成，因此其驱动程序的*DispatchPnP*例程可以重新获得控制权。 当此驱动程序的*DispatchPnP*例程完成 irp 时，i/o 管理器将继续为此 irp 调用更高的驱动程序*IoCompletion*例程。

3.  I/o 管理器停止完成 IRP 并将控制返回到调用**IoCompleteRequest**的例程，在此示例中为总线驱动程序的*DispatchPnP*例程。

4.  总线驱动程序从其*DispatchPnP*例程返回，状态指示其 IRP 处理的结果：状态\_成功或错误状态。

5.  **IoCallDriver**将控制权返回给其调用方，在本例中为函数驱动程序的*DispatchPnP*例程。

6.  函数驱动程序的*DispatchPnP*例程将继续处理 IRP。

    如果**IoCallDriver**返回\_挂起状态，则*DispatchPnP*例程在调用其*IoCompletion*例程之前恢复了执行。 因此， *DispatchPnP*例程必须等待内核事件发出*IoCompletion*例程的信号。 这可确保*DispatchPnP*例程不会继续处理 IRP，直到所有较低版本的驱动程序都已完成。

    如果**irp&gt;IoStatus**设置为错误，则低级驱动程序无法继续处理 irp，并且函数驱动程序不得继续处理 irp （任何必要的清理操作除外）。

7.  在较低的驱动程序成功完成 IRP 后，函数驱动程序将处理 IRP。

    对于首先由父总线驱动程序处理的 Irp，总线驱动程序通常会在**irp&gt;IoStatus**中设置成功状态，还可以选择在**Irp-&gt;IoStatus**中设置一个值。 函数和筛选器驱动程序将**IoStatus**中的值保留原样，除非它们失败。

    函数驱动程序的*DispatchPnP*例程调用**IOCOMPLETEREQUEST**来完成 IRP。 I/o 管理器恢复 i/o 完成处理。 在此示例中，函数驱动程序之上没有筛选器驱动程序，因此没有其他要调用的*IoCompletion*例程。 当**IoCompleteRequest**将控制权返回给函数驱动程序*DispatchPnP*例程时， *DispatchPnP*例程返回状态。

对于某些 Irp，如果某个函数或筛选器驱动程序失败了 IRP 备份设备堆栈的方式，则 PnP 管理器会通知较低的驱动程序。 例如，如果某个函数或筛选器驱动程序失败了[**IRP\_MN\_启动\_设备**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-start-device)，则 PnP 管理器会将[**irp\_MN\_删除\_设备**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-remove-device)发送到设备堆栈。

 

 




