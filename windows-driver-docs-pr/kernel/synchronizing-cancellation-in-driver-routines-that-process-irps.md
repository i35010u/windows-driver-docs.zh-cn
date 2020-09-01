---
title: 在处理 IRP 的驱动程序例程中同步取消
description: 在处理 IRP 的驱动程序例程中同步取消
ms.assetid: 0b252ebd-b9d5-4747-9a27-c1ecffdbae18
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: c61529f5c397874e218b25034a0c1f0c38376a6f
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89185945"
---
# <a name="synchronizing-cancellation-in-driver-routines-that-process-irps"></a>在处理 IRP 的驱动程序例程中同步取消





使用保留处于可取消状态（包括驱动程序的 [*StartIo*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_startio) 例程）的 IRP 调用的任何驱动程序例程必须执行以下操作：

1.  调用 [**IoAcquireCancelSpinLock**](/previous-versions/windows/hardware/drivers/ff548196(v=vs.85))。

2.  请检查以确保 **Irp** 等于 **DeviceObject- &gt; CurrentIrp**。 否则，请调用 [**IoReleaseCancelSpinLock**](/previous-versions/windows/hardware/drivers/ff549550(v=vs.85)) 并返回 control。

    如果这两个方法不相同，则 **CurrentIrp** 可能在 [**IoStartPacket**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-iostartpacket) 释放 "取消" 旋转锁定并获取该锁的时间之间被取消。

3.  使用**空**的*CancelRoutine*指针调用[**IoSetCancelRoutine**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iosetcancelroutine) ，以从可取消的状态中删除 IRP。

4.  检查 **irp- &gt; 取消** 字段，以确定是取消 Irp 还是开始处理 i/o 请求。

    如果 **Irp-" &gt; 取消** " 设置为 " **TRUE**"，请执行以下操作：

    -   调用 **IoReleaseCancelSpinLock**。
    -   将 **Irp- &gt; IoStatus** 设置为已 \_ 取消状态。
    -   将 ** &gt; IoStatus** 设置为0。
    -   调用*StartIo*例程) 中的[**IoStartNextPacket**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-iostartnextpacket) (，启动下一数据包。
    -   调用 [**IoCompleteRequest**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocompleterequest) ，并将 IO 提升为 IO \_ 无 \_ 增量来完成 IRP。

    如果 **Irp " &gt; 取消** " 设置为 " **FALSE**"，请调用 **IoReleaseCancelSpinLock** 并启动请求的 i/o 请求处理，或将 Irp 传递到下一个较低的驱动程序（根据需要）。

用于管理自己的 Irp 队列的驱动程序（而不是使用 i/o 管理器提供的设备队列），无需在调用 **IoSetCancelRoutine**时获取 cancel 自旋锁。 但是，这些驱动程序应检查**IoSetCancelRoutine**返回的[*取消*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_cancel)例程指针，以确定取消例程是否已启动。

在处理可取消的 Irp 的任何驱动程序中，处理 IRP 的每个驱动程序例程在为所请求的 i/o 操作进行编程之前，都应检查所有传入的 Irp 的可取消状态。 具体而言，同时具有 *StartIo* 和 [*ControllerControl*](https://msdn.microsoft.com/library/windows/hardware/ff542049) 例程的最高级别的设备驱动程序应在这两个驱动程序例程中处理传入的 irp，如前面所述。

 

