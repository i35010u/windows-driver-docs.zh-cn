---
title: 等待/唤醒 Irp 的 IoCompletion 例程
description: 等待/唤醒 Irp 的 IoCompletion 例程
ms.assetid: 61239398-2d37-4163-8128-7a4a0916a262
keywords:
- 接收等待/唤醒 Irp
- 等待/唤醒 Irp WDK 电源管理，接收
- IoCompletion 例程
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3f2df22314f662f05957524c8da7e39890b00453
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56547839"
---
# <a name="iocompletion-routines-for-waitwake-irps"></a>等待/唤醒 Irp 的 IoCompletion 例程





I/O 管理器调用的驱动程序等待/唤醒[ *IoCompletion* ](https://msdn.microsoft.com/library/windows/hardware/ff548354)后设备堆栈中的下一步低驱动程序已完成等待/唤醒 IRP 的例程。 每个函数，并筛选 (FDO) 驱动程序，应设置一个等待/唤醒 IRP 的句柄*IoCompletion* IRP 的例程。

每个函数或筛选器驱动程序设置*IoCompletion*例程的方式与处理等待/唤醒 IRP 向下设备堆栈。 因此可能必须发送 IRP，将设备电源策略所有者*IoCompletion*例程除了回调例程。 请记住，之后调用回调例程*IoCompletion*例程和两个具有不同的要求。 有关详细信息，请参阅[等待/唤醒回调例程](wait-wake-callback-routines.md)。

在等待/唤醒所需的操作*IoCompletion*例程依赖于设备和驱动程序的类型。 以下是一个驱动程序可能需要在其等待/唤醒中执行某些操作*IoCompletion*例程：

1.  重置设备扩展中的任何相关字段。 例如，等待/唤醒 IRP 挂起时，大多数驱动程序将设置一个标志，并将指针保留在设备扩展 IRP。

2.  重置[*取消*](https://msdn.microsoft.com/library/windows/hardware/ff540742)例程中，如果有，通过调用 IRP [ **IoSetCancelRoutine**](https://msdn.microsoft.com/library/windows/hardware/ff549674)，并指定**NULL**例程的指针。

3.  调用**IoCompleteRequest**，指定 IO\_否\_增量，以完成 IRP。

每个连续的驱动程序完成后 IRP，I/O 管理器将控制权传递给*IoCompletion*例程在堆栈中向上追溯的下一个更高版本驱动程序。

在调用*IoCompletion*设置的驱动程序为它们通过等待/唤醒 IRP 向设备堆栈下的例程，I/O 管理器会调用传递给回调例程[ **PoRequestPowerIrp**](https://msdn.microsoft.com/library/windows/hardware/ff559734)发送 IRP 驱动程序。 有关详细信息，请参阅[等待/唤醒回调例程](wait-wake-callback-routines.md)。

 

 




