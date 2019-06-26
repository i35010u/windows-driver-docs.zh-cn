---
title: 使用删除锁
description: 使用删除锁
ms.assetid: 78ca7fe5-ceed-4752-bf1b-d13309097cd8
keywords:
- 删除锁定 WDK 即插即用
- 锁定例程 WDK 即插即用
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8e3fdd7f7345cf9128e4c7b47037e3ba5c705621
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67381533"
---
# <a name="using-remove-locks"></a>使用删除锁





[删除锁定例程](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)提供一种方法来跟踪在设备上的未完成 I/O 操作的数目并确定何时可以安全地分离和删除驱动程序的设备对象。 系统提供的这些例程对驱动程序编写者作为实现自己的跟踪机制的替代方法。

驱动程序可以使用此机制有两个用途：

1.  若要确保在驱动程序[ *DispatchPnP* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)例程将无法完成[ **IRP\_MN\_删除\_设备**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-remove-device)请求 （例如，而另一个驱动程序例程访问设备） 持有锁时。

2.  为什么该驱动程序不应删除其设备对象，原因数目进行计数并设置该计数变为零时时发生的事件。

若要初始化的删除锁，驱动程序应分配**IO\_删除\_锁**结构中其[设备扩展](device-extensions.md)，然后调用[ **IoInitializeRemoveLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioinitializeremovelock)。 驱动程序通常会调用**IoInitializeRemoveLock**在其[ *AddDevice* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_add_device)例程，当驱动程序的初始化的设备扩展插件的设备对象的其余部分。

您的驱动程序必须调用[ **IoAcquireRemoveLock** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioacquireremovelock)每次启动 I/O 操作。 该驱动程序必须调用[ **IoReleaseRemoveLock** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioreleaseremovelock)每次完成某个 I/O 操作。 驱动程序可以超过一次获取的锁。 删除锁定例程维护的锁的未完成的收购的计数。 每次调用**IoAcquireRemoveLock**递增计数，并**IoReleaseRemoveLock**递减计数。

您的驱动程序还应调用**IoAcquireRemoveLock**时出对其代码的引用传递 （对于计时器、 Dpc、 回调和等等）。 该驱动程序然后必须调用**IoReleaseRemoveLock**时返回事件。

在为其调度代码中[ **IRP\_MN\_删除\_设备**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-remove-device)，驱动程序必须一次获取锁，然后调用[ **IoReleaseRemoveLockAndWait**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioreleaseremovelockandwait)。 此例程不返回，直到已释放的锁的所有未完成的收购。 若要允许排队的 I/O 操作完成，每个驱动程序应调用**IoReleaseRemoveLockAndWait** *后*它将传递**IRP\_MN\_删除\_设备**请求到下一个较低的驱动程序，并*之前*会释放内存，调用[ **IoDetachDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iodetachdevice)，或调用[ **IoDeleteDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iodeletedevice)。 之后**IoReleaseRemoveLockAndWait**已调用的特定删除锁，对所有后续调用**IoAcquireRemoveLock**对于同一个删除锁定将失败。

之后**IoReleaseRemoveLockAndWait**返回时，该驱动程序应考虑设备不处于状态，它已准备好删除，无法执行 I/O 操作。 因此，不能调用该驱动程序**IoInitializeRemoveLock**重新初始化删除锁。 正在验证的驱动程序时此规则的冲突[Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/driver-verifier)将导致的 bug 检查。

因为驱动程序存储**IO\_删除\_锁**对象在设备的设备扩展中的结构，删除锁被删除时，驱动程序处理时删除设备的扩展**IRP\_MN\_删除\_设备**请求。

 

 




