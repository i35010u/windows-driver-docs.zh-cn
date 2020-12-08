---
title: 示例 I/O 请求 - 详细信息
description: 示例 I/O 请求 - 详细信息
keywords:
- I/o 堆栈位置 WDK 内核
- 分层驱动程序 IRP 处理 WDK 内核
- 堆栈位置 WDK 内核
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0f26f53c9b66ef113774246357dfb5946cfdbff2
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96793591"
---
# <a name="example-io-request---the-details"></a>示例 I/O 请求 - 详细信息


## <a href="" id="ddk-example-i-o-request---the-details-kg"></a>


说明 "打开文件对象" 的图形显示具有两个 i/o 堆栈位置的 IRP，但 IRP 可以具有任意数量的 i/o 堆栈位置，具体取决于分层驱动程序处理给定请求的数量。

下图更详细地演示了 [打开文件对象](example-i-o-request---an-overview.md) 图中的驱动程序如何使用 i/o 支持例程 (**Io * Xxx*** 例程) 为读取或写入请求处理 IRP。

![说明如何处理分层驱动程序中的 irp 的关系图](images/2girpeg.png)

1. I/o 管理器 (FSD) 调用文件系统驱动程序，并将其分配给子系统的读/写请求。 FSD 访问 IRP 中的 i/o 堆栈位置，以确定应执行的操作。

