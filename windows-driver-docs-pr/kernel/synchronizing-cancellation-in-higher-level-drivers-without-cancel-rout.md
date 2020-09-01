---
title: 在不包含 Cancel 例程的较高级驱动程序中同步取消
description: 在不包含 Cancel 例程的较高级驱动程序中同步取消
ms.assetid: 741d504e-7e61-4f60-a8cf-e4ea92f0654e
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 702b4307da9f8e9a6a23ad44c30dd5a22db16dbd
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89185927"
---
# <a name="synchronizing-cancellation-in-higher-level-drivers-without-cancel-routines"></a>在不包含 Cancel 例程的较高级驱动程序中同步取消





较高级别的驱动程序对现有的低级驱动程序是否可以处理可取消的 Irp 没有任何假设。 一旦任何更高级别的驱动程序为 IRP 调用 [**IoCallDriver**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver) ，它就不再拥有该 irp，它既不能确定也不能控制低级别驱动程序对 IRP 的处理。

但是，任何更高级别的驱动程序都可以通过在调用**IoCallDriver**之前调用[**IOSETCOMPLETIONROUTINE**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iosetcompletionroutine) ，为 IRP 设置[*IoCompletion*](/windows-hardware/drivers/ddi/wdm/nc-wdm-io_completion_routine)例程。 较高级别的驱动程序可以通过在将 IRP 传递到较低的驱动程序之前调用 **IoSetCompletionRoutine** ，并将 *InvokeOnCancel* 参数设置为 **TRUE** 来确定是否已在较低的驱动程序中取消任何挂起的 IRP。 这样做可确保无论 IRP 是否已取消或已完成，都将调用驱动程序的 *IoCompletion* 例程。

较高级别的驱动程序可以使用该驱动程序已分配的任何挂起的 IRP 来调用 [**IoCancelIrp**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocancelirp) 。 但是，执行此调用不会确保已完成驱动程序分配的 IRP，并将其 i/o 状态阻止设置为 "状态"， \_ 另一个线程可能已经完成 IRP。 若要检查 IRP 是否已取消，更高级别的驱动程序必须在将 IRP 传递到下一个较低版本的驱动程序之前调用 **IoSetCompletionRoutine** ，并将 *InvokeOnCancel* 参数设置为 **TRUE** 。 有关完成例程的详细信息，请参阅 [完成 irp](completing-irps.md) 。

较高级别的驱动程序不得使用未分配的 IRP 调用 **IoCancelIrp** 。

 

