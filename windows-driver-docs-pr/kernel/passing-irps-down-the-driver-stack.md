---
title: 向驱动程序堆栈的下层传递 IRP
description: 向驱动程序堆栈的下层传递 IRP
ms.assetid: 69d912c5-83cf-4651-b379-de6baea8ddd0
keywords:
- Irp WDK 内核，向下传递堆栈
- 将 Irp 向下传递驱动程序堆栈 WDK
- 将 Irp 向下传送驱动程序堆栈
- I/o 堆栈位置 WDK 内核
- 堆栈位置 WDK 内核
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 62611aad7993f2d02b603ed31a3d49c5cc6ebc05
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89191847"
---
# <a name="passing-irps-down-the-driver-stack"></a>向驱动程序堆栈的下层传递 IRP





当驱动程序的调度例程收到 IRP 时，它必须调用 [**IoGetCurrentIrpStackLocation**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetcurrentirpstacklocation) ，以便它可以检查其自己的 i/o 堆栈位置并确定任何参数是否有效。 如果驱动程序无法满足并完成请求，则可以执行下列操作之一：

-   传递 IRP 以供较低级别的驱动程序进一步处理。

-   创建一个或多个新的 Irp，并将它们向下传递到较低级别的驱动程序。

### <a name="a-higher-level-driver-should-pass-an-io-request-on-to-a-next-lower-driver-as-follows"></a>较高级别的驱动程序应将 i/o 请求传递到下一个较低的驱动程序，如下所示：

1.  如果驱动程序将输入 IRP 传递到下一个较低级别的驱动程序，则调度例程应调用 [**IoSkipCurrentIrpStackLocation**](./mm-bad-pointer.md) 或 [**IoCopyCurrentIrpStackLocationToNext**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocopycurrentirpstacklocationtonext) 来设置下一个较低驱动程序的 i/o 堆栈位置。

    如果驱动程序调用 [**IoAllocateIrp**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioallocateirp) 为较低的驱动程序分配一个或多个附加的 irp，则调度例程必须按照 [处理中间级别驱动程序中的 irp](processing-irps-in-an-intermediate-level-driver.md)中所述的步骤来初始化下一个较低的驱动程序 i/o 堆栈位置。

    调度例程可以修改下一个较低驱动程序的 i/o 堆栈位置中某些请求的一些参数。 例如，当基础设备具有已知的传输容量限制时，较高级别的驱动程序可能会修改大型传输请求的参数，并重复使用 IRP 将部分传输请求发送到基础设备驱动程序。

2.  调用 [**IoSetCompletionRoutine**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iosetcompletionroutine)。

    如果调度例程将接收的 IRP 传递到下一个较低的驱动程序，则设置 [*IoCompletion*](/windows-hardware/drivers/ddi/wdm/nc-wdm-io_completion_routine) 例程是可选的，但很有用，因为例程可以执行以下任务，如确定驱动程序完成请求所需的时间、重复使用 IRP 进行部分传输、更新驱动程序维持的任何状态（如果它跟踪 irp），然后重试返回并返回错误的请求。

    如果调度例程分配了新的 Irp，则需要设置 *IoCompletion* 例程，因为在较低的驱动程序完成后，例程必须释放每个 irp。

    有关 *IoCompletion* 例程的详细信息，请参阅 [完成 irp](completing-irps.md)。

3.  为每个 IRP 调用 [**IoCallDriver**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver) ，以由较低的驱动程序处理。

4.  返回相应的 NTSTATUS 值，例如：
    -   状态已 \_ 挂起

        \_如果输入 irp 是异步请求（如[**IRP \_ Mj \_ 读取**](./irp-mj-read.md)或[**irp \_ mj \_ 写入**](./irp-mj-write.md)），则驱动程序通常会返回 "挂起" 状态。

    -   调用**IoCallDriver**的结果

        如果输入 IRP 为同步请求（如[**IRP \_ MJ \_ CREATE**](./irp-mj-create.md)），则驱动程序会频繁返回对**IoCallDriver**的调用结果。

### <a name="a-lowest-level-device-driver-passes-any-irp-that-it-cannot-complete-in-its-dispatch-routine-on-to-other-driver-routines-as-follows"></a>最低级别的设备驱动程序将它无法在其调度例程中完成的任何 IRP 传递到其他驱动程序例程，如下所示：

1.  将 [**也**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iomarkirppending) 与输入 IRP 一起调用。

2.  调用 [**IoStartPacket**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-iostartpacket) ，将 IRP 传递到驱动程序的 [*StartIo*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_startio) 例程，或将其排队，除非驱动程序管理自己的内部 Irp 队列，如 [驱动程序托管的 irp 队列](driver-managed-irp-queues.md)中所述。

    如果驱动程序没有 *StartIo* 例程但处理可取消的 irp，则它必须注册 [*取消*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_cancel) 例程或实现 [取消安全 irp 队列](cancel-safe-irp-queues.md)。 有关 *取消* 例程的详细信息，请参阅 [取消 irp](canceling-irps.md)。

3.  返回状态为 " \_ 挂起"。

 

