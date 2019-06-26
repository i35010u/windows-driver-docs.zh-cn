---
title: 示例 I/O 请求 - 详细信息
description: 示例 I/O 请求 - 详细信息
ms.assetid: 480db6a1-2a13-4f1a-87ff-c3bd37aa79be
keywords:
- I/O 堆栈位置 WDK 内核
- 分层驱动程序 IRP 处理 WDK 内核
- 堆栈位置 WDK 内核
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 27dc594d26435f5b1d71a9542c57c837dd5106ac
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385117"
---
# <a name="example-io-request---the-details"></a>示例 I/O 请求 - 详细信息


## <a href="" id="ddk-example-i-o-request---the-details-kg"></a>


说明如何打开文件对象图显示了具有两个 I/O 堆栈位置 IRP 但 IRP 可以有任意数量的 I/O 堆栈位置，具体取决于多少分层驱动程序将处理给定的请求。

下图更详细地说明了如何在驱动程序[打开文件对象](example-i-o-request---an-overview.md)图使用 I/O 支持例程 (**Io * Xxx*** 例程) 处理 IRP 进行读取或写入请求。

![说明处理 irp 分层驱动程序中的关系图](images/2girpeg.png)

1. I/O 管理器调用的 IRP 它已经分配了子系统的读/写请求的文件系统驱动程序 (FSD)。 FSD 访问其在 IRP，以确定它应执行哪些操作的 I/O 堆栈位置。

2. FSD 可以将原始请求分为较小的请求 （可能是适用于多个设备驱动程序） 通过调用 I/O 支持例程 ([**IoAllocateIrp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioallocateirp)) 一个或多个要分配其他 Irp 的时间。 其他 Irp 将返回到 FSD 与低级驱动程序为零填充 I/O 堆栈的位置。 其判断 FSD 可以重复使用原始 IRP，而不是分配其他 Irp 设置下一步低驱动程序的 I/O 堆栈位置中原始 IRP 并将其传递到较低的驱动程序上图中所示。

3. 对于每个驱动程序分配 IRP，在上一图调用 I/O FSD 支持例程，以注册一个 FSD 提供完成例程;在完成例程中，FSD 可以确定低级驱动程序是否满足该请求，并且在较低的驱动程序都完成后，可以释放每个驱动程序分配的 IRP。 是否已成功完成、 已完成，但错误状态，或取消每个驱动程序分配的 IRP，I/O 管理器将调用 FSD 提供完成例程。 更高级别的驱动程序负责释放任何 Irp 分配和设置较低级别的驱动程序代表其自身。 I/O 管理器释放它毕竟会分配 Irp 驱动程序已完成它们。

   FSD 接下来，调用的 I/O 支持例程 ([**IoGetNextIrpStackLocation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iogetnextirpstacklocation)) 若要设置为下一步低驱动程序请求访问下一步低级驱动程序的 I/O 堆栈位置。 （在上图中下, 一个较低的驱动程序恰好是最低级别驱动程序。）FSD 然后调用 I/O 支持例程 ([**IoCallDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocalldriver)) 要传递到下一步低驱动程序该 IRP。

4. 最低级别驱动程序与 IRP 调用它时，检查其 I/O 堆栈位置来确定哪些操作 (由**IRP\_MJ\_* XXX*** 函数代码) 它应在目标设备上执行。 目标设备由其指定的 I/O 堆栈位置中的设备对象表示，并使用 IRP 传递给驱动程序。 最低级别驱动程序可以假设 I/O 管理器已路由到为定义该驱动程序的入口点 IRP **IRP\_MJ\_* XXX*** 操作 (此处[ **IRP\_MJ\_读取**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-read)或[ **IRP\_MJ\_编写**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-write)) 和更高级别的驱动程序已检查的有效性请求的其他参数。

   如果没有任何更高级别的驱动程序，最低级别驱动程序会检查是否为输入的参数**IRP\_MJ\_* XXX*** 操作是有效。 如果是，该驱动程序通常调用 I/O 支持例程，从而告知 I/O 管理器的设备操作处于挂起状态上 IRP 和以排队 IRP 或将其传递到另一个访问 （此处的目标设备的驱动程序提供的例程物理或逻辑设备： 磁盘或磁盘上的分区)。

