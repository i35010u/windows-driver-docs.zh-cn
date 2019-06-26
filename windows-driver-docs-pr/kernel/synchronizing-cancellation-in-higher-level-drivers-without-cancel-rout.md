---
title: 在不包含 Cancel 例程的较高级驱动程序中同步取消
description: 在不包含 Cancel 例程的较高级驱动程序中同步取消
ms.assetid: 741d504e-7e61-4f60-a8cf-e4ea92f0654e
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 171f9f60ca4b03b8741553b9dd589a051be611df
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67355474"
---
# <a name="synchronizing-cancellation-in-higher-level-drivers-without-cancel-routines"></a>在不包含 Cancel 例程的较高级驱动程序中同步取消





更高级别的驱动程序可以做任何假设还是较低级别的现有驱动程序处理可取消 Irp 的方式。 只要任何更高级别的驱动程序调用[ **IoCallDriver** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocalldriver)的 IRP，它不再拥有的 IRP 和它不能确定或控制处理的 IRP 的较低级驱动程序。

但是，可以设置任何更高级别的驱动程序[ *IoCompletion* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-io_completion_routine)例程对于通过调用 IRP [ **IoSetCompletionRoutine** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iosetcompletionroutine)之前调用**IoCallDriver**。 更高级别的驱动程序可以确定是否任何挂起的 IRP 取消较低的驱动程序中通过调用**IoSetCompletionRoutine**与*InvokeOnCancel*参数设置为**TRUE**它将传递到较低的驱动程序 IRP 之前。 这样做可确保该驱动程序的*IoCompletion* IRP 是取消还是已完成，将调用例程。

更高级别的驱动程序可以调用[ **IoCancelIrp** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocancelirp)具有任何挂起的 IRP 已经分配了该驱动程序。 但是，进行此调用不能确保将状态设置为其 I/O 状态块已完成驱动程序分配 IRP\_已取消; 另一个线程可能已完成 IRP。 若要检查是否已取消 IRP，更高级别的驱动程序必须调用**IoSetCompletionRoutine**与*InvokeOnCancel*参数设置为**TRUE**然后才传递IRP 到下一个较低的驱动程序。 请参阅[完成 Irp](completing-irps.md)有关完成例程的详细信息。

更高级别的驱动程序不能调用**IoCancelIrp**与未分配的 IRP。

 

 




