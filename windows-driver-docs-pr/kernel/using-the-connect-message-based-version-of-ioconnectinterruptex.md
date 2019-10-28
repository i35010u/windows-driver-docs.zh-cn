---
title: 使用 IoConnectInterruptEx 的 CONNECT_MESSAGE_BASED 版本
description: 使用 IoConnectInterruptEx 的 CONNECT_MESSAGE_BASED 版本
ms.assetid: 8e06c6aa-85de-4ed2-ac0d-0179201d1272
keywords:
- IoConnectInterruptEx
- CONNECT_MESSAGE_BASED
- 消息-已发出信号中断 WDK 内核
- 自动中断检测 WDK 内核
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2b243220efad966ef8d1964fe5d727d3c13c5ffb
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838332"
---
# <a name="using-the-connect_message_based-version-of-ioconnectinterruptex"></a>使用连接\_基于 IoConnectInterruptEx 的消息\_版本


对于 Windows Vista 和更高版本的操作系统，驱动程序可以使用连接\_基于[**IoConnectInterruptEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioconnectinterruptex)的消息\_版本来注册 ISR 以获取驱动程序的消息发出的中断。 驱动程序将\_消息\_的值指定为-&gt;**版本**的*参数*，并使用-**MessageBased** *参数*的成员来指定其他参数操作。

-   *Parameters * * *-&gt;MessageBased. PhysicalDeviceObject** 指定 ISR 服务的设备的 PDO。 系统使用设备对象自动标识设备的消息信号中断。

-   *Parameters * * *-&gt;MessageBased. MessageServiceRoutine** 指向[*InterruptMessageService*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-kmessage_service_routine)例程，而*parameters * * *-&gt;MessageBased. ServiceContext** 指定系统作为*InterruptMessageService*的*ServiceContext*参数。 驱动程序可以使用它来传递上下文信息。 有关传递上下文信息的详细信息，请参阅[提供 ISR 上下文信息](providing-isr-context-information.md)。

-   驱动程序还可以在 Parameters *-中指定回退*InterruptMessageService*例程 ***&gt;FallBackServiceRoutine**。如果设备具有基于行的中断，但没有消息信号中断，则系统将改为注册*InterruptMessageService*例程来处理基于行的中断。在这种情况下，系统会将*参数 * *&gt;ServiceContext** 作为*ServiceContext*参数传递到[*InterruptService*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-kservice_routine)。 **IoConnectInterruptEx**更新*参数 * * * *&gt;版本**，以\_行\_注册回退例程。

-   *Parameters * * *-&gt;MessageBased. microsoft.sqlserver.replication.replicationobject.connectioncontext** 指向一个变量，该变量接收指向[**IO\_中断\_\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_interrupt_message_info)[**消息的指针。KINTERRUPT**](https://docs.microsoft.com/windows-hardware/drivers/kernel/eprocess)结构（适用于*InterruptService*）。 驱动程序可以使用接收到的指针来删除 ISR。 有关详细信息，请参阅[删除 ISR](removing-an-isr.md)。

-   驱动程序可以选择指定参数中的自旋锁 ** * *-&gt;旋转锁** 以便系统在与 ISR 同步时使用。 大多数驱动程序可以仅指定**NULL** ，使系统能够代表驱动程序分配自旋锁。 有关与 ISR 同步的详细信息，请参阅[同步对设备数据的访问](synchronizing-access-to-device-data.md)。

下面的代码示例演示如何通过使用 CONNECT\_MESSAGE\_来注册*InterruptMessageService*例程。

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

 

 




