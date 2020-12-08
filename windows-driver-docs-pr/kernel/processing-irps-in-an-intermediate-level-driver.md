---
title: 在中间级驱动程序中处理 IRP
description: 在中间级驱动程序中处理 IRP
keywords:
- Irp WDK 内核，处理示例
- IoCompletion 例程
- IoSetCompletionRoutine
- 镜像驱动程序 WDK Irp
- 分配 Irp
- IoCallDriver
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 845ce23e3fda57f6a23cd5dde2bf935f9b532ccb
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96805409"
---
# <a name="processing-irps-in-an-intermediate-level-driver"></a>在中间级驱动程序中处理 IRP





较高级别的驱动程序具有一组不同于最低级别设备驱动程序的标准例程，并具有对这两种类型的驱动程序通用的标准例程的重叠子集。

中间层和高级驱动程序的例程集也会根据以下条件而有所不同：

-   底层物理设备的性质

-   基础设备驱动程序是否为直接或缓冲 i/o 设置设备对象

-   单个较高级别的驱动程序的设计

下图说明了 IRP 可以通过在上一部分所述的最低级别设备驱动程序中的某个位置，通过中间 *镜像驱动程序* 的标准例程来执行的路径。

下图中所示的驱动程序具有以下特征：

-   该驱动程序在多个物理设备上分层，并可能跨多个设备驱动程序。

-   有时，驱动程序会根据输入 IRP 中请求的操作为较低级别的驱动程序分配其他 Irp。

-   驱动程序上至少有一个包含的文件系统驱动程序，并且该文件系统驱动程序可能与此文件系统驱动程序在更高级别的中间驱动程序上分层。

### <a href="" id="irp-path-through-intermediate-driver-routines"></a>

![通过中间驱动程序例程说明 irp 路径的关系图](images/4hiddirp.png)

如图所示，i/o 管理器会创建一个 IRP，并将其发送到给定主要函数代码的驱动程序调度例程。 假设函数代码为 [**IRP \_ MJ \_ 写入**](./irp-mj-write.md)，则调度例程为 **DDDispatchWrite**。 中间驱动程序的 i/o 堆栈位置在中间显示，对于较高和较低级别的驱动程序，显示阴影的 i/o 堆栈位置数量不定。

### <a name="allocating-irps"></a><a href="" id="allocating-irps-"></a>分配 Irp

镜像驱动程序的目的是将写入请求发送到多个物理设备，并将读取请求交替发送到这些设备的驱动程序。 对于写入请求，驱动程序会为要写入数据的每个设备创建重复的 Irp，前提是输入 IRP 中的参数有效。

上图显示了对 [**IoAllocateIrp**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioallocateirp) 的调用，但较高级别的驱动程序可以调用其他支持例程为较低级别的驱动程序分配 irp。 请参阅 [为 Lower-Level 驱动程序创建 irp](creating-irps-for-lower-level-drivers.md)。

当调度例程调用 **IoAllocateIrp** 时，它会指定 IRP 所需的 i/o 堆栈位置数量。 驱动程序必须为链中的每个较低驱动程序指定堆栈位置，并从镜像驱动程序正下方的每个驱动程序的设备对象中获取相应的值。 或者，当驱动程序调用 **IoAllocateIrp** 为其分配的每个 IRP 获取自己的堆栈位置时，驱动程序可以将一个添加到此值，如上图中的驱动程序所述。

此中间驱动程序的调度例程将调用 [**IoGetCurrentIrpStackLocation**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetcurrentirpstacklocation) (未显示原始 IRP) ，以检查参数。

它调用 [**IoSetNextIrpStackLocation**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iosetnextirpstacklocation) ，因为它在每个新建的 IRP 和 [**IoGetCurrentIrpStackLocation**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetcurrentirpstacklocation) 中分配了自己的堆栈位置，以创建它在稍后在 [*IoCompletion*](/windows-hardware/drivers/ddi/wdm/nc-wdm-io_completion_routine) 例程中使用的上下文。

接下来，它为每个新创建的 IRP 调用 [**IoGetNextIrpStackLocation**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetnextirpstacklocation) ，以便它可以在其分配的 irp 中设置下一个较低级别的驱动程序的 i/o 堆栈位置。 镜像驱动程序的调度例程将 IRP 函数代码和参数 (指针复制到传输缓冲区，并将为 **IRP \_ MJ \_ 写入**) 传输的长度（以字节为单位）复制到下一个较低驱动程序的 i/o 堆栈位置。 这些驱动程序进而会为位于其下的驱动程序设置 i/o 堆栈位置（如果有）。

### <a name="calling-iosetcompletionroutine-and-iocalldriver"></a>调用 IoSetCompletionRoutine 和 IoCallDriver

上图中的调度例程为它分配的每个 IRP 调用 [**IoSetCompletionRoutine**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iosetcompletionroutine) 。 由于上图中的驱动程序必须释放它所分配的 Irp，因此，当驱动程序完成其 Irp 时，无论 i/o 操作是否成功完成、失败或已取消，此驱动程序都将设置其 *IoCompletion* 例程。

由于上图中的驱动程序会以并行方式镜像，因此它通过两次调用 [**IoCallDriver**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver) 将它分配到的两个 irp 传递到下一个较低级别的驱动程序，每个目标设备对象表示一个镜像分区。

### <a name="processing-irps-in-the-drivers-iocompletion-routine"></a>处理驱动程序的 IoCompletion 例程中的 Irp

当其中一组低级驱动程序完成请求的操作时，i/o 管理器将调用中间镜像驱动程序的 *IoCompletion* 例程。 镜像驱动程序在其自己的 i/o 堆栈位置中维护原始 IRP 的计数，以跟踪较低的驱动程序何时完成所有重复的 Irp。

假设 i/o 状态块表明一组较小的驱动程序已经完成了 [上图](#irp-path-through-intermediate-driver-routines)中所示的重复 irp，镜像驱动程序的 *IoCompletion* 例程会减少其计数，但无法完成原始 irp，直到它将计数递减到零。 如果减少的计数不为零，则 *IoCompletion* 例程将在上一个图中与第一个返回的 IRP (DupIRP1 一起调用 [**IoFreeIrp**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iofreeirp) ，) 分配的驱动程序并返回状态 " \_ 需要的更多 \_ 处理" \_ 。

当使用上图中所示的 DupIRP2 再次调用镜像驱动程序的 *IoCompletion* 例程时， *IoCompletion* 例程将减少原始 IRP 中的计数，并确定两组较低级别的驱动程序是否已执行请求的操作。

假设 DupIRP2 中的 i/o 状态块也设置为 "成功" 状态 \_ ，则 *IoCompletion* 例程会将 i/o 状态块从 DupIRP2 复制到原始 IRP，并释放 DupIRP2。 它与原始 IRP 一起调用 [**IoCompleteRequest**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocompleterequest) ，并返回 \_ 所需的状态更多 \_ 处理 \_ 。 返回此状态会阻止 i/o 管理器尝试在 DupIRP2 上执行任何进一步的完成处理;因为 IRP 不与线程关联，所以它的完成处理应以创建它的驱动程序结束。

如果一组较低级别的驱动程序无法成功完成镜像驱动程序的 Irp，镜像驱动程序的 *IoCompletion* 例程应记录一个错误并尝试适当的镜像数据恢复。 有关详细信息，请参阅 [日志记录错误](logging-errors.md)。

 

