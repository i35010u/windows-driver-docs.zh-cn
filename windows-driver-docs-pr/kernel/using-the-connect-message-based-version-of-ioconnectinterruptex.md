---
title: 使用 IoConnectInterruptEx 的 CONNECT_MESSAGE_BASED 版本
description: 使用 IoConnectInterruptEx 的 CONNECT_MESSAGE_BASED 版本
ms.assetid: 8e06c6aa-85de-4ed2-ac0d-0179201d1272
keywords:
- IoConnectInterruptEx
- CONNECT_MESSAGE_BASED
- 消息信号中断 WDK 内核
- 自动中断检测 WDK 内核
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: fd5db43ff53c25aa74441935a850a48247b6c2b5
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67365784"
---
# <a name="using-the-connect_message_based-version-of-ioconnectinterruptex"></a>使用 CONNECT\_消息\_IoConnectInterruptEx 基于版本


对于 Windows Vista 和更高版本操作系统中，驱动程序可以使用 CONNECT\_消息\_基于版本[ **IoConnectInterruptEx** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioconnectinterruptex)注册 ISR 的驱动程序消息信号中断。 该驱动程序指定的连接值\_消息\_基于 for*参数*-&gt;**版本**，并使用的成员*参数*-&gt;**MessageBased**来指定该操作的其他参数。

-   *参数 * * *-&gt;MessageBased.PhysicalDeviceObject** 指定的设备是 PDO，ISR 服务。 系统使用的设备对象自动识别设备的消息信号中断。

-   *参数 * * *-&gt;MessageBased.MessageServiceRoutine** 指向[ *InterruptMessageService* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-kmessage_service_routine)例程，同时*参数 * * *-&gt;MessageBased.ServiceContext** 指定系统将作为传递的值*ServiceContext*参数*InterruptMessageService*。 该驱动程序可以使用此传递上下文信息。 有关传递上下文信息的详细信息，请参阅[提供 ISR 上下文信息](providing-isr-context-information.md)。

-   该驱动程序还可以指定回退*InterruptMessageService*例程中*参数 * **-&gt;MessageBased.FallBackServiceRoutine**。如果设备具有基于行的中断，但没有收到消息信号中断，系统将改为注册*InterruptMessageService*例程，以服务的基于线条的中断。在这种情况下，系统将传递*参数 * * *-&gt;MessageBased.ServiceContext** 作为*ServiceContext*参数[ *InterruptService*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-kservice_routine)。 **IoConnectInterruptEx**更新*参数 * * *-&gt;版本** 到 CONNECT\_行\_根据是否已注册的回退例程。

-   *参数 * * *-&gt;MessageBased.ConnectionContext** 指向一个变量来接收指向任一[ **IO\_中断\_消息\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_io_interrupt_message_info) (对于*InterruptMessageService*) 结构或[ **KINTERRUPT** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/eprocess)结构 (为*InterruptService*). 该驱动程序可以使用收到的指针来删除 ISR 有关详细信息，请参阅[删除 ISR](removing-an-isr.md)。

-   驱动程序可以选择指定在旋转锁*参数 * * *-&gt;MessageBased.SpinLock** ISR 与同步时要使用的系统 大多数驱动程序可以只需指定**NULL**启用系统分配旋转锁代表该驱动程序。 有关与 ISR 同步的详细信息，请参阅[对设备数据的同步访问](synchronizing-access-to-device-data.md)。

下面的代码示例演示如何注册*InterruptMessageService*例程使用 CONNECT\_消息\_基于。

```cpp
IO_CONNECT_INTERRUPT_PARAMETERS params;

// deviceExtension is a pointer to the driver's device extension. 
//     deviceExtension->IntInfo is a PVOID.
//     deviceExtension->IntType is a ULONG.
// deviceInterruptService is a pointer to the driver's InterruptService routine.
// deviceInterruptMessageService is a pointer to the driver's InterruptMessageService routine.
// PhysicalDeviceObject is a pointer to the device's PDO. 
// ServiceContext is a pointer to driver-specified context for the ISR.

RtlZeroMemory( &params, sizeof(IO_CONNECT_INTERRUPT_PARAMETERS) );
params.Version = CONNECT_MESSAGE_BASED;
params.MessageBased.PhysicalDeviceObject = PhysicalDeviceObject;
params.MessageBased.MessageServiceRoutine = deviceInterruptMessageService;
params.MessageBased.ServiceContext = ServiceContext;
params.MessageBased.SpinLock = NULL;
params.MessageBased.SynchronizeIrql = 0;
params.MessageBased.FloatingSave = FALSE;
params.MessageBased.FallBackServiceRoutine = deviceInterruptService;

status = IoConnectInterruptEx(&params);

if (NT_SUCCESS(status)) {
    // We record the type of ISR registered.
    devExt->IsrType = params.Version;
} else {
    // Operation failed. Handle error.
    ...
}
```

 

 




