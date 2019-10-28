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
ms.openlocfilehash: ddfe0ef558fce7fc8f0b4d752600a87d919e2b26
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838513"
---
# <a name="passing-irps-down-the-driver-stack"></a>向驱动程序堆栈的下层传递 IRP





当驱动程序的调度例程收到 IRP 时，它必须调用[**IoGetCurrentIrpStackLocation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetcurrentirpstacklocation) ，以便它可以检查其自己的 i/o 堆栈位置并确定任何参数是否有效。 如果驱动程序无法满足并完成请求，则可以执行下列操作之一：

-   传递 IRP 以供较低级别的驱动程序进一步处理。

-   创建一个或多个新的 Irp，并将它们向下传递到较低级别的驱动程序。

### <a name="a-higher-level-driver-should-pass-an-io-request-on-to-a-next-lower-driver-as-follows"></a>较高级别的驱动程序应将 i/o 请求传递到下一个较低的驱动程序，如下所示：

1.  如果驱动程序将输入 IRP 传递到下一个较低级别的驱动程序，则调度例程应调用[**IoSkipCurrentIrpStackLocation**](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer)或[**IoCopyCurrentIrpStackLocationToNext**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocopycurrentirpstacklocationtonext)来设置下一个较低驱动程序的 i/o 堆栈位置。

    如果驱动程序调用[**IoAllocateIrp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioallocateirp)为较低的驱动程序分配一个或多个附加的 irp，则调度例程必须按照处理中的[irp 中所述的步骤初始化下一个较低版本的驱动程序的 i/o 堆栈位置。中级驱动程序](processing-irps-in-an-intermediate-level-driver.md)。

    调度例程可以修改下一个较低驱动程序的 i/o 堆栈位置中某些请求的一些参数。 例如，当基础设备具有已知的传输容量限制时，较高级别的驱动程序可能会修改大型传输请求的参数，并重复使用 IRP 将部分传输请求发送到基础设备驱动程序。

2.  调用[**IoSetCompletionRoutine**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iosetcompletionroutine)。

    如果调度例程将接收的 IRP 传递到下一个较低版本的驱动程序，则设置[*IoCompletion*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-io_completion_routine)例程是可选的，但很有用，因为例程可以执行如下任务来确定驱动程序完成请求的速度，并重复使用 IRP部分传输，更新驱动程序在跟踪 Irp 时维持的任何状态，并重试返回的包含错误的请求。

    如果调度例程分配了新的 Irp，则需要设置*IoCompletion*例程，因为在较低的驱动程序完成后，例程必须释放每个 irp。

    有关*IoCompletion*例程的详细信息，请参阅[完成 irp](completing-irps.md)。

3.  为每个 IRP 调用[**IoCallDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver) ，以由较低的驱动程序处理。

4.  返回相应的 NTSTATUS 值，例如：
    -   状态\_挂起

        如果输入 IRP 是异步请求（如[**IRP\_mj\_READ**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-read)或[**irp\_MJ\_写入**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-write)，则驱动程序通常会返回状态\_"挂起"。

    -   调用**IoCallDriver**的结果

        如果输入 IRP 为同步请求（如[**IRP\_MJ\_CREATE**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-create)，则驱动程序会频繁返回对**IoCallDriver**的调用结果。

### <a name="a-lowest-level-device-driver-passes-any-irp-that-it-cannot-complete-in-its-dispatch-routine-on-to-other-driver-routines-as-follows"></a>最低级别的设备驱动程序将它无法在其调度例程中完成的任何 IRP 传递到其他驱动程序例程，如下所示：

1.  将[**也**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iomarkirppending)与输入 IRP 一起调用。

2.  调用[**IoStartPacket**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-iostartpacket) ，将 IRP 传递到驱动程序的[*StartIo*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_startio)例程，或将其排队，除非驱动程序管理自己的内部 Irp 队列，如[驱动程序托管的 irp 队列](driver-managed-irp-queues.md)中所述。

    如果驱动程序没有*StartIo*例程但处理可取消的 irp，则它必须注册[*取消*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_cancel)例程或实现[取消安全 irp 队列](cancel-safe-irp-queues.md)。 有关*取消*例程的详细信息，请参阅[取消 irp](canceling-irps.md)。

3.  返回状态\_挂起。

 

 




