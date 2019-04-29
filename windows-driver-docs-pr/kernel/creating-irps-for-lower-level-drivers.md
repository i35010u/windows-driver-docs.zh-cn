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
ms.openlocfilehash: a22064f49292ebefa6b6a29bc1c9db4813ba876d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63388255"
---
# <a name="creating-irps-for-lower-level-drivers"></a>为较低级驱动程序创建 IRP





若要为将由较低的驱动程序处理任意线程上下文中，一个异步请求分配 IRP [ *DispatchReadWrite* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)例程可以调用以下支持例程之一：

-   [**IoAllocateIrp**](https://msdn.microsoft.com/library/windows/hardware/ff548257)，可分配 IRP 和初始化为零的 I/O 堆栈位置数

    调度例程必须设置的新分配的 IRP 下, 一步低驱动程序的 I/O 堆栈位置通常由其自己的堆栈位置中原始 IRP 从复制 （可能已修改） 的信息。 如果更高级别的驱动程序分配其自己的新分配 IRP 的 I/O 堆栈位置，调度例程可以设置每个请求上下文信息存在[ *IoCompletion* ](https://msdn.microsoft.com/library/windows/hardware/ff548354)例程，以使用.

-   [**IoBuildAsynchronousFsdRequest**](https://msdn.microsoft.com/library/windows/hardware/ff548310)，该设置的调用方，根据调用方指定参数的下一步低驱动程序的 I/O 堆栈位置

    更高级别的驱动程序可以调用此例程来分配的 Irp [ **IRP\_MJ\_读取**](https://msdn.microsoft.com/library/windows/hardware/ff550794)， [ **IRP\_MJ\_编写**](https://msdn.microsoft.com/library/windows/hardware/ff550819)， [ **IRP\_MJ\_刷新\_缓冲区**](https://msdn.microsoft.com/library/windows/hardware/ff550760)，并[ **IRP\_MJ\_关机**](https://msdn.microsoft.com/library/windows/hardware/ff550807)请求。

    当[ *IoCompletion* ](https://msdn.microsoft.com/library/windows/hardware/ff548354)为此类 IRP 调用例程，它可以检查 I/O 状态块中，如果需要 （或可能），它将设置为下一步低驱动程序的 I/O 再次堆栈中的位置，然后重试请求或重复使用它。 但是， *IoCompletion*例程拥有任何本地上下文存储本身中 IRP，因此，驱动程序必须在常驻内存中其他位置维护有关原始请求的上下文。

-   [**IoMakeAssociatedIrp**](https://msdn.microsoft.com/library/windows/hardware/ff549397)，其中分配 IRP 和大量的 I/O 堆栈初始化为零的位置，并将关联与 IRP *master* IRP。

    中间驱动程序不能调用[ **IoMakeAssociatedIrp** ](https://msdn.microsoft.com/library/windows/hardware/ff549397)创建 Irp 的较低的驱动程序。

    任何调用的最高级别的驱动程序**IoMakeAssociatedIrp**若要为发送其关联的 Irp 和调用后，较低的驱动程序可以将控制返回到 I/O 管理器创建 Irp [ **IoMarkIrpPending**](https://msdn.microsoft.com/library/windows/hardware/ff549422)原始的主 IRP。 最高级别的驱动程序可以依赖于要完成的主 IRP 时所有关联的 Irp 都已由较低的驱动程序的 I/O 管理器。

    驱动程序很少设置[ *IoCompletion* ](https://msdn.microsoft.com/library/windows/hardware/ff548354)关联 IRP 的例程。 如果最高级别的驱动程序调用[ **IoSetCompletionRoutine** ](https://msdn.microsoft.com/library/windows/hardware/ff549679)为它创建关联 IRP，I/O 管理器不会完成主 IRP 如果驱动程序将返回状态\_详细\_处理\_从所需其*IoCompletion*例程。 在这些情况下，该驱动程序的*IoCompletion*例程必须显式完成与主 IRP [ **IoCompleteRequest**](https://msdn.microsoft.com/library/windows/hardware/ff548343)。

如果驱动程序分配其自己在新 IRP 的 I/O 堆栈位置，必须调用的调度例程[ **IoSetNextIrpStackLocation** ](https://msdn.microsoft.com/library/windows/hardware/ff550321)调用之前[ **IoGetCurrentIrpStackLocation** ](https://msdn.microsoft.com/library/windows/hardware/ff549174)若要为其自身 I/O 堆栈位置中设置上下文[ *IoCompletion* ](https://msdn.microsoft.com/library/windows/hardware/ff548354)例程。 有关详细信息，请参阅[中间级驱动程序中处理 Irp](processing-irps-in-an-intermediate-level-driver.md)。

必须调用的调度例程[ **IoMarkIrpPending** ](https://msdn.microsoft.com/library/windows/hardware/ff549422)原始 IRP，但不是与任何驱动程序分配 Irp，因为[ *IoCompletion* ](https://msdn.microsoft.com/library/windows/hardware/ff548354)例程将释放它们。

如果调度例程分配的部分传输的 Irp 和基础设备驱动程序可能会控制可移动介质设备，调度例程必须设置在其新分配的 Irp 的线程上下文处的值从**Tail.Overlay.Thread**中原始 IRP。

可移动媒体设备的基础驱动程序可能会调用[ **IoSetHardErrorOrVerifyDevice**](https://msdn.microsoft.com/library/windows/hardware/ff549707)，它引用在指针**Irp-&gt;Tail.Overlay.Thread**，为驱动程序分配 IRP。 如果驱动程序调用此支持例程，文件系统驱动程序可以发送到相应的用户线程，以提示用户取消、 重试，或失败的操作不能满足该驱动程序对话框。 请参阅[支持可移动介质](supporting-removable-media.md)有关详细信息。

调度例程必须返回状态\_后发送到较低的驱动程序的所有驱动程序分配 Irp 的待决。

驱动程序的[ *IoCompletion* ](https://msdn.microsoft.com/library/windows/hardware/ff548354)例程应释放使用的所有驱动程序分配 Irp [ **IoFreeIrp** ](https://msdn.microsoft.com/library/windows/hardware/ff549113)调用之前[**IoCompleteRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff548343)原始 IRP 的。 原始 IRP，完成*IoCompletion*例程必须释放所有驱动程序分配 Irp，才会返回控制。

每个更高级别的驱动程序设置了较低的驱动程序的方式，它并不重要到基础设备驱动程序是否某个给定的请求来自中间驱动程序或来自其他源，如文件的任何驱动程序分配 （和重用） Irp系统或用户模式应用程序。

最高级别的驱动程序可以调用[ **IoMakeAssociatedIrp** ](https://msdn.microsoft.com/library/windows/hardware/ff549397)分配 Irp，并将其设置为较低的驱动程序的链。 I/O 管理器自动完成原始 IRP 时已完成其所有关联的 Irp，只要该驱动程序不会调用[ **IoSetCompletionRoutine** ](https://msdn.microsoft.com/library/windows/hardware/ff549679)与原始 IRP 或任何关联的 Irp 的分配。 最高级别的驱动程序必须但是，关联的 Irp 为分配请求缓冲的 I/O 操作任何 IRP。

中间级驱动程序无法通过调用为较低级别的驱动程序分配 Irp **IoMakeAssociatedIrp**。 中间驱动程序将收到任何 IRP 可能已经有这些关联的 IRP，并驱动程序不能将另一个 IRP 与此类 IRP 关联。

相反，如果中间驱动程序的较低的驱动程序创建 Irp，则应调用[ **IoAllocateIrp**](https://msdn.microsoft.com/library/windows/hardware/ff548257)， [ **IoBuildDeviceIoControlRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff548318)， [ **IoBuildSynchronousFsdRequest**](https://msdn.microsoft.com/library/windows/hardware/ff548330)，或[ **IoBuildAsynchronousFsdRequest**](https://msdn.microsoft.com/library/windows/hardware/ff548310)。 但是， **IoBuildSynchronousFsdRequest**可以仅在以下情况下调用：

-   由驱动程序创建的线程，以生成 Irp 进行读取或写入请求，因为此类线程中可以等待 nonarbitrary 线程上下文 （自身） 上的调度程序对象，如驱动程序初始化*事件*传递给**IoBuildSynchronousFsdRequest**

-   在初始化期间或在卸载时在系统线程上下文中

-   若要生成 Irp 为本质上是同步操作，如创建、 刷新，关机、 关闭和设备控制请求

但是，驱动程序是更有可能调用**IoBuildDeviceIoControlRequest**分配设备控制 Irp 比**IoBuildSynchronousFsdRequest**。

 

 




