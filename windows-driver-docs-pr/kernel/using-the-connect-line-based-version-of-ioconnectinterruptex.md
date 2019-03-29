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
ms.openlocfilehash: 45e6492af31d6485d56810df9f51b18014de61ec
ms.sourcegitcommit: b3859d56cb393e698c698d3fb13519ff1522c7f3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57349692"
---
# <a name="using-the-connectlinebased-version-of-ioconnectinterruptex"></a>使用 CONNECT\_行\_IoConnectInterruptEx 基于版本


对于 Windows Vista 和更高版本操作系统中，驱动程序可以使用 CONNECT\_行\_基于版本[ **IoConnectInterruptEx** ](https://msdn.microsoft.com/library/windows/hardware/ff548378)注册[ *InterruptService* ](https://msdn.microsoft.com/library/windows/hardware/ff547958)例程的驱动程序的基于线条的中断。 (早期版本操作系统的驱动程序可以使用 CONNECT\_完全\_SPECIFIED 新版**IoConnectInterruptEx**。)

**请注意**  可以为其基于行的中断的所有使用此方法只应该用于注册单个中断服务例程 (ISR) 的驱动程序。 如果该驱动程序可以接收多个中断，它必须使用 CONNECT\_完全\_SPECIFIED 新版**IoConnectInterruptEx**。

 

该驱动程序指定的连接值\_行\_基于 for*参数*-&gt;**版本**，并使用的成员*参数*-&gt;**LineBased**来指定该操作的其他参数：

-   *参数*-&gt;**LineBased.PhysicalDeviceObject**指定设备的物理设备对象 (PDO) 的 ISR 服务。 系统使用的设备对象自动识别设备的基于线条的中断。

-   *参数*-&gt;**LineBased.ServiceRoutine**指向*InterruptService*例程，而*参数*- &gt; **LineBased**。**ServiceContext**指定系统将作为传递的值*ServiceContext*参数*InterruptService*。 该驱动程序可以使用此传递上下文信息。 有关传递上下文信息的详细信息，请参阅[提供 ISR 上下文信息](providing-isr-context-information.md)。

-   该驱动程序提供了指向 PKINTERRUPT 变量中的 * 参数 ***-&gt;LineBased.InterruptObject**。 **IoConnectInterruptEx**设置此变量，使其指向的中断，可以删除 ISR 时使用的中断对象 有关详细信息，请参阅[删除 ISR](removing-an-isr.md)。

-   驱动程序可以选择指定在旋转锁*参数 * * *-&gt;LineBased.SpinLock** ISR 与同步时要使用的系统 大多数驱动程序可以只需指定**NULL**启用系统分配旋转锁代表该驱动程序。 有关与 ISR 同步的详细信息，请参阅[对设备数据的同步访问](synchronizing-access-to-device-data.md)。

下面的代码示例演示如何注册*InterruptService*例程使用 CONNECT\_行\_基于：

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

 

 




