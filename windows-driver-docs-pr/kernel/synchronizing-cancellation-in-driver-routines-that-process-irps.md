---
title: 在处理 IRP 的驱动程序例程中同步取消
description: 在处理 IRP 的驱动程序例程中同步取消
ms.assetid: 0b252ebd-b9d5-4747-9a27-c1ecffdbae18
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: a8818a41ef0831c9150362de9bc5e94defc856a5
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72836188"
---
# <a name="synchronizing-cancellation-in-driver-routines-that-process-irps"></a>在处理 IRP 的驱动程序例程中同步取消





使用保留处于可取消状态（包括驱动程序的[*StartIo*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_startio)例程）的 IRP 调用的任何驱动程序例程必须执行以下操作：

1.  调用[**IoAcquireCancelSpinLock**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff548196(v=vs.85))。

2.  请检查以确保**Irp**等于**DeviceObject-&gt;CurrentIrp**。 否则，请调用[**IoReleaseCancelSpinLock**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff549550(v=vs.85))并返回 control。

    如果这两个方法不相同，则**CurrentIrp**可能在[**IoStartPacket**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-iostartpacket)释放 "取消" 旋转锁定并获取该锁的时间之间被取消。

3.  使用**空**的*CancelRoutine*指针调用[**IoSetCancelRoutine**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iosetcancelroutine) ，以从可取消的状态中删除 IRP。

4.  检查**irp&gt;的 "取消**" 字段，以确定是取消 irp 还是开始处理 i/o 请求。

    如果**Irp&gt;Cancel**设置为**TRUE**，请执行以下操作：

    -   调用**IoReleaseCancelSpinLock**。
    -   将**Irp&gt;IoStatus**设置为状态\_取消。
    -   将**Irp&gt;IoStatus**设置为0。
    -   调用[**IoStartNextPacket**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-iostartnextpacket) （在*StartIo*例程中）以启动下一个数据包。
    -   使用 IO\_"优先级提升" 来调用[**IoCompleteRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocompleterequest) ，以完成 IRP\_递增。

    如果**Irp&gt;Cancel**设置为**FALSE**，请调用**IoReleaseCancelSpinLock**并启动请求的 i/o 请求处理，或根据需要将 irp 传递到下一个较低的驱动程序。

用于管理自己的 Irp 队列的驱动程序（而不是使用 i/o 管理器提供的设备队列），无需在调用**IoSetCancelRoutine**时获取 cancel 自旋锁。 但是，这些驱动程序应检查**IoSetCancelRoutine**返回的[*取消*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_cancel)例程指针，以确定取消例程是否已启动。

在处理可取消的 Irp 的任何驱动程序中，处理 IRP 的每个驱动程序例程在为所请求的 i/o 操作进行编程之前，都应检查所有传入的 Irp 的可取消状态。 具体而言，同时具有*StartIo*和[*ControllerControl*](https://msdn.microsoft.com/library/windows/hardware/ff542049)例程的最高级别的设备驱动程序应在这两个驱动程序例程中处理传入的 irp，如前面所述。

 

 




