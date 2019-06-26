---
title: 向驱动程序堆栈的下层传递 IRP
description: 向驱动程序堆栈的下层传递 IRP
ms.assetid: 69d912c5-83cf-4651-b379-de6baea8ddd0
keywords:
- Irp WDK 内核，关闭堆栈传递
- 将 Irp 传递关闭驱动程序堆栈 WDK
- 传输驱动程序堆栈下的 Irp
- I/O 堆栈位置 WDK 内核
- 堆栈位置 WDK 内核
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 40c95a4ec8b057ece925256a31ef24eb9043d06d
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67383798"
---
# <a name="passing-irps-down-the-driver-stack"></a>向驱动程序堆栈的下层传递 IRP





当驱动程序的调度例程接收 IRP 时，它必须调用[ **IoGetCurrentIrpStackLocation** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iogetcurrentirpstacklocation) ，以便它可以检查其自己的 I/O 堆栈位置并确定任何参数都有效。 如果该驱动程序不能满足并完成该请求本身，它可以执行下列任一操作：

-   将 IRP 传递进行进一步处理较低级别的驱动程序。

-   创建一个或多个新 Irp，并将其传递到较低级别的驱动程序。

### <a name="a-higher-level-driver-should-pass-an-io-request-on-to-a-next-lower-driver-as-follows"></a>更高级别的驱动程序应 I/O 将请求传递到下一步低驱动程序，如下所示：

1.  如果该驱动程序将传递到下一步的较低级驱动程序的输入 IRP，应调用的调度例程[ **IoSkipCurrentIrpStackLocation** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer)或[ **IoCopyCurrentIrpStackLocationToNext** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocopycurrentirpstacklocationtonext)设置下一步低驱动程序的 I/O 堆栈位置。

    如果该驱动程序调用[ **IoAllocateIrp** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioallocateirp)为较低的驱动程序分配一个或多个其他 Irp，调度例程必须初始化下, 一步低驱动程序的 I/O 堆栈位置的步骤中所述[中间级驱动程序中处理 Irp](processing-irps-in-an-intermediate-level-driver.md)。

    调度例程可以修改某些参数中的某些请求的下一步低驱动程序的 I/O 堆栈位置。 例如，更高级别的驱动程序可能基础设备传输能力，在具有已知的限制时修改大型传输请求的参数，并重复使用 IRP 将部分传输请求发送到基础设备驱动程序。

2.  调用[ **IoSetCompletionRoutine**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iosetcompletionroutine)。

    如果调度例程将接收的 IRP 传递给下一个较低驱动程序，则将设置[ *IoCompletion* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-io_completion_routine)例程是可选的但很有用，因为该例程可以执行更低时如何确定此类任务驱动程序已完成请求，重用 IRP 的部分传输、 更新驱动程序可保证在它跟踪 Irp，无论状态和重试的请求，返回出现错误。

    如果调度例程已经分配了新的 Irp，设置*IoCompletion*例程是必需的因为低级驱动程序都完成后，该例程必须释放每个 IRP。

    有关详细信息*IoCompletion*例程，请参阅[完成 Irp](completing-irps.md)。

3.  调用[ **IoCallDriver** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocalldriver)与由较低的驱动程序处理每个 IRP。

4.  返回适当的 NTSTATUS 值，如：
    -   状态\_PENDING

        驱动程序通常将返回状态\_PENDING 如果 IRP 的输入是一个异步请求，诸如[ **IRP\_MJ\_读取**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-read)或[ **IRP\_MJ\_编写**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-write)。

    -   为调用的结果**IoCallDriver**

        驱动程序将频繁地返回到调用的结果**IoCallDriver** IRP 的输入是否为同步请求，如[ **IRP\_MJ\_创建**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-create).

### <a name="a-lowest-level-device-driver-passes-any-irp-that-it-cannot-complete-in-its-dispatch-routine-on-to-other-driver-routines-as-follows"></a>最低级别的设备驱动程序传递任何 IRP，它不能在完成到其他驱动程序例程其调度例程，如下所示：

1.  调用[ **IoMarkIrpPending** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iomarkirppending) IRP 中的输入。

2.  调用[ **IoStartPacket** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-iostartpacket)传递或队列到驱动程序的 IRP [ *StartIo* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_startio)例程，除非该驱动程序管理其自身内部队列，如中所述的 IRP [Driver-Managed IRP 队列](driver-managed-irp-queues.md)。

    如果该驱动程序不具有*StartIo*例程，但处理可取消 Irp，它必须是寄存器[*取消*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_cancel)例程或实现[取消安全IRP 队列](cancel-safe-irp-queues.md)。 有关详细信息*取消*例程，请参阅[取消 Irp](canceling-irps.md)。

3.  返回状态\_PENDING。

 

 




