---
title: 包含 StartIo 例程的驱动程序中的 Cancel 例程
description: 包含 StartIo 例程的驱动程序中的 Cancel 例程
ms.assetid: 5098e4b9-d4db-44c2-acb3-a46878d6f1c4
keywords:
- 正在取消 Irp，StartIo 例程
- 取消例程，StartIo 例程
- StartIo 例程，取消例程
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3ba91d7266f9a04dd6ba57b9c98ea28bb042d406
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63338550"
---
# <a name="cancel-routines-in-drivers-with-startio-routines"></a>包含 StartIo 例程的驱动程序中的 Cancel 例程





I/O 管理器维护**CurrentIrp**字段中的设备对象仅当 Irp 排列在关联的设备队列对象。 也就是说，该字段是仅当该驱动程序具有有效[ *StartIo* ](https://msdn.microsoft.com/library/windows/hardware/ff563858)例程。

中的驱动程序*StartIo*例程、 典型[*取消*](https://msdn.microsoft.com/library/windows/hardware/ff540742)例程必须执行以下操作：

1.  检查输入 IRP 的指针是否与目标设备对象相匹配**CurrentIrp**地址。

    如果这些指针是等效的*取消*例程调用[ **IoReleaseCancelSpinLock**](https://msdn.microsoft.com/library/windows/hardware/ff549550)，并传递**Irp-&gt;CancelIrql**，并将控制权返回。

2.  如果已取消的 IRP 不是当前 IRP，检查与目标设备对象通过调用关联的设备队列是否为输入已取消的 IRP [ **KeRemoveEntryDeviceQueue** ](https://msdn.microsoft.com/library/windows/hardware/ff553163)与 IRP 的**Tail.Overlay.DeviceQueueEntry**指针。
    -   如果设备队列中有 IRP，调用**KeRemoveEntryDeviceQueue**从队列中删除它。 *取消*例程调用[ **IoReleaseCancelSpinLock**](https://msdn.microsoft.com/library/windows/hardware/ff549550)，设置状态的 IRP 的 I/O 状态块\_取消**状态**对于该值为零**信息**，调用[ **IoCompleteRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff548343)与已取消的 IRP 和返回控件。

    -   如果设备队列中的不是 IRP*取消*例程调用**IoReleaseCancelSpinLock**并将控制权返回。

在驱动程序*取消*例程应调用**KeRemoveEntryDeviceQueue**来测试是否 IRP 为设备队列中。 此支持例程从设备队列中移除给定的 IRP 或不执行任何操作返回除**FALSE**，指示给定的入口不已排入队列。 一个*取消*例程不能假定输入的 IRP 位于设备队列中任何特定位置，以便它不能调用[ **KeRemoveDeviceQueue** ](https://msdn.microsoft.com/library/windows/hardware/ff553156)或[**KeRemoveByKeyDeviceQueue** ](https://msdn.microsoft.com/library/windows/hardware/ff553152)比较返回 IRP 指向并输入 IRP。

具有驱动程序*取消*例程可以处理[ **IRP\_MJ\_清理**](https://msdn.microsoft.com/library/windows/hardware/ff550718)也请求。 请参阅[ *DispatchCleanup* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)有关详细信息**IRP\_MJ\_清理**请求。

 

 




