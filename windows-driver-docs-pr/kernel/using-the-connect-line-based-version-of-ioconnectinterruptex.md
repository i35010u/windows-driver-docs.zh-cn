---
title: 使用 IoConnectInterruptEx 的 CONNECT_LINE_BASED 版本
description: 使用 IoConnectInterruptEx 的 CONNECT_LINE_BASED 版本
ms.assetid: 245be266-f76c-43f6-9ea7-2dc853b1d5e2
keywords:
- IoConnectInterruptEx
- CONNECT_LINE_BASED
- 基于行的中断 WDK 内核
- 自动中断检测 WDK 内核
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1b11f541600ce432672b4dedb569f1e2d8b42505
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72835868"
---
# <a name="using-the-connect_line_based-version-of-ioconnectinterruptex"></a>使用连接\_行\_IoConnectInterruptEx 版本


对于 Windows Vista 和更高版本的操作系统，驱动程序可以使用 CONNECT\_LINE\_[**IoConnectInterruptEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioconnectinterruptex)版本为驱动程序的基于行的中断注册[*InterruptService*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-kservice_routine)例程。 （对于较早版本的操作系统，驱动程序可以使用连接\_完全\_指定版本的**IoConnectInterruptEx**。）

**请注意**   只能对为其所有基于行的中断注册单个中断服务例程（ISR）的驱动程序使用此方法。 如果驱动程序可以接收多个中断，则必须使用连接\_完全\_指定的**IoConnectInterruptEx**版本。

 

驱动程序将\_行\_的值指定为-&gt;**版本**的*参数*，并使用-**LineBased** *参数*的成员来指定操作的其他参数：&gt;

-   *参数*-&gt;**LineBased。 PhysicalDeviceObject**指定 ISR 服务的设备的物理设备对象（PDO）。 系统使用设备对象自动标识设备的基于线路的中断。

-   *参数*-&gt;**ServiceRoutine**指向*InterruptService*例程，而*参数*-&gt;**LineBased**。**ServiceContext**指定系统作为*ServiceContext*参数传递到*InterruptService*的值。 驱动程序可以使用它来传递上下文信息。 有关传递上下文信息的详细信息，请参阅[提供 ISR 上下文信息](providing-isr-context-information.md)。

-   驱动程序提供指向 * Parameters * **-&gt;LineBased InterruptObject**中的 PKINTERRUPT 变量的指针。 **IoConnectInterruptEx**将此变量设置为指向中断的中断对象，可在删除 ISR 时使用该对象。 有关详细信息，请参阅[删除 ISR](removing-an-isr.md)。

-   驱动程序可以选择指定参数中的自旋锁 ** * *-&gt;旋转锁** 以便系统在与 ISR 同步时使用。 大多数驱动程序可以仅指定**NULL** ，使系统能够代表驱动程序分配自旋锁。 有关与 ISR 同步的详细信息，请参阅[同步对设备数据的访问](synchronizing-access-to-device-data.md)。

下面的代码示例演示如何使用 CONNECT\_LINE\_来注册*InterruptService*例程：

```cpp
IO_CONNECT_INTERRUPT_PARAMETERS params;

// deviceExtension is a pointer to the driver's device extension. 
//     deviceExtension->IntObj is a PKINTERRUPT.
// deviceInterruptService is a pointer to the driver's InterruptService routine.
// PhysicalDeviceObject is a pointer to the device's PDO. 
// ServiceContext is a pointer to driver-specified context for the ISR.

RtlZeroMemory( &params, sizeof(IO_CONNECT_INTERRUPT_PARAMETERS) );
params.Version = CONNECT_LINE_BASED;
params.LineBased.PhysicalDeviceObject = PhysicalDeviceObject;
params.LineBased.InterruptObject = &deviceExtension->IntObj;
params.LineBased.ServiceRoutine = deviceInterruptService;
params.LineBased.ServiceContext = ServiceContext;
params.LineBased.SpinLock = NULL;
params.LineBased.SynchronizeIrql = 0;
params.LineBased.FloatingSave = FALSE;

status = IoConnectInterruptEx(&params);

if (!NT_SUCCESS(status)) {
    // Operation failed. Handle error.
    ...
}
```

 

 




