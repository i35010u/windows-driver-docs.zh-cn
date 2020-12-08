---
title: 在驱动程序中创建 IOCTL 请求
description: 在驱动程序中创建 IOCTL 请求
keywords:
- I/o 控制代码 WDK 内核，创建请求
- 控制代码 WDK IOCTLs，创建请求
- IOCTLs WDK 内核，创建请求
- 同步 WDK Irp
- 嵌入指针 WDK IOCTLs
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 12bbde711a0259e8a26d87557e48f00a5b95cb1d
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96816091"
---
# <a name="creating-ioctl-requests-in-drivers"></a>在驱动程序中创建 IOCTL 请求





类驱动程序或其他较高级别的驱动程序可以为 i/o 控制请求分配 Irp，并将其发送到下一个较低的驱动程序，如下所示：

1.  使用主要的函数代码 [**IRP \_ mj \_ 设备 \_ 控制**](./irp-mj-device-control.md)或 [**IRP \_ mj \_ 内部 \_ 设备 \_ 控制**](./irp-mj-internal-device-control.md)分配或重复使用 i/o 请求数据包 ([**IRP**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_irp)) 。 可以使用 [**IoBuildDeviceIoControlRequest**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iobuilddeviceiocontrolrequest) 例程专门分配 IOCTL IRP。 你还可以使用常规用途 IRP 创建和初始化例程，如 [**IoAllocateIrp**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioallocateirp)、 [**IoReuseIrp**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioreuseirp)或 [**IoInitializeIrp**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioinitializeirp)。 有关 IRP 分配的详细信息，请参阅 [为 Lower-Level 驱动程序创建 irp](creating-irps-for-lower-level-drivers.md)。

2.  为 IRP 设置低级驱动程序的 i/o 堆栈位置，其中包含 IOCTL \_ *XXX* 代码和相应的参数。

3.  如果要异步完成 IOCTL 请求，请调用 [**KeInitializeEvent**](/windows-hardware/drivers/ddi/wdm/nf-wdm-keinitializeevent) 例程，以将事件对象初始化为通知事件。 驱动程序使用此事件等待 i/o 操作完成。

4.  使用 IRP 调用 [**IoSetCompletionRoutine**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iosetcompletionroutine) ，以便上部驱动程序可以提供 [*IoCompletion*](/windows-hardware/drivers/ddi/wdm/nc-wdm-io_completion_routine) 例程（如有必要）来执行以下操作：

    -   确定低级驱动程序如何处理给定的请求。

    -   在较低的驱动程序完成请求的操作之后，重新使用 IRP 发送其他请求或释放驱动程序创建的 IRP。 驱动程序无法重复使用 [**IoBuildDeviceIoControlRequest**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iobuilddeviceiocontrolrequest) 创建的 irp。 有关详细信息，请参阅 [重复使用 irp](reusing-irps.md)。

5.  调用 [**IoCallDriver**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver) ，将请求传递到低级驱动程序。

6.  如果 [**IoCallDriver**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver) 返回状态 \_ 挂起，则调用 [**KeWaitForSingleObject**](/windows-hardware/drivers/ddi/wdm/nf-wdm-kewaitforsingleobject) 例程将当前线程置于等待状态。 驱动程序将例程的 *Object* 参数设置为在对 [**KeInitializeEvent**](/windows-hardware/drivers/ddi/wdm/nf-wdm-keinitializeevent)的调用中初始化的事件对象的地址。

    **注意**  如果驱动程序调用 [**KeWaitForSingleObject**](/windows-hardware/drivers/ddi/wdm/nf-wdm-kewaitforsingleobject) ，并将其 *Timeout* 参数设置为 **NULL** 或包含非零值的变量的地址，则驱动程序必须 &lt; \_ 在 nonarbitrary 线程上下文中以 IRQL = APC 级别运行。 否则，驱动程序必须以 IRQL &lt; = 调度级别运行 \_ 。




当 IOCTL 请求完成时，事件由其 [*IoCompletion*](/windows-hardware/drivers/ddi/wdm/nc-wdm-io_completion_routine) 例程发出信号。 发出事件信号后，线程将继续执行。

**重要提示**  如果驱动程序将事件对象分配为堆栈上的局部变量，则驱动程序必须调用 [**KeWaitForSingleObject**](/windows-hardware/drivers/ddi/wdm/nf-wdm-kewaitforsingleobject) ，并将其 *WaitMode* 参数设置为 **KernelMode**。 此参数值可防止堆栈被调出。




为避免出现同步问题和可能的访问冲突，i/o 控制代码的参数很少包括嵌入指针。 除了某些 SCSI 请求之外，AssociatedIrp *的缓冲区* - &gt; **AssociatedIrp**。**SystemBuffer**，位于 *Irp* - &gt; **MdlAddress**，and at **参数**。**DeviceIoControl**。驱动程序的 i/o 堆栈位置中的 **Type3InputBuffer** 不包含指向其他数据缓冲区的指针，也不包含包含系统定义的 i/o 控制代码的指针的结构。 有关如何将数据缓冲区与包含 i/o 控制代码的 Irp 一起使用的详细信息，请参阅 [I/o 控制代码的缓冲区说明](buffer-descriptions-for-i-o-control-codes.md)。

尽管如此，定义内部 i/o 控制代码的一对类/端口驱动程序可以将嵌入式指针传递到从较高级别的驱动程序分配给驱动程序的内存。 这样一对类/端口驱动程序负责确保满足以下条件：

-   一次只能有一个驱动程序可以访问数据。

-   可以通过端口驱动程序在任意线程上下文中访问专用数据缓冲区。

显示驱动程序可以调用 GDI 函数 [**EngDeviceIoControl**](/windows/win32/api/winddi/nf-winddi-engdeviceiocontrol) ，通过系统视频端口驱动程序将专用定义的特定于设备的 i/o 控制请求以及系统定义的公共 i/o 控制请求发送到相应的特定于适配器的 [视频微型端口驱动程序](../display/video-miniport-drivers-in-the-windows-2000-display-driver-model.md)。

驱动程序包的任何用户模式组件都可以调用 [**DeviceIoControl**](/windows/win32/api/ioapiset/nf-ioapiset-deviceiocontrol) ，将 i/o 控制请求发送到驱动程序堆栈。 I/o 管理器创建 [**IRP \_ MJ \_ 设备 \_ 控制**](./irp-mj-device-control.md) 请求并将其传递到最高级别的驱动程序。
