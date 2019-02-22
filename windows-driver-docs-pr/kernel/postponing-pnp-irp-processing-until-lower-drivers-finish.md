---
title: 较低的驱动程序完成之前推迟 PnP IRP 处理
description: 较低的驱动程序完成之前推迟 PnP IRP 处理
ms.assetid: 5bd9f3aa-30d5-4c45-afec-3e5ae0264f4a
keywords:
- 即插即用 WDK 内核，推迟 IRP 处理
- 即插即用和播放 WDK 内核，推迟 IRP 处理
- WDK PnP Irp
- I/O 请求数据包 WDK 即插即用
- 推迟处理 WDK PnP IRP
- 延迟处理 WDK PnP IRP
- DispatchPnP 例程
- IoCompletion 例程
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 41a7b2bef603ee1268cd8eb60a4163e625850cda
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56533226"
---
# <a name="postponing-pnp-irp-processing-until-lower-drivers-finish"></a>较低的驱动程序完成之前推迟 PnP IRP 处理





一些 PnP 和电源 Irp，必须首先处理由父总线驱动程序的设备，然后按设备堆栈中每个下一步更高版本的驱动程序。 例如，父总线驱动程序必须要执行其开始操作的设备的第一个驱动程序 ([**IRP\_MN\_启动\_设备**](https://msdn.microsoft.com/library/windows/hardware/ff551749)) 后, 跟每个下一步更高版本的驱动程序。 有关此类 IRP，函数和筛选器驱动程序必须设置的 I/O 完成例程、 将 IRP 传递给下一个较低的驱动程序，并推迟任何活动进行处理 IRP，直到 IRP 用完的较低的驱动程序。

[ *IoCompletion* ](https://msdn.microsoft.com/library/windows/hardware/ff548354)例程可以在 IRQL 调度调用\_级别，但函数或筛选器驱动程序可能需要处理 IRP 在 IRQL = 被动\_级别。 若要返回到被动\_级别从*IoCompletion*例程，驱动程序可以使用内核事件。 驱动程序寄存器*IoCompletion*例程，用于设置内核模式事件并在驱动程序中的事件上等待其[ *DispatchPnP* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)例程。 设置事件，较低的驱动程序已完成 IRP，驱动程序可以处理 IRP。

请注意，驱动程序必须不使用此方法以等待完成 power IRP 的低级驱动程序 ([**IRP\_MJ\_POWER**](https://msdn.microsoft.com/library/windows/hardware/ff550784))。 等待中的事件[ *DispatchPower* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)中设置的例程*IoCompletion*例程可能会导致死锁。 请参阅[传递 Power Irp](passing-power-irps.md)有关详细信息。

以下两个图片显示如何驱动程序需要等待完成 PnP IRP 的低级驱动程序的示例。 以下示例显示的函数和总线驱动程序必须执行的内容，以及它们如何与 PnP 管理器和 I/O 管理器进行交互。

![说明处理，第 1 部分再插 irp 的关系图](images/delay1.png)

以下说明与上图中带圆圈的数字相对应：

1.  PnP 管理器调用 I/O 管理器以将 IRP 发送到设备堆栈中的顶部驱动程序。

2.  I/O 管理器调用*DispatchPnP*例程的顶部驱动程序。 在此示例中，设备堆栈 （函数驱动程序和父总线驱动程序） 中有只有两个驱动程序和功能驱动程序是顶部驱动程序。

3.  功能驱动程序声明和初始化一个内核模式事件、 设置下一步低驱动程序的堆栈位置并设置*IoCompletion*此 irp 例程。

    功能驱动程序可以使用[ **IoCopyCurrentIrpStackLocationToNext** ](https://msdn.microsoft.com/library/windows/hardware/ff548387)若要设置的堆栈位置。

    在调用[ **IoSetCompletionRoutine**](https://msdn.microsoft.com/library/windows/hardware/ff549679)，该函数驱动程序设置*InvokeOnSuccess*， *InvokeOnError*，和*InvokeOnCancel*到 **，则返回 TRUE** ，并将内核模式事件传递作为上下文参数的一部分。

4.  功能驱动程序将传递与设备堆栈的下层 IRP [ **IoCallDriver** ](https://msdn.microsoft.com/library/windows/hardware/ff548336)之前执行任何操作来处理 IRP。

5.  I/O 管理器通过调用该驱动程序将 IRP 发送到设备堆栈中的下一步低驱动程序*DispatchPnP*例程。

6.  在此示例中的下一步低驱动程序是设备堆栈，父总线驱动程序中的最低驱动程序。 总线驱动程序执行其操作以启动设备。 总线驱动程序集**Irp-&gt;IoStatus.Status**，设置**Irp-&gt;IoStatus.Information**如果与此 IRP，并通过调用完成 IRP [ **IoCompleteRequest**](https://msdn.microsoft.com/library/windows/hardware/ff548343)。

    如果总线驱动程序调用其他驱动程序例程，或将 I/O 发送到设备，才能启动它，总线驱动程序不会完成 PnP IRP 中其*DispatchPnP*例程。 相反，它必须将标记与挂起的 IRP [ **IoMarkIrpPending** ](https://msdn.microsoft.com/library/windows/hardware/ff549422)并返回状态\_PENDING 从其*DispatchPnP*例程。 该驱动程序更高版本调用**IoCompleteRequest**从另一个驱动程序例程，可能是一个 DPC 例程。

下图显示的第二个示例中，一部分设备堆栈中的更高版本驱动程序在其中恢复其推迟的 IRP 处理。

![说明处理第 2 部分再插 irp 的关系图](images/delay2.png)

以下说明与上图中带圆圈的数字相对应：

1.  当总线驱动程序调用**IoCompleteRequest**，I/O 管理器检查的更高版本的驱动程序的堆栈位置，并调用任意*IoCompletion*它找到的例程。 在此示例中，I/O 管理器查找并调用*IoCompletion*例程的更高的驱动程序，功能驱动程序。

2.  功能驱动程序*IoCompletion*例程设置上下文参数中提供的内核模式事件，并返回状态\_详细\_处理\_必需。

    IoCompletion 例程必须返回状态\_更多\_处理\_必需以免 I/O 管理器调用*IoCompletion*例程在此时间设置的更高版本的驱动程序。 *IoCompletion*例程使用此状态要阻止完成，因此其驱动程序*DispatchPnP*例程可以重新获得控制权。 I/O 管理器将继续调用更高版本驱动程序*IoCompletion*此 irp 的例程时此驱动程序*DispatchPnP*例程完成 IRP。

3.  I/O 管理器停止完成 IRP，并将控制权返回给调用的例程**IoCompleteRequest**，在此示例是总线驱动程序*DispatchPnP*例程。

4.  总线驱动程序返回从其*DispatchPnP*例程替换状态指示其 IRP 处理的结果： 任一状态\_成功或错误状态。

5.  **IoCallDriver**将控制权返回给调用方，它在此示例中为功能驱动程序*DispatchPnP*例程。

6.  功能驱动程序*DispatchPnP*例程恢复处理 IRP。

    如果**IoCallDriver**将返回状态\_PENDING， *DispatchPnP*例程已恢复之前执行其*IoCompletion*调用例程。 *DispatchPnP*例程，因此，必须等待内核事件的信号及其*IoCompletion*例程。 这可确保*DispatchPnP*例程不会继续处理 IRP，直到所有较低的驱动程序已完成。

    如果**Irp-&gt;IoStatus.Status**设置较低的驱动程序错误，到失败 IRP 和功能驱动程序必须继续处理 IRP （除了任何必要的清理）。

7.  一旦低级驱动程序已成功完成 IRP，功能驱动程序处理 IRP。

    对于 Irp 首先由处理父总线驱动程序，总线驱动程序通常设置成功状态， **Irp-&gt;IoStatus.Status**并根据需要设置一个值以**Irp-&gt;IoStatus.Information**。 函数和筛选器驱动程序将保留中的值**IoStatus**原样除非它们失败 IRP。

    功能驱动程序*DispatchPnP*例程调用**IoCompleteRequest**完成 IRP。 I/O 管理器将恢复 I/O 完成处理。 在此示例中，有更高版本的功能驱动程序，因此不会有任何筛选器驱动程序*IoCompletion*例程来调用。 当**IoCompleteRequest**将控制权返回给功能驱动程序*DispatchPnP*例程*DispatchPnP*例程将返回状态。

对于某些 Irp，函数或筛选器驱动程序失败，重新启动设备堆栈手 IRP 的即插即用的管理器会通知的较低的驱动程序。 例如，如果函数或筛选器驱动程序将失败[ **IRP\_MN\_启动\_设备**](https://msdn.microsoft.com/library/windows/hardware/ff551749)，即插即用管理器将发送[ **IRP\_MN\_删除\_设备**](https://msdn.microsoft.com/library/windows/hardware/ff551738)到设备堆栈。

 

 




