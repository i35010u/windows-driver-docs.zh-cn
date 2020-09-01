---
title: 包含 StartIo 例程的驱动程序中的 Cancel 例程
description: 包含 StartIo 例程的驱动程序中的 Cancel 例程
ms.assetid: 5098e4b9-d4db-44c2-acb3-a46878d6f1c4
keywords:
- 取消 Irp，StartIo 例程
- 取消例程，StartIo 例程
- StartIo 例程，取消例程
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6c10ba095a869518bf089ca038e9ba2a1ba67035
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89188636"
---
# <a name="cancel-routines-in-drivers-with-startio-routines"></a>包含 StartIo 例程的驱动程序中的 Cancel 例程





仅当 Irp 在关联设备队列对象中排队时，i/o 管理器才会在设备对象中维护 **CurrentIrp** 字段。 也就是说，仅当驱动程序具有 [*StartIo*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_startio) 例程时，此字段才有效。

在具有 *StartIo* 例程的驱动程序中，典型的 [*Cancel*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_cancel) 例程必须执行以下操作：

1.  检查输入 IRP 的指针是否与目标设备对象的 **CurrentIrp** 地址匹配。

    如果这些指针相等，则 *Cancel* 例程将调用 [**IoReleaseCancelSpinLock**](/previous-versions/windows/hardware/drivers/ff549550(v=vs.85))，并通过 ** &gt; irp->cancelirql**并返回控制权。

2.  如果取消的 IRP 不是当前的 IRP，请通过使用 IRP 的**DeviceQueueEntry**指针调用[**KeRemoveEntryDeviceQueue**](/windows-hardware/drivers/ddi/wdm/nf-wdm-keremoveentrydevicequeue)来检查输入的 "已取消" irp 是否位于与目标设备对象相关联的设备队列中。
    -   如果 IRP 在设备队列中，则调用 **KeRemoveEntryDeviceQueue** 会将其从队列中删除。 *Cancel*例程将调用[**IoReleaseCancelSpinLock**](/previous-versions/windows/hardware/drivers/ff549550(v=vs.85))，并设置 IRP 的 i/o 状态块，状态 \_ 为 "已取消"; 对于 " **Information****状态**"， [**IoCompleteRequest**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocompleterequest)将调用已取消的 IRP，并返回 control。

    -   如果 IRP 不在设备队列中，则 *Cancel* 例程将调用 **IoReleaseCancelSpinLock** 并返回 control。

驱动程序的 *Cancel* 例程应调用 **KEREMOVEENTRYDEVICEQUEUE** 来测试 IRP 是否在设备队列中。 此支持例程会从设备队列中删除给定的 IRP，或不执行任何操作（返回 **FALSE**除外），指示给定的条目未排队。 *取消*例程无法假定输入 IRP 在设备队列中的任何特定位置，因此它无法调用[**KeRemoveDeviceQueue**](/windows-hardware/drivers/ddi/wdm/nf-wdm-keremovedevicequeue)或[**KeRemoveByKeyDeviceQueue**](/windows-hardware/drivers/ddi/wdm/nf-wdm-keremovebykeydevicequeue)来比较指向返回的 irp 和输入 irp 的指针。

带有 *取消* 例程的驱动程序也可以处理 [**IRP \_ MJ \_ 清理**](./irp-mj-cleanup.md) 请求。 有关**IRP \_ MJ \_ 清理**请求的详细信息，请参阅[*DispatchCleanup*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch) 。

 

