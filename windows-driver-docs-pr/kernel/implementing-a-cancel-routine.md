---
title: 实现 Cancel 例程
description: 实现 Cancel 例程
ms.assetid: 243b623b-317c-4084-a753-940c91c4cc50
keywords:
- 正在取消 Irp，准则
- 取消例程准则
ms.date: 05/09/2018
ms.localizationpriority: medium
ms.openlocfilehash: 9c57afb0e5099cd3591b17bd8de241cb77c463a1
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67365813"
---
# <a name="implementing-a-cancel-routine"></a>实现 Cancel 例程





I/O 管理器会调用驱动程序提供[*取消*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_cancel)例程与 IRP 取消某个输入和一个*DeviceObject*表示目标设备对 i/o 的指针请求。

IRP 可以是下列的驱动程序的[ *DispatchReadWrite* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)例程已排队，就像用户正在关闭当前的 Win32 应用程序。 IRP 也可能是一个更高级别的驱动程序显式取消，具体取决于基础设备的性质。

当*取消*例程被调用时，可能已经有输入的 IRP **CurrentIrp**中目标设备对象或可能已在如果与目标设备对象关联的设备队列驱动程序具有[ *StartIo* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_startio)例程。 如果驱动程序不包含*StartIo*例程，IRP 可能是驱动程序管理的 Irp 的内部队列中时其*取消*调用例程。 在任何情况下，在 I/O 管理器调用前*取消*传入 IRP 的例程，I/O 管理器设置**取消**中对此 IRP 成员**TRUE**并设置**CancelRoutine**成员中到 IRP **NULL**。

*取消*例程对于主控形状具有关联的 Irp 的 IRP 负责调用[ **IoCancelIrp** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocancelirp)取消那些相关联的 Irp。

所有*取消*例程必须遵守以下原则：

-   调用[ **IoReleaseCancelSpinLock** ](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff549550(v=vs.85))发布系统的取消自旋锁。

-   设置 I/O 状态块**状态**成员添加到状态\_已取消，并设置其**信息**为零的成员。

-   通过调用完成指定的 IRP [ **IoCompleteRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocompleterequest)。

-   因为*取消*与系统取消自旋锁持有始终调用例程，不能调用该例程[ **IoAcquireCancelSpinLock** ](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff548196(v=vs.85))除非调用**IoReleaseCancelSpinLock**第一个。

-   一个*取消*例程不能被系统取消自旋锁时按住它将控制权返回。 也就是说，每个*取消*例程必须调用**IoReleaseCancelSpinLock**至少一次返回控件之前。

-   如果它调用**IoAcquireCancelSpinLock**即*取消*例程必须进行相互调用**IoReleaseCancelSpinLock**尽可能快地。

-   永远不会调用[ **IoCompleteRequest** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocompleterequest)与同时保留数值调节钮锁定 IRP。 尝试在持有自旋锁完成 IRP，可能会导致死锁。


 

 




