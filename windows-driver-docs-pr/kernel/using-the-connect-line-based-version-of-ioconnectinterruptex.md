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
ms.openlocfilehash: 0131f14d6ccf6c5e0e6864e2513bd19f16c02eb9
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89187703"
---
# <a name="using-the-connect_line_based-version-of-ioconnectinterruptex"></a>使用 IoConnectInterruptEx 的 \_ 基于连接线 \_ 的版本


对于 Windows Vista 和更高版本的操作系统，驱动程序可以使用 \_ 基于连接线路 \_ 的 [**IoConnectInterruptEx**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioconnectinterruptex) 版本为驱动程序的基于行的中断注册 [*InterruptService*](/windows-hardware/drivers/ddi/wdm/nc-wdm-kservice_routine) 例程。 对于早期版本的操作系统 (驱动程序可以使用 \_ 连接 \_ 的 **IoConnectInterruptEx**的完全指定版本。 ) 

**注意**   此方法只能用于为其所有基于行的中断注册单个中断服务例程 (ISR) 的驱动程序。 如果驱动程序可以接收多个中断，则必须使用 IoConnectInterruptEx 的 CONNECT \_ 完全 \_ 指定**IoConnectInterruptEx**版本。

 

驱动程序为参数版本指定连接 \_ 行值 \_ *Parameters* - &gt; **Version** ，并使用*参数* - &gt; **LineBased**的成员指定操作的其他参数：

-   *Parameters* - 参数 &gt;**LineBased**为 ISR 服务的设备指定 (PDO) 的物理设备对象。 系统使用设备对象自动标识设备的基于线路的中断。

-   *Parameters* - 参数 &gt;**LineBased ServiceRoutine**指向*InterruptService*例程，而*参数* - &gt; **LineBased**。**ServiceContext**指定系统作为*ServiceContext*参数传递到*InterruptService*的值。 驱动程序可以使用它来传递上下文信息。 有关传递上下文信息的详细信息，请参阅 [提供 ISR 上下文信息](providing-isr-context-information.md)。

-   驱动程序提供指向 * Parameters *** - &gt; LineBased. InterruptObject**中的 PKINTERRUPT 变量的指针。 **IoConnectInterruptEx** 将此变量设置为指向中断的中断对象，可在删除 ISR 时使用该对象。 有关详细信息，请参阅 [删除 ISR](removing-an-isr.md)。

-   驱动程序可以选择在参数中指定一个自旋锁 ** * * &gt; LineBased**，以便在与 ISR 同步时使用系统。 大多数驱动程序可以仅指定 **NULL** ，使系统能够代表驱动程序分配自旋锁。 有关与 ISR 同步的详细信息，请参阅 [同步对设备数据的访问](synchronizing-access-to-device-data.md)。

下面的代码示例演示如何使用基于连接线*InterruptService*的连接线注册 InterruptService \_ 例程 \_ ：

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

 