5. I/O 管理器确定驱动程序是否已忙于处理另一个 IRP 为目标设备，如果是，并返回 IRP 队列。 否则，I/O 管理器将 IRP 路由到启动 I/O 操作在其设备上的驱动程序所提供的例程。 （在此阶段上, 图和 I/O 管理器中的这两个驱动程序返回控制。）

6. 当设备中断时，驱动程序的中断服务例程 (ISR) 执行唯一随着作为得多工作，必须停止从中断的设备并将保存有关操作的必要上下文。 然后，ISR 调用的 I/O 支持例程 ([**IoRequestDpc**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iorequestdpc)) 与 IRP 排队驱动程序提供的 DPC （延迟过程调用） 例程来完成请求的操作在较低的硬件优先级比 ISR

7. 当驱动程序的 DPC 获取控件时，它使用的上下文 (ISR 的调用中传递[ **IoRequestDpc**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iorequestdpc)) 来完成 I/O 操作。 DPC 调用取消下一步 IRP 排队 （如果有） 并将传递到启动 I/O 操作在设备上的驱动程序所提供的例程的 IRP 的支持例程 （请参阅第 5 步）。 DPC 然后 IRP 的 I/O 状态块中设置有关刚完成操作的状态并将其返回给与 I/O 管理器[ **IoCompleteRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocompleterequest)。

8. I/O 管理器中 IRP 的最低级别驱动程序的 I/O 堆栈位置零的处理方法，并调用文件系统的已注册的完成例程 （请参阅步骤 3） 与 FSD 分配 IRP。 此完成例程将检查以确定是否要重试请求或更新维护有关原始请求的任何内部状态并释放其驱动程序分配的 IRP 的 I/O 状态块。 文件系统可以收集，以便它可以将 I/O 状态设置并完成原始 IRP 发送到较低级别的驱动程序的所有驱动程序分配 Irp 的状态信息。 当文件系统已完成原始 IRP，I/O 管理器返回和 NTSTATUS 值与 I/O 操作的原始请求者 （子系统的本机函数）。

像文件系统驱动程序中所示[分层驱动程序中处理 Irp](#ddk-example-i-o-request---the-details-kg)图，任何新的驱动程序添加到现有的驱动程序的链可以执行所有以下操作：

-   设置到 IRP 自己完成例程。 [ *IoCompletion* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-io_completion_routine)例程检查 I/O 状态块，以确定是否较低的驱动程序已成功完成 IRP、 取消 IRP，和/或完成并出现错误。 完成例程还可以更新任何 IRP 特定状态可能已保存驱动程序，释放驱动程序可能已分配，任何特定于操作的资源和等完成 IRP 之前。 此外，完成例程可以推迟 IRP 完成 （通过告知 I/O 管理器 IRP 需要更多的处理），并可以将发送另一个请求到下一步低级驱动程序允许 IRP 完成之前。

-   设置下一步低级驱动程序的 I/O 堆栈位置中它会分配的 Irp，并将请求发送到下一步低级驱动程序。

-   将任何传入请求低级驱动程序通过设置每个 IRP 和调用中的下一步低驱动程序的 I/O 堆栈位置传递给[ **IoCallDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocalldriver)。 (请注意，对于 Irp，主要函数代码[ **IRP\_MJ\_POWER**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-power)，驱动程序必须使用[ **PoCallDriver** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-pocalldriver).)

每个驱动程序创建的设备对象表示为其特定的驱动程序执行输入/输出请求的物理、 逻辑，或虚拟设备。 有关创建和设置的设备对象的详细信息，请参阅[设备对象和设备堆栈](device-objects-and-device-stacks.md)。

作为[分层驱动程序中处理 Irp](#ddk-example-i-o-request---the-details-kg)图还显示，大多数驱动程序中通过驱动程序提供一系列系统定义的阶段处理每个 IRP*标准例程*，但在不同的驱动程序在一个链中的级别一定具有不同的标准例程。 例如，仅最低级别的驱动程序句柄中断从物理设备，因此，只有一个最低级别驱动程序将具有 ISR 和完成中断驱动 I/O 操作 DPC。 但是，因为这样的驱动程序知道它从其设备接收中断时的 I/O 已完成，它具有无需完成例程。 更高级别的驱动程序将在此图中具有一个或多个完成例程，如 FSD。

 

 




