---
title: 在驱动程序中创建 IOCTL 请求
description: 在驱动程序中创建 IOCTL 请求
ms.assetid: 155e2577-0e9a-4c0b-a25a-8516ce3de631
keywords:
- I/O 控制代码 WDK 内核，创建请求
- 控制代码 WDK Ioctl，创建请求
- Ioctl WDK 内核，创建请求
- 同步 WDK Irp
- 嵌入式的指针 WDK Ioctl
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: f7484e66ea127da239c2c080d460c463d3f3b62d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56555675"
---
# <a name="creating-ioctl-requests-in-drivers"></a>在驱动程序中创建 IOCTL 请求





类驱动程序或其他更高级别的驱动程序可以为输入/输出控制请求分配 Irp，并将其发送到下一步低驱动程序，如下所示：

1.  分配或重复使用的 I/O 请求数据包 ([**IRP**](https://msdn.microsoft.com/library/windows/hardware/ff550694))，主要函数代码[ **IRP\_MJ\_设备\_控件**](https://msdn.microsoft.com/library/windows/hardware/ff550744)或[ **IRP\_MJ\_内部\_设备\_控件**](https://msdn.microsoft.com/library/windows/hardware/ff550766)。 可以使用[ **IoBuildDeviceIoControlRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff548318)例程，以专门分配 IOCTL IRP。 此外可以使用常规用途的 IRP 创建和初始化例程，如[ **IoAllocateIrp**](https://msdn.microsoft.com/library/windows/hardware/ff548257)， [ **IoReuseIrp**](https://msdn.microsoft.com/library/windows/hardware/ff549661)，或[**IoInitializeIrp**](https://msdn.microsoft.com/library/windows/hardware/ff549315)。 有关 IRP 分配的详细信息，请参阅[较低级别驱动程序创建 Irp](creating-irps-for-lower-level-drivers.md)。

2.  设置较低的驱动程序的 I/O 堆栈位置与 IOCTL IRP\_*XXX*代码并将相应的参数。

3.  如果 IOCTL 请求是要以异步方式完成，则调用[ **KeInitializeEvent** ](https://msdn.microsoft.com/library/windows/hardware/ff552137)例程，以初始化为通知事件的事件对象。 该驱动程序使用此事件来等待 I/O 操作完成。

4.  调用[ **IoSetCompletionRoutine** ](https://msdn.microsoft.com/library/windows/hardware/ff549679)与 IRP，以便可以提供上限的驱动程序[ *IoCompletion* ](https://msdn.microsoft.com/library/windows/hardware/ff548354)例程，如有必要，以执行操作以下内容：

    -   确定较低的驱动程序如何处理给定的请求。

    -   重用 IRP 发送另一个请求或驱动程序创建 IRP，较低的驱动程序完成请求的操作后释放。 该驱动程序不能重复使用 Irp， [ **IoBuildDeviceIoControlRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff548318)创建。 有关详细信息，请参阅[重用 Irp](reusing-irps.md)。

5.  调用[ **IoCallDriver** ](https://msdn.microsoft.com/library/windows/hardware/ff548336)以将请求传递到较低的驱动程序。

6.  如果[ **IoCallDriver** ](https://msdn.microsoft.com/library/windows/hardware/ff548336)返回状态\_挂起状态，调用[ **KeWaitForSingleObject** ](https://msdn.microsoft.com/library/windows/hardware/ff553350)例程，以将当前进入等待状态的线程。 驱动程序设置的例程*对象*参数对的调用中初始化的事件对象的地址[ **KeInitializeEvent**](https://msdn.microsoft.com/library/windows/hardware/ff552137)。

    **请注意**如果该驱动程序调用[ **KeWaitForSingleObject** ](https://msdn.microsoft.com/library/windows/hardware/ff553350)使用其*超时*参数设置为**NULL**或包含一个非零值，该驱动程序的变量的地址必须运行在 IRQL &lt;= APC\_级别 nonarbitrary 线程上下文中。 否则，该驱动程序必须运行在 IRQL &lt;= 调度\_级别。




事件信号通过其[ *IoCompletion* ](https://msdn.microsoft.com/library/windows/hardware/ff548354)例程时 IOCTL 请求已完成。 一旦该事件发出信号，线程恢复执行。

**重要**如果该驱动程序为本地变量在堆栈上分配的事件对象，该驱动程序必须调用[ **KeWaitForSingleObject** ](https://msdn.microsoft.com/library/windows/hardware/ff553350)使用其*WaitMode*参数设置为**KernelMode**。 此参数值可防止正在换出堆栈。




若要避免同步问题和可能的访问冲突，I/O 控制代码的参数很少包含嵌入式的指针。 对于某些除外 SCSI 请求，在缓冲区*Irp*-&gt;**AssociatedIrp**。**SystemBuffer**，在*Irp*-&gt;**MdlAddress**，而是在**参数**。**DeviceIoControl**。**Type3InputBuffer**驱动程序的 I/O 堆栈中位置不包含指向其他数据缓冲区，也不包含结构中包含的系统定义的 I/O 控制代码的指针。 详细了解与包含 I/O 的 Irp 结合数据缓冲区的方式控制代码，请参阅[I/O 控制代码的缓冲区说明](buffer-descriptions-for-i-o-control-codes.md)。

不过，定义内部的 I/O 控制代码的类/端口驱动程序的一对可以嵌入的指针驱动程序分配的内存将从传递到更高级别的驱动程序添加到较低级别驱动程序。 此类的类/端口驱动程序对负责确保以下条件为真：

-   一次只有一个驱动程序可以访问的数据。

-   可在端口驱动程序的任意线程上下文中访问私有数据缓冲区。

显示器驱动程序可以调用 GDI 函数[ **EngDeviceIoControl** ](https://msdn.microsoft.com/library/windows/hardware/ff564838)通过发送私人定义、 特定于设备的 I/O 控制请求，以及系统定义公共 I/O 控制请求，以在向相应的适配器特定的系统的视频端口驱动程序[微型端口驱动程序](https://msdn.microsoft.com/library/windows/hardware/ff570509)。

驱动程序包的任何用户模式组件可以调用[ **DeviceIoControl** ](https://msdn.microsoft.com/library/windows/desktop/aa363216)将发送到驱动程序堆栈的 I/O 控制请求。 I/O 管理器创建[ **IRP\_MJ\_设备\_控制**](https://msdn.microsoft.com/library/windows/hardware/ff550744)请求并将其提供给最高级别的驱动程序。








