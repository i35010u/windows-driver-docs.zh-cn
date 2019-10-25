---
title: 等待/唤醒 IRP 的 IoCompletion 例程
description: 等待/唤醒 IRP 的 IoCompletion 例程
ms.assetid: 61239398-2d37-4163-8128-7a4a0916a262
keywords:
- 正在接收等待/唤醒 Irp
- 等待/唤醒 Irp WDK 电源管理，接收
- IoCompletion 例程
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 367bf079156463522bfc64ebcf187efcccca6d3d
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838612"
---
# <a name="iocompletion-routines-for-waitwake-irps"></a>等待/唤醒 IRP 的 IoCompletion 例程





在设备堆栈中的下一个低驱动程序完成等待/唤醒 IRP 后，i/o 管理器会调用驱动程序的等待/唤醒[*IoCompletion*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-io_completion_routine)例程。 处理等待/唤醒 IRP 的每个函数和筛选器（FDO）驱动程序都应为 IRP 设置*IoCompletion*例程。

每个函数或筛选器驱动程序都设置*IoCompletion*例程，因为它会在设备堆栈下处理等待/唤醒 IRP。 因此，发送 IRP 的设备电源策略所有者可能具有*IoCompletion*例程以及回调例程。 请记住，回调例程在*IoCompletion*例程之后调用，这两个例程具有不同的要求。 有关详细信息，请参阅[等待/唤醒回调例程](wait-wake-callback-routines.md)。

Wait/唤醒*IoCompletion*例程所需的操作取决于设备和驱动程序类型。 下面是驱动程序可能需要在其 wait/唤醒*IoCompletion*例程中执行的某些操作：

1.  重置设备扩展中的所有相关字段。 例如，等待/唤醒 IRP 处于挂起状态时，大多数驱动程序会设置一个标志，并在设备扩展中保留一个指向 IRP 的指针。

2.  通过调用[**IoSetCancelRoutine**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iosetcancelroutine)为 IRP 重置[*取消*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_cancel)例程（如果有），并指定例程的**NULL**指针。

3.  调用**IoCompleteRequest**，指定 IO\_NO\_递增，以完成 IRP。

每个连续的驱动程序完成 IRP 后，i/o 管理器会将控制传递到下一个更高的驱动程序的*IoCompletion*例程，该例程会在堆栈中进行备份。

在调用由驱动程序设置的*IoCompletion*例程后，当它们通过设备堆栈向下传递等待/唤醒 IRP 时，i/o 管理器会调用发送 IRP 的驱动程序传递给[**PoRequestPowerIrp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-porequestpowerirp)的回调例程。 有关详细信息，请参阅[等待/唤醒回调例程](wait-wake-callback-routines.md)。

 

 




