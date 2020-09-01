---
title: 为较低级驱动程序创建 IRP
description: 为较低级驱动程序创建 IRP
ms.assetid: 2d298eb1-6169-4742-80c1-200223a2d4fa
keywords:
- Irp WDK 内核，创建
- 异步请求 WDK Irp
- Irp WDK 内核，异步请求
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: c48a49bd38a4b09e0105cfa6d5f971ec8ab2dc10
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89189553"
---
# <a name="creating-irps-for-lower-level-drivers"></a>为较低级驱动程序创建 IRP





若要为异步请求分配 IRP，此操作将在较低的驱动程序的任意线程上下文中进行处理， [*DispatchReadWrite*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch) 例程可以调用以下支持例程之一：

-   [**IoAllocateIrp**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioallocateirp)，用于分配 IRP 和多个零初始化 i/o 堆栈位置

    调度例程必须为新分配的 IRP 设置下一个低的驱动程序 i/o 堆栈位置，这通常是通过复制 (可能会从原始 IRP 中其自身的堆栈位置修改) 信息。 如果较高级别的驱动程序为新分配的 IRP 分配其自己的 i/o 堆栈位置，则调度例程可以为要使用的 [*IoCompletion*](/windows-hardware/drivers/ddi/wdm/nc-wdm-io_completion_routine) 例程设置每个请求的上下文信息。

-   [**IoBuildAsynchronousFsdRequest**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iobuildasynchronousfsdrequest)，根据调用方指定的参数为调用方设置下一个较低的驱动程序 i/o 堆栈位置

    较高级别的驱动程序可以调用此例程，为 [**irp \_ mj \_ 读取**](./irp-mj-read.md)、 [**irp \_ mj \_ 写入**](./irp-mj-write.md)、 [**irp \_ mj \_ 刷新 \_ 缓冲区**](./irp-mj-flush-buffers.md)和 [**IRP \_ mj \_ 关闭**](./irp-mj-shutdown.md) 请求分配 irp。

    为此类 IRP 调用 [*IoCompletion*](/windows-hardware/drivers/ddi/wdm/nc-wdm-io_completion_routine) 例程时，它可以检查 i/o 状态块，如有必要 (或可能) 在 IRP 中再次设置下一个较低的 i/o 堆栈位置，然后重试该请求或重复使用它。 但是， *IoCompletion* 例程在 IRP 中没有自身的本地上下文存储，因此，驱动程序必须在驻留内存中其他位置维护有关原始请求的上下文。

-   [**IoMakeAssociatedIrp**](/windows-hardware/drivers/ddi/ntddk/nf-ntddk-iomakeassociatedirp)，它分配 irp 和多个零初始化 i/o 堆栈位置，并将 irp 与 *主* IRP 关联。

    中间驱动程序无法调用 [**IoMakeAssociatedIrp**](/windows-hardware/drivers/ddi/ntddk/nf-ntddk-iomakeassociatedirp) 为较低的驱动程序创建 irp。

    调用 **IoMakeAssociatedIrp** 创建 irp 用于较低驱动程序的任何最高级别驱动程序都可以在发送其关联的 irp 并为原始的 master IRP 调用 [**也**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iomarkirppending) 后，将控制权返回给 i/o 管理器。 当所有关联的 Irp 都已由较低版本的驱动程序完成时，最高级别的驱动程序可以依赖于 i/o 管理器来完成主 IRP。

    驱动程序很少为关联的 IRP 设置 [*IoCompletion*](/windows-hardware/drivers/ddi/wdm/nc-wdm-io_completion_routine) 例程。 如果最高级别的驱动程序为其创建的关联 IRP 调用 [**IoSetCompletionRoutine**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iosetcompletionroutine) ，则如果驱动程序 \_ \_ \_ 从其 *IoCompletion* 例程返回状态更多处理，则 I/O 管理器不会完成主 IRP。 在这些情况下，驱动程序的 *IoCompletion* 例程必须通过 [**IoCompleteRequest**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocompleterequest)显式完成 master IRP。

