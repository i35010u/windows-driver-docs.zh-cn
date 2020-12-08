---
title: 使用 IoConnectInterruptEx 的 CONNECT_MESSAGE_BASED 版本
description: 使用 IoConnectInterruptEx 的 CONNECT_MESSAGE_BASED 版本
keywords:
- IoConnectInterruptEx
- CONNECT_MESSAGE_BASED
- 消息-已发出信号中断 WDK 内核
- 自动中断检测 WDK 内核
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: a321ade0f1babbc6e535b6b8a2479778a4bb4e3f
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96803757"
---
# <a name="using-the-connect_message_based-version-of-ioconnectinterruptex"></a>使用基于连接 \_ 消息 \_ 的 IoConnectInterruptEx 版本


对于 Windows Vista 和更高版本的操作系统，驱动程序可以使用 \_ 基于连接消息 \_ 的 [**IoConnectInterruptEx**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioconnectinterruptex) 版本为驱动程序的消息终止中断注册 ISR。 驱动程序指定值 \_ \_ "基于参数的连接消息 *Parameters* - &gt; "**版本**，并使用 *参数* - &gt; **MessageBased** 的成员指定操作的其他参数。

-   *Parameters * * *- &gt;MessageBased. PhysicalDeviceObject** 指定 ISR 服务的设备的 PDO。 系统使用设备对象自动标识设备的消息信号中断。

-   *Parameters * * *- &gt;MessageBased. MessageServiceRoutine** 指向 [*InterruptMessageService*](/windows-hardware/drivers/ddi/wdm/nc-wdm-kmessage_service_routine) 例程，而 *Parameters * * *- &gt; MessageBased. ServiceContext** 指定系统作为 *ServiceContext 参数传递* 到 *InterruptMessageService* 的值。 驱动程序可以使用它来传递上下文信息。 有关传递上下文信息的详细信息，请参阅 [提供 ISR 上下文信息](providing-isr-context-information.md)。

-   驱动程序还可以在 *InterruptMessageService* *Parameters ***- &gt; MessageBased. FallBackServiceRoutine** 中指定回退 InterruptMessageService 例程。如果设备具有基于行的中断，但没有消息信号中断，则系统将改为注册 *InterruptMessageService* 例程来处理基于行的中断。在这种情况下，系统会将 *参数 * * *- &gt; MessageBased. ServiceContext** 作为 *ServiceContext* 参数传递到 [*InterruptService*](/windows-hardware/drivers/ddi/wdm/nc-wdm-kservice_routine)。 **IoConnectInterruptEx** 将更新 *参数 * * * * &gt; 版本**，以便 \_ \_ 在它注册了回退例程的情况时连接行。

-   *Parameters * * *- &gt;MessageBased. Microsoft.sqlserver.replication.replicationobject.connectioncontext** 指向一个变量，该变量接收指向 *InterruptMessageService*) 结构的 [**IO \_ 中断 \_ 消息 \_ 信息**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_interrupt_message_info) (或 *InterruptService*)  ([**KINTERRUPT**](./eprocess.md)结构的指针。 驱动程序可以使用接收到的指针来删除 ISR。 有关详细信息，请参阅 [删除 ISR](removing-an-isr.md)。

-   驱动程序可以选择在参数中指定一个自旋锁 ** * * &gt; MessageBased**，以便在与 ISR 同步时使用系统。 大多数驱动程序可以仅指定 **NULL** ，使系统能够代表驱动程序分配自旋锁。 有关与 ISR 同步的详细信息，请参阅 [同步对设备数据的访问](synchronizing-access-to-device-data.md)。

下面的代码示例演示如何使用基于的 CONNECT 消息注册 *InterruptMessageService* 例程 \_ \_ 。

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

 

