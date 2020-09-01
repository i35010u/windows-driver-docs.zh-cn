---
title: 实现 Cancel 例程
description: 实现 Cancel 例程
ms.assetid: 243b623b-317c-4084-a753-940c91c4cc50
keywords:
- 取消 Irp，指导原则
- 取消例程，指导原则
ms.date: 05/09/2018
ms.localizationpriority: medium
ms.openlocfilehash: a4440dc005d137caa54c2b1359d48fe7d0bda89d
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89189359"
---
# <a name="implementing-a-cancel-routine"></a>实现 Cancel 例程





I/o 管理器调用驱动程序提供的 [*取消*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_cancel) 例程，其中包含要取消的输入 IRP，并使用 *DeviceObject* 指针表示 i/o 请求的目标设备。

IRP 可以是驱动程序的 [*DispatchReadWrite*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch) 例程已排队等候，因为用户正在关闭当前的 Win32 应用程序。 IRP 还可以是根据基础设备的性质，更高级别的驱动程序已明确取消。

如果调用了 *Cancel* 例程，则输入 IRP 可能已经是目标设备对象中的 **CurrentIrp** ，或者如果驱动程序具有 [*StartIo*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_startio) 例程，则它可能已经位于与目标设备对象相关联的设备队列中。 如果驱动程序没有 *StartIo* 例程，则在调用 *取消* 例程时，irp 可能在 irp 的驱动程序托管的内部队列中。 在任何情况下，在 i/o 管理器调用传入 IRP 的 *取消* 例程之前，i/o 管理器会将此 IRP 中的 **cancel** 成员设置为 **TRUE** ，并将 irp 中的 **CancelRoutine** 成员设置为 **NULL**。

具有关联的 Irp 的 master IRP 的 " *取消* " 例程负责调用 [**IoCancelIrp**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocancelirp) 来取消这些关联的 irp。

所有 *取消* 例程必须遵循以下准则：

-   调用 [**IoReleaseCancelSpinLock**](/previous-versions/windows/hardware/drivers/ff549550(v=vs.85)) 以释放系统的取消旋转锁。

-   将 i/o 状态块的 **状态** 成员设置为 "已取消" 状态 \_ ，并将其 **信息** 成员设置为零。

-   通过调用 [**IoCompleteRequest**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocompleterequest)来完成指定的 IRP。

-   由于始终会在系统取消旋转锁的情况下调用 *cancel* 例程，因此此例程不得调用 [**IoAcquireCancelSpinLock**](/previous-versions/windows/hardware/drivers/ff548196(v=vs.85)) ，除非它首先调用 **IoReleaseCancelSpinLock** 。

-   当 *取消* 例程返回 control 时，它无法保持系统取消旋转锁。 也就是说，每个 *取消* 例程在返回 control 之前必须至少调用一次 **IoReleaseCancelSpinLock** 。

-   如果调用 **IoAcquireCancelSpinLock**，则 *取消* 例程必须尽快使对 **IoReleaseCancelSpinLock** 的调用。

-   持有自旋锁时，切勿使用 IRP 调用 [**IoCompleteRequest**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocompleterequest) 。 尝试在持有自旋锁时完成 IRP 会导致死锁。


 

