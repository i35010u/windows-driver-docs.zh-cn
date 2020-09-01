---
title: 注册 IoCompletion 例程
description: 注册 IoCompletion 例程
ms.assetid: 413d8463-b2ce-44b6-846c-f853b5cd580e
keywords:
- IoCompletion 例程
- 注册 IoCompletion 例程
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 56d74217bb0ba78e45df5e47d34dc4ee6f67797b
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89186195"
---
# <a name="registering-an-iocompletion-routine"></a>注册 IoCompletion 例程





若要注册 [*IoCompletion*](/windows-hardware/drivers/ddi/wdm/nc-wdm-io_completion_routine) 例程，调度例程会调用 [**IoSetCompletionRoutine**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iosetcompletionroutine)，并提供 *IOCOMPLETION* 例程的地址和 IRP，然后它随后会通过 [**IoCallDriver**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver)传递到较低的驱动程序。

当它调用 **IoSetCompletionRoutine**时，调度例程将指定 i/o 管理器应调用指定的 *IoCompletion* 例程的情况。 如果低级驱动程序成功完成 IRP (*InvokeOnSuccess*) 、完成 irp，并将错误状态值 (*InvokeOnError*) ，则可以选择使用*IoCompletion*例程，或取消任何组合中的 irp (*InvokeOnCancel*) 。

*IoCompletion*例程的目的是通过 IRP 监视更低级别的驱动程序，并根据需要执行其他完成处理。 具体而言，驱动程序的 *IoCompletion* 例程的最常见用途如下：

-   释放使用[**IoAllocateIrp**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioallocateirp)或[**IoBuildAsynchronousFsdRequest**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iobuildasynchronousfsdrequest)分配的驱动程序的 IRP

    使用任一支持例程分配 IRP 的任何更高级别的驱动程序都必须为该 IRP 提供 *IoCompletion* 例程。 *IoCompletion*例程必须调用[**IoFreeIrp**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iofreeirp)以释放驱动程序分配的 irp。

-   若要重新使用传入的 IRP 来请求较低版本的驱动程序，请完成一些操作，例如部分传输，直到 *IoCompletion* 例程满足并完成原始请求

-   重试请求，驱动程序驱动程序已完成，但出现错误

    最高级别的驱动程序（如文件系统）更有可能使用 *IoCompletion* 例程来尝试重试请求，而不是中间驱动程序，这种情况下的类驱动程序可能会超出紧耦合的端口驱动程序。 但是，任何中间驱动程序都使用 *IoCompletion* 例程来重试请求。

当最高级别或中间驱动程序的 [*DispatchReadWrite*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch) 例程最有可能处理需要 *IoCompletion* 例程的 irp 时，任何将 irp 传递到较低的驱动程序的驱动程序中的任何调度例程都可以注册 *IoCompletion* 例程。

对于驱动程序分配的 Irp 和重复使用的 Irp，调度例程必须使用以下布尔参数调用 **IoSetCompletionRoutine** ：

-   *InvokeOnSuccess* 设置为 **TRUE**

-   *InvokeOnError* 设置为 **TRUE**

-   如果链中的任何较低的驱动程序可能处理可取消的 Irp， *InvokeOnCancel*设置为**TRUE**

    通常情况下， *InvokeOnCancel* 设置为 **TRUE**，不管 IRP 是否可能返回状态为 "已 \_ 取消"，以确保 *IoCompletion* 例程释放每个驱动程序分配的 irp，或检查 irp 的每次重复使用的完成状态。

使用 **IoAllocateIrp** 或 [**IoBuildAsynchronousFsdRequest**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iobuildasynchronousfsdrequest)为低级驱动程序分配 irp 的调度例程必须为每个驱动程序分配的 IRP 设置一个 *IoCompletion* 例程。

-   调度例程必须设置有关原始 IRP 及其分配的 IRP (s 的状态，) ， *IoCompletion* 例程才能使用。 *IoCompletion*例程至少需要具有对原始 IRP 的访问权限，以及已分配的其他 irp 的计数。

-   如果) 分配的 IRP (的所有*InvokeOnXxx*参数均设置为**TRUE** ，则调度例程应调用**IoSetCompletionRoutine** 。

重新使用 Irp 来执行一系列操作或重试 i/o 操作的调度例程，必须为将重新使用或重试的每个 IRP 调用 **IoSetCompletionRoutine** 。

-   调度例程必须保存原始 IRP 的状态信息，以供 *IoCompletion* 例程以后使用。

    例如， [*DispatchReadWrite*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch) 例程必须先保存 *IoCompletion* 例程的输入 IRP 的相关传输参数，然后再为该 IRP 中下一个较低版本的驱动程序设置部分传输。 如果 *DispatchReadWrite* 例程修改了 *IoCompletion* 例程需要确定何时满足原始请求所需的任何参数，则保存参数尤其重要。

-   如果 *IoCompletion* 例程可以重试请求，则 *调度例程必须* 在完成原始 IRP 的错误之前，设置驱动程序确定的重试次数的上限。

-   如果要重复使用 IRP，调度例程应调用 **IoSetCompletionRoutine** ，并将所有 *InvokeOnXxx* 参数设置为 **TRUE**。

-   对于异步请求，任何中间驱动程序的调度例程必须为原始 IRP 调用 [**也**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iomarkirppending) 。 然后，它必须在 \_ 将 IRP 发送到较低的驱动程序后返回状态 "挂起"。

 