如果驱动程序在新的 IRP 中分配其自己的 i/o 堆栈位置，则调度例程必须先调用 [**IoSetNextIrpStackLocation**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iosetnextirpstacklocation) ，然后再调用 [**IoGetCurrentIrpStackLocation**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetcurrentirpstacklocation) ，以在其自己的 [*IoCompletion*](/windows-hardware/drivers/ddi/wdm/nc-wdm-io_completion_routine) 例程的 i/o 堆栈位置中设置上下文。 有关详细信息，请参阅 [在中间级驱动程序中处理 irp](processing-irps-in-an-intermediate-level-driver.md)。

调度例程必须与原始 IRP 一起调用 [**也**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iomarkirppending) ，但不能调用任何驱动程序分配的 irp，因为 [*IoCompletion*](/windows-hardware/drivers/ddi/wdm/nc-wdm-io_completion_routine) 例程会释放它们。

如果调度例程正在为部分传输分配 Irp，并且基础设备驱动程序可以控制可移动媒体设备，则调度例程必须在其新分配的 Irp 中设置线程上下文，使其从原始 IRP 中的 **Tail** 。

可移动媒体设备的底层驱动程序可能会调用 [**IoSetHardErrorOrVerifyDevice**](/windows-hardware/drivers/ddi/ntddk/nf-ntddk-iosetharderrororverifydevice)，该驱动程序将引用 **irp- &gt; Tail**. " 如果驱动程序调用此支持例程，则文件系统驱动程序可以向相应的用户线程发送一个对话框，提示用户取消、重试或使驱动程序无法满足的操作失败。 有关详细信息，请参阅 [支持可移动介质](supporting-removable-media.md) 。

\_将驱动程序分配的所有 irp 发送到更低的驱动程序后，调度例程必须返回 "挂起" 状态。

在为原始 IRP 调用[**IoCompleteRequest**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocompleterequest)之前，驱动程序的[*IoCompletion*](/windows-hardware/drivers/ddi/wdm/nc-wdm-io_completion_routine)例程应该使用[**IoFreeIrp**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iofreeirp)释放所有驱动程序分配的 irp。 完成原始 IRP 后， *IoCompletion* 例程必须释放所有驱动程序分配的 irp，然后才能返回控制权。

每个更高级别的驱动程序会设置任何驱动程序分配的 (，并为低版本的驱动程序重用) Irp，无论给定请求来自中间驱动程序还是源自任何其他源（如文件系统或用户模式应用程序），都可以将其重要到基础设备驱动程序。

最高级别的驱动程序可以调用 [**IoMakeAssociatedIrp**](/windows-hardware/drivers/ddi/ntddk/nf-ntddk-iomakeassociatedirp) 来分配 irp，并为较低的驱动程序链设置它们。 只要驱动程序不会使用原始 IRP 或它分配的任何关联的 irp 调用 [**IoSetCompletionRoutine**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iosetcompletionroutine) ，i/o 管理器就会自动完成其所有关联的 irp。 然而，最高级别的驱动程序不得为请求缓冲 i/o 操作的任何 IRP 分配关联的 Irp。

中间级别驱动程序无法通过调用 **IoMakeAssociatedIrp**为低级驱动程序分配 irp。 中间驱动程序接收的任何 IRP 都可能已经是关联的 IRP，驱动程序不能将其他 IRP 与此类 IRP 关联。

相反，如果中间驱动程序为低级驱动程序创建了 Irp，则它应调用 [**IoAllocateIrp**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioallocateirp)、 [**IoBuildDeviceIoControlRequest**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iobuilddeviceiocontrolrequest)、 [**IoBuildSynchronousFsdRequest**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iobuildsynchronousfsdrequest)或 [**IoBuildAsynchronousFsdRequest**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iobuildasynchronousfsdrequest)。 但是，只能在以下情况下调用 **IoBuildSynchronousFsdRequest** ：

-   由驱动程序创建的线程为读取或写入请求构建 Irp，因为此类线程可以在 nonarbitrary 线程上下文中等待，因此在调度程序对象上 (自己的) ，如传递到**IoBuildSynchronousFsdRequest**的驱动程序初始化*事件*。

-   在初始化期间或卸载时在系统线程上下文中

-   为原本同步操作（如创建、刷新、关闭、关闭和设备控制请求）生成 Irp

但是，驱动程序更有可能调用 **IoBuildDeviceIoControlRequest** 来分配设备控制 irp，而不是 **IoBuildSynchronousFsdRequest**。

 

