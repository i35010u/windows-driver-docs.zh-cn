---
title: 使用删除锁
description: 使用删除锁
ms.assetid: 78ca7fe5-ceed-4752-bf1b-d13309097cd8
keywords:
- 删除锁定 WDK PnP
- 锁定例程 WDK PnP
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: e6376afa82412fb953b7cccfa71dafcb4280006a
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72835864"
---
# <a name="using-remove-locks"></a>使用删除锁





[删除锁例程](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)提供一种方法来跟踪设备上的未完成 i/o 操作的数目，并确定何时可以安全地分离和删除驱动程序的设备对象。 系统向驱动程序编写器提供这些例程，作为实现其自己的跟踪机制的替代方法。

驱动程序可以将此机制用于两个目的：

1.  若要确保驱动程序的[*DispatchPnP*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)例程不会完成[**IRP\_MN\_** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-remove-device)在持有锁时删除\_设备请求（例如，另一个驱动程序例程正在访问设备）。

2.  计算驱动程序不应删除其设备对象的原因的数量，以及在该计数变为零时设置事件。

若要初始化删除锁定，驱动程序应分配**IO\_删除**其[设备扩展](device-extensions.md)中的\_锁定结构，然后调用[**IoInitializeRemoveLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioinitializeremovelock)。 当驱动程序初始化设备对象的其他设备扩展时，驱动程序通常会在其[*AddDevice*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_add_device)例程中调用**IoInitializeRemoveLock** 。

每次启动 i/o 操作时，驱动程序都必须调用[**IoAcquireRemoveLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioacquireremovelock) 。 每次完成 i/o 操作时，驱动程序都必须调用[**IoReleaseRemoveLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioreleaseremovelock) 。 驱动程序可以多次获取锁定。 "删除锁" 例程维护锁的未完成的获取计数。 对**IoAcquireRemoveLock**的每次调用都会递增计数， **IoReleaseRemoveLock**将减少计数。

当驱动程序传递到其代码的引用时（对于计时器、Dpc、回调等），您的驱动程序还应调用**IoAcquireRemoveLock** 。 然后，该驱动程序必须在该事件返回时调用**IoReleaseRemoveLock** 。

在其用于 IRP\_MN 的调度代码中[ **\_删除\_设备**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-remove-device)，驱动程序必须再次获取锁定，然后调用[**IoReleaseRemoveLockAndWait**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioreleaseremovelockandwait)。 此例程不会返回，直到释放了锁定的所有未完成的获取。 若要允许排队 i/o 操作完成，每个驱动程序都应 *在*将 IRP 传递给**IRP\_MN**时调用 IoReleaseRemoveLockAndWait，\_删除向下一个较低版本的驱动程序\_设备请求 *，然后再*释放内存、调用[**IoDetachDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iodetachdevice)或调用[**IoDeleteDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iodeletedevice)。 针对特定的删除锁定调用了**IoReleaseRemoveLockAndWait**之后，对同一删除锁定的**IoAcquireRemoveLock**的所有后续调用都将失败。

**IoReleaseRemoveLockAndWait**返回后，驱动程序应考虑设备处于已准备好可供删除且无法执行 i/o 操作的状态。 因此，驱动程序不得调用**IoInitializeRemoveLock**来重新初始化删除锁定。 当驱动程序验证程序验证驱动程序时，违反此[规则会导致](https://docs.microsoft.com/windows-hardware/drivers/devtest/driver-verifier)bug 检查。

由于驱动程序存储**IO\_删除**设备对象的设备扩展中\_锁定结构，因此，当驱动程序在处理 IRP 时删除设备扩展时删除锁定 **\_MN\_删除\_设备**请求。

 

 




