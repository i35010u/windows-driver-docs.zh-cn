---
title: 注册 IoCompletion 例程
description: 注册 IoCompletion 例程
ms.assetid: 413d8463-b2ce-44b6-846c-f853b5cd580e
keywords:
- IoCompletion 例程
- 注册 IoCompletion 例程
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 981e8874a97ef95715db99c01c2b894a7a4536d3
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67378737"
---
# <a name="registering-an-iocompletion-routine"></a>注册 IoCompletion 例程





若要注册[ *IoCompletion* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-io_completion_routine)例程，调度例程调用[ **IoSetCompletionRoutine**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iosetcompletionroutine)，提供*IoCompletion*例程的地址和它将随后传递到较低的驱动程序使用了 IRP [ **IoCallDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocalldriver)。

当调用**IoSetCompletionRoutine**，调度例程指定在其中 I/O 管理器应调用指定的情况*IoCompletion*例程。 你可以选择允许*IoCompletion*如果较低级别的驱动程序成功完成 IRP，调用例程 (*InvokeOnSuccess*)，完成并显示错误状态值 IRP (*InvokeOnError*)，或取消 IRP (*InvokeOnCancel*)，以任意组合。

目的*IoCompletion*例程是监视低级驱动程序未与 IRP，并以进行处理，附加完成，如有必要。 具体来说，驱动程序的使用的最常见*IoCompletion*例程如下：

-   要释放的驱动程序分配的 IRP [ **IoAllocateIrp** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioallocateirp)或[ **IoBuildAsynchronousFsdRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iobuildasynchronousfsdrequest)

    分配 IRP 的例程必须提供这些支持使用任何更高级别的驱动程序*IoCompletion*该 IRP 的例程。 *IoCompletion*例程必须调用[ **IoFreeIrp** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iofreeirp)要释放的驱动程序分配 Irp。

-   重复使用传入 IRP 请求低级驱动程序完成一定数量的操作，例如部分传输操作，直到可以满足原始请求，并将其通过完成*IoCompletion*例程

-   若要重试较低的驱动程序已完成，但出现错误的请求

    最高级别的驱动程序，如文件系统是更有可能能够*IoCompletion*尝试重试请求多于中间驱动程序，除可能的例程类的上面紧密耦合的端口驱动程序的驱动程序。 但是，任何中间驱动程序使用*IoCompletion*例程以重试请求。

而最高级别的或中间驱动[ *DispatchReadWrite* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)例程是最有可能给过程需要的 Irp *IoCompletion*例程，任何调度可以注册任何驱动程序将 Irp 传递到较低的驱动程序中的例程*IoCompletion*例程。

有关驱动程序分配的 Irp 和重复使用的 Irp，必须调用的调度例程**IoSetCompletionRoutine**使用以下布尔参数：

-   *InvokeOnSuccess*设置为 **，则返回 TRUE**

-   *InvokeOnError*设置为 **，则返回 TRUE**

-   *InvokeOnCancel*设置为**TRUE**如果链中任何较低的驱动程序可能会处理可取消的 Irp

    通常情况下， *InvokeOnCancel*设置为**TRUE**，无论是否带有状态可能会返回 IRP\_已取消，以确保*IoCompletion*例程释放每个驱动程序分配的 IRP，或检查每个重复使用的 IRP 的完成状态。

为使用较低的驱动程序分配 Irp 的调度例程**IoAllocateIrp**或[ **IoBuildAsynchronousFsdRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iobuildasynchronousfsdrequest)必须设置*IoCompletion*为每个驱动程序分配的 IRP 例程。

-   调度例程必须设置有关这两个原始状态，IRP 和为其分配的 IRP(s) *IoCompletion*例程使用。 最低限度*IoCompletion*例程需要访问原始的 IRP 和已分配了多少其他 Irp 的计数。

-   应调用的调度例程**IoSetCompletionRoutine**所有*InvokeOnXxx*参数设置为**TRUE**为它分配的 IRP(s)。

必须调用，将 Irp 重新用于一系列操作，或，重试 I/O 操作的调度例程**IoSetCompletionRoutine**为每个 IRP 将重复使用或重试。

-   调度例程必须保存原始 IRP 的状态信息，以供后续*IoCompletion*例程。

    例如， [ *DispatchReadWrite* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)例程必须保存相关传输参数为输入 IRP *IoCompletion*例程在设置部分之前，较低的下一步中该 IRP，驱动程序的传输。 保存参数是特别重要如果*DispatchReadWrite*例程修改任何参数的*IoCompletion*例程需要确定在原始请求时满足的条件。

-   如果*IoCompletion*例程可以重试请求，调度例程必须设置重试次数的驱动程序确定上限限制其*IoCompletion*例程应尝试在其之前完成原始 IRP 并出现错误。

-   如果 IRP 将重复使用，应调用的调度例程**IoSetCompletionRoutine**所有*InvokeOnXxx*参数设置为**TRUE**。

-   对于异步请求，必须调用任何中间驱动程序的调度例程[ **IoMarkIrpPending** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iomarkirppending)原始 IRP 的。 然后，它必须返回状态\_PENDING 后已发送 IRP 到低级驱动程序。

 

 




