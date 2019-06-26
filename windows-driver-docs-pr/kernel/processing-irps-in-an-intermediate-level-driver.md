---
title: 在中间级驱动程序中处理 IRP
description: 在中间级驱动程序中处理 IRP
ms.assetid: 7606ab1b-68af-4d27-8668-7662969b85b8
keywords:
- Irp WDK 内核，处理示例
- IoCompletion 例程
- IoSetCompletionRoutine
- 镜像驱动程序 WDK Irp
- 分配 Irp
- IoCallDriver
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 321187a8ef0056776c6c3a46bb9733970c061a88
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67378801"
---
# <a name="processing-irps-in-an-intermediate-level-driver"></a>在中间级驱动程序中处理 IRP





更高级别的驱动程序具有不同的一组标准例程比最低级别的设备驱动程序，使用这两种类型的驱动程序通用的标准例程重叠子集。

例程的中间和最高级别的驱动程序组根据以下条件各不相同：

-   基础物理设备特性

-   是否基础的设备驱动程序设置的设备对象的直接或缓冲 I/O

-   单独的更高级别的驱动程序的设计

下图说明了 IRP 可能需要通过中间的标准例程的路径*镜像驱动程序*上层的某个位置上一节中所述的最低级别的设备驱动程序。

下图中所示的驱动程序具有以下特征：

-   通过多个物理设备和可能是多个设备驱动程序，该驱动程序是分层结构。

-   驱动程序有时会附加 Irp 分配较低级别的驱动程序，具体取决于输入 IRP 中请求的操作。

-   该驱动程序具有至少一个文件系统驱动程序，它的上面，该文件系统驱动程序可能上层比这个较高级别上其他中间驱动程序。

### <a href="" id="irp-path-through-intermediate-driver-routines"></a>

![说明通过中间驱动程序例程的 irp 途径的关系图](images/4hiddirp.png)

如图所示，I/O 管理器创建 IRP，并将其发送到给定的主要函数代码的驱动程序的调度例程。 假设函数代码是[ **IRP\_MJ\_编写**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-write)，调度例程**DDDispatchWrite**。 在中间，与更高版本和较低级别驱动程序显示带阴影的 I/O 堆栈位置数量不确定显示中间驱动程序的 I/O 堆栈位置。

### <a href="" id="allocating-irps-"></a>分配 Irp

镜像驱动程序的用途是将写入请求发送到多台物理设备，并将读取的请求或者发送到这些设备的驱动程序。 写入请求，驱动程序创建重复 Irp 为每个设备的数据是能够进行编写，假设在 IRP 的输入参数有效。

上图演示如何调用[ **IoAllocateIrp** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioallocateirp)但更高级别的驱动程序可以调用其他支持例程，以将 Irp 分配较低级别的驱动程序。 请参阅[的较低级驱动程序创建 Irp](creating-irps-for-lower-level-drivers.md)。

当调用的调度例程**IoAllocateIrp**，它指定所需的 IRP 的 I/O 堆栈位置数。 该驱动程序必须链，每个驱动程序正下方的镜像驱动程序的设备对象从获取适当的值中指定每个较低的驱动程序的堆栈位置。 （可选） 该驱动程序可以添加一个为此值时，它调用**IoAllocateIrp**若要获取与上图中的驱动程序分配，其自己的每个 IRP 的堆栈位置。

此中间驱动程序的调度例程调用[ **IoGetCurrentIrpStackLocation** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iogetcurrentirpstacklocation) （未显示） 与原始 IRP，用于检查参数。

它将调用[ **IoSetNextIrpStackLocation** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iosetnextirpstacklocation)因为它分配了其自己的堆栈位置中每个新创建的 IRP 和[ **IoGetCurrentIrpStackLocation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iogetcurrentirpstacklocation)为自身它使用更高版本中创建的上下文[ *IoCompletion* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-io_completion_routine)例程。

接下来，调用[ **IoGetNextIrpStackLocation** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iogetnextirpstacklocation)与每个新创建的 IRP，以便它可以将它分配的 Irp 中的下一步的较低级驱动程序的 I/O 堆栈位置设置。 镜像驱动程序的调度例程将 IRP 函数代码和参数 (指向传输缓冲区的指针，以字节为单位传输的长度**IRP\_MJ\_编写**) 到 I/O 堆栈的位置下一步较低的驱动程序。 这些驱动程序，将反过来会立刻设置正下方，驱动程序的 I/O 堆栈位置，如果有的话。

### <a name="calling-iosetcompletionroutine-and-iocalldriver"></a>调用 IoSetCompletionRoutine 和 IoCallDriver

在上一图调用中的调度例程[ **IoSetCompletionRoutine** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iosetcompletionroutine)为它分配每个 IRP。 上图中的驱动程序必须释放它分配的 Irp，因为此驱动程序将设置其*IoCompletion*例程时要调用低级驱动程序完成其 Irp，是否已成功完成，I/O 操作失败，或已取消。

由于并行反映了上图中的驱动程序，它将它分配到下一步低级驱动程序通过调用这两个 Irp [ **IoCallDriver** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocalldriver)两次，一次针对每个目标设备表示一个镜像的分区对象。

### <a name="processing-irps-in-the-drivers-iocompletion-routine"></a>在驱动程序的 IoCompletion 例程处理 Irp

I/O 管理器的较低级驱动程序的设置完成请求的操作，调用中间镜像驱动程序*IoCompletion*例程。 镜像驱动程序将保持在跟踪时的较低的驱动程序已完成所有重复的 Irp 原始 IRP 自己 I/O 堆栈位置计数。

假设 I/O 状态块表示一组较低的驱动程序已完成重复 IRP 中所示[上图](#irp-path-through-intermediate-driver-routines)，在镜像驱动程序*IoCompletion*例程递减其计数但不能完成原始 IRP 之前递减计数归零。 如果递减计数还不是零， *IoCompletion*例程调用[ **IoFreeIrp** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iofreeirp)与第一个返回 IRP (DupIRP1 在上图中) 的驱动程序分配并返回状态\_更多\_处理\_必需。

时镜像驱动程序*IoCompletion*与上图中所示 DupIRP2 再次调用例程*IoCompletion*例程递减中原始 IRP 的计数，并确定的同时所请求的操作已执行的较低级驱动程序集。

此外假设 DupIRP2 中的 I/O 状态块设置有状态\_成功后， *IoCompletion*例程将 I/O 状态块从 DupIRP2 复制到原始 IRP 并释放 DupIRP2。 它将调用[ **IoCompleteRequest** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocompleterequest)保留原始的 IRP 和返回状态\_详细\_处理\_必需。 返回此状态可防止在 I/O 管理器尝试 DupIRP2; 上的处理任何进一步完成IRP 不与线程关联，因为其完成处理应结尾创建它的驱动程序。

如果任何一个的较低级驱动程序集不会成功，完成镜像驱动程序的 Irp 镜像驱动程序*IoCompletion*例程应记录错误和尝试的相应镜像数据恢复。 有关详细信息，请参阅[日志记录错误](logging-errors.md)。

 

 




