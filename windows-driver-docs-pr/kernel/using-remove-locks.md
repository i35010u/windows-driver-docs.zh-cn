---
title: 使用删除锁
description: 使用删除锁
keywords:
- 删除锁定 WDK PnP
- 锁定例程 WDK PnP
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: a568be3e52e028c48af3c68306d86b2f48db729d
ms.sourcegitcommit: e47bd7eef2c2b89e3417d7f2dceb7c03d894f3c3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/10/2020
ms.locfileid: "97091098"
---
# <a name="using-remove-locks"></a>使用删除锁





删除锁例程提供一种方法来跟踪设备上的未完成 i/o 操作的数目，并确定何时可以安全地分离和删除驱动程序的设备对象。 系统向驱动程序编写器提供这些例程，作为实现其自己的跟踪机制的替代方法。

驱动程序可以将此机制用于两个目的：

1.  为了确保驱动程序的 [*DispatchPnP*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch) 例程在持有锁时不会完成 [**IRP \_ MN \_ REMOVE \_ 设备**](./irp-mn-remove-device.md) 请求 (例如，另一个驱动程序例程正在访问设备) 。

2.  计算驱动程序不应删除其设备对象的原因的数量，以及在该计数变为零时设置事件。

若要初始化删除锁定，驱动程序应在其 [设备扩展](device-extensions.md)中分配 **IO \_ 删除 \_ 锁定** 结构，然后调用 [**IoInitializeRemoveLock**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioinitializeremovelock)。 当驱动程序初始化设备对象的其他设备扩展时，驱动程序通常会在其 [*AddDevice*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_add_device)例程中调用 **IoInitializeRemoveLock** 。

每次启动 i/o 操作时，驱动程序都必须调用 [**IoAcquireRemoveLock**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioacquireremovelock) 。 每次完成 i/o 操作时，驱动程序都必须调用 [**IoReleaseRemoveLock**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioreleaseremovelock) 。 驱动程序可以多次获取锁定。 "删除锁" 例程维护锁的未完成的获取计数。 对 **IoAcquireRemoveLock** 的每次调用都会递增计数， **IoReleaseRemoveLock** 将减少计数。

驱动程序还应在将对其 (代码的引用 IoAcquireRemoveLock 到计时器、Dpc、回调等) 上时调用 。 然后，该驱动程序必须在该事件返回时调用 **IoReleaseRemoveLock** 。

对于 [**IRP \_ MN \_ REMOVE \_ 设备**](./irp-mn-remove-device.md)，该驱动程序必须获取此锁定，然后调用 [**IoReleaseRemoveLockAndWait**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioreleaseremovelockandwait)。 此例程不会返回，直到释放了锁定的所有未完成的获取。 若要允许排队 i/o 操作完成，每个驱动程序应在将 **IRP \_ MN \_ REMOVE \_ 设备** 请求传递到下一个较低版本的驱动程序之后、*释放* 内存、调用 [**IoDetachDevice**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iodetachdevice)或调用 [**IoDeleteDevice**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iodeletedevice)*后*，调用 **IoReleaseRemoveLockAndWait** 。 针对特定的删除锁定调用了 **IoReleaseRemoveLockAndWait** 之后，对同一删除锁定的 **IoAcquireRemoveLock** 的所有后续调用都将失败。

**IoReleaseRemoveLockAndWait** 返回后，驱动程序应考虑设备处于已准备好可供删除且无法执行 i/o 操作的状态。 因此，驱动程序不得调用 **IoInitializeRemoveLock** 来重新初始化删除锁定。 当驱动程序验证程序验证驱动程序时，违反此 [规则会导致](../devtest/driver-verifier.md) bug 检查。

由于驱动程序在设备对象的设备扩展中存储 **IO \_ 删除 \_ 锁定** 结构，因此，当驱动程序在处理 **IRP \_ MN \_ REMOVE \_ 设备** 请求时删除设备扩展时，删除锁定会被删除。

 