2. FSD 可以通过调用 i/o 支持例程 ([**IoAllocateIrp**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioallocateirp)) 一次或多次来分配其他 irp，将原始请求拆分为较小) 的请求 (。 附加的 Irp 返回到 FSD，其中包含零填充 i/o 堆栈位置 (s) 用于低级驱动程序 () 。 为此，FSD 可以重复使用原始 IRP，而不是按上图所示分配其他 Irp，方法是在原始 IRP 中设置下一个较低的驱动程序 i/o 堆栈位置，并将其传递到较低的驱动程序。

3. 对于每个驱动程序分配的 IRP，上图中的 FSD 调用 i/o 支持例程来注册 FSD 提供的完成例程;在完成例程中，FSD 可以确定低级驱动程序是否满足请求，并可以在驱动程序完成后释放每个驱动程序分配的 IRP。 无论每个驱动程序分配的 IRP 是已成功完成、已完成并带有错误状态还是已取消，i/o 管理器都将调用 FSD 提供的完成例程。 较高级别的驱动程序负责释放它分配的任何 Irp，并为低级驱动程序自行设置。 在所有驱动程序均已完成后，i/o 管理器将释放它分配的 Irp。

   接下来，FSD 调用 i/o 支持例程 ([**IoGetNextIrpStackLocation**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetnextirpstacklocation)) 访问下一级驱动程序的 i/o 堆栈位置，以便为下一个较低版本的驱动程序设置请求。 上图中 (，下一个较低的驱动程序将成为最低级别的驱动程序。 ) FSD 然后调用 i/o 支持例程 ([**IoCallDriver**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver)) 将 IRP 传递到下一个较低的驱动程序。

4. 当使用 IRP 调用此方法时，最低级别的驱动程序将检查其 i/o 堆栈位置，以确定由 **irp \_ MJ \_ * XXX*** 函数代码指示 (哪个操作，) 应在目标设备上执行该操作。 目标设备在其指定 i/o 堆栈位置中由设备对象表示，并与 IRP 一起传递给驱动程序。 最低级别的驱动程序可以假定 i/o 管理器已将 IRP 路由到为 **irp \_ mj \_ * XXX*** 操作定义驱动程序的入口点 (此处为 Irp mj [**\_ \_ READ**](./irp-mj-read.md) 或 [**IRP \_ mj \_ 写入**](./irp-mj-write.md)) ，以及更高级别的驱动程序已检查请求的其他参数的有效性。

   如果没有更高级别的驱动程序，最低级别的驱动程序将检查 **IRP \_ MJ \_ * XXX*** 操作的输入参数是否有效。 如果是这样，则驱动程序通常会调用 i/o 支持例程来告知 i/o 管理器设备操作在 IRP 上处于挂起状态，并将 IRP 传递给 IRP，或将它传递到另一个驱动程序提供的用于访问目标设备 (（物理或逻辑设备）的例程：磁盘或磁盘上的分区) 。

5. I/o 管理器确定驱动程序是否正在忙于处理目标设备的其他 IRP，如果是，则将 IRP 排队，并返回。 否则，i/o 管理器会将 IRP 路由到驱动程序提供的例程，该例程在其设备上启动 i/o 操作。  (在此阶段，上图中的两个驱动程序和 i/o 管理器都返回 control。 ) 

6. 当设备中断时，驱动程序的中断服务例程 (ISR) 只是为了使设备不再中断，并保存必要的操作上下文。 然后，ISR 通过 IRP 调用 i/o 支持例程 ([**IoRequestDpc**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iorequestdpc)) ，并使用 IRP 将驱动程序提供的 DPC 排队 (延迟的过程调用) 例程，以在低于 ISR 的硬件优先级完成请求的操作。

7. 当驱动程序的 DPC 获得控制时，它将使用在 ISR 对 [**IoRequestDpc**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iorequestdpc)) 的调用中传递的上下文 (来完成 i/o 操作。 如果任何) 并将 IRP 传递到驱动程序提供的用于启动设备上的 i/o 操作的例程，则 DPC 会调用支持例程来取消对下一个 IRP (的排队 (请参阅步骤 5) 。 然后，DPC 在 IRP 的 i/o 状态块中设置有关刚完成操作的状态，并将其返回到带有 [**IoCompleteRequest**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocompleterequest)的 i/o 管理器。

8. I/o 管理器 0 IRP 中最低级别驱动程序的 i/o 堆栈位置，并调用文件系统的已注册完成例程 (参见步骤3与 FSD 分配的 IRP) 。 此完成例程检查 i/o 状态块，以确定是重试请求还是更新对原始请求维护的任何内部状态，并释放其驱动程序分配的 IRP。 文件系统可以收集其发送到较低级别驱动程序的所有驱动程序分配的 Irp 的状态信息，以便能够设置 i/o 状态并完成原始 IRP。 当文件系统已完成原始 IRP 时，i/o 管理器会将和 NTSTATUS 值返回给原始请求方 (子系统的本机函数) i/o 操作。

与在 [分层驱动程序的处理 irp](#ddk-example-i-o-request---the-details-kg) 中显示的文件系统驱动程序一样，添加到现有驱动程序链中的任何新驱动程序都可以执行以下操作：

-   将其自己的完成例程设置为 IRP。 [*IoCompletion*](/windows-hardware/drivers/ddi/wdm/nc-wdm-io_completion_routine)例程检查 i/o 状态块，以确定低级驱动程序是否已成功完成 irp，是否取消了 irp，并/或是否已完成，但出现了错误。 完成例程还可以更新驱动程序可能已保存的任何 IRP 特定的状态，并在完成 IRP 之前释放驱动程序可能已分配的任何特定于操作的资源等。 此外，完成例程可以通过通知 i/o 管理器在 IRP) 上需要更多处理来推迟 IRP 完成 (，并可以在允许 IRP 完成之前将另一个请求发送到下一个较低级别的驱动程序。

-   在它分配的 Irp 中设置下一个较低级别的驱动程序的 i/o 堆栈位置，并将请求发送到下一个较低级别的驱动程序。

-   通过在每个 IRP 中设置下一个较低的驱动程序的 i/o 堆栈位置并调用 [**IoCallDriver**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver)，将中的任何传入请求传递到更低的驱动程序。  (请注意，对于具有主要功能代码 [**IRP \_ MJ \_ 功能**](./irp-mj-power.md)的 irp，驱动程序必须使用 [**PoCallDriver**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-pocalldriver)。 ) 

每个驱动程序创建的设备对象表示一个物理设备、逻辑设备或虚拟设备，特定驱动程序会对该设备执行 i/o 请求。 有关创建和设置设备对象的详细信息，请参阅 [设备对象和设备堆栈](introduction-to-device-objects.md)。

由于 [分层驱动程序中的处理 irp](#ddk-example-i-o-request---the-details-kg) 还显示，大多数驱动程序通过驱动程序提供的一组由系统定义的 *标准例程* 来处理每个 IRP，而链中不同级别的驱动程序必须具有不同的标准例程。 例如，只有最低级别的驱动程序处理来自物理设备的中断，因此，只有最低级别的驱动程序才能有 ISR 和用于完成中断驱动 i/o 操作的 DPC。 另一方面，因为此类驱动程序知道当 i/o 从其设备接收到一个中断时，它不需要完成例程。 只有较高级别的驱动程序具有一个或多个完成例程，如此图中的 FSD。

 

