---
title: 使用 IoConnectInterruptEx 的 CONNECT_FULLY_SPECIFIED 版本
description: 使用 IoConnectInterruptEx 的 CONNECT_FULLY_SPECIFIED 版本
ms.assetid: 5b75c32e-77e5-4761-b709-fedb8e33b57a
keywords:
- IoConnectInterruptEx
- CONNECT_FULLY_SPECIFIED
- 手动中断检测 WDK 内核
- 基于行的中断 WDK 内核
- 消息-已发出信号中断 WDK 内核
- FullySpecified
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 770cd0c0c71ffc247c6c0fd06afffec49c8da7d8
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838333"
---
# <a name="using-the-connect_fully_specified-version-of-ioconnectinterruptex"></a>使用连接\_完全\_指定版本的 IoConnectInterruptEx


驱动程序可以使用连接\_完全\_指定版本的[**IoConnectInterruptEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioconnectinterruptex)为特定中断注册[*InterruptService*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-kservice_routine)例程。 驱动程序可以从 Windows Vista 开始使用完全\_指定版本的连接\_。 通过链接到 Iointex 库，驱动程序可以在 Windows 2000、Windows XP 和 Windows Server 2003 中完全\_指定版本\_使用连接。 有关详细信息，请参阅[Windows Vista 之前的使用 IoConnectInterruptEx](using-ioconnectinterruptex-prior-to-windows-vista.md)。

驱动程序指定值 "连接\_完全\_为参数指定 ** * *&gt;版本**，并使用参数的成员 ** * *-&gt;FullySpecified** 来指定操作的其他参数：

-   *Parameters * * *-&gt;FullySpecified. PhysicalDeviceObject** 指定 ISR 服务的设备的 PDO。

-   *参数*-&gt;**ServiceRoutine**指向*InterruptService*例程，而*参数*-&gt;**FullySpecified**。**ServiceContext**指定系统作为*ServiceContext*参数传递到*InterruptService*的值。 驱动程序可以使用它来传递上下文信息。 有关传递上下文信息的详细信息，请参阅[提供 ISR 上下文信息](providing-isr-context-information.md)。

-   驱动程序提供指向 * Parameters * **-&gt;FullySpecified InterruptObject**中的 PKINTERRUPT 变量的指针。 **IoConnectInterruptEx**例程将此变量设置为指向中断的中断对象，可在[删除 ISR](removing-an-isr.md)时使用该对象。

-   驱动程序可以选择指定参数中的自旋锁 ** * *-&gt;旋转锁** 以便系统在与 ISR 同步时使用。 大多数驱动程序可以仅指定**NULL** ，使系统能够代表驱动程序分配自旋锁。 有关与 ISR 同步的详细信息，请参阅[同步对设备数据的访问](synchronizing-access-to-device-data.md)。

驱动程序必须在 * Parameters * **-&gt;FullySpecified**的其他成员中指定中断的键属性。 系统在将[**irp\_MN\_START\_DEVICE**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-start-device) IRP 发送到驱动程序时，在[**CM\_部分\_资源\_描述符**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_cm_partial_resource_descriptor)结构中提供必需的信息。

系统为每个中断提供**CM\_部分\_资源\_描述符**结构，**类型**成员等于**CmResourceTypeInterrupt**。 对于消息发出信号的中断，设置了**标志**成员的 CM\_资源\_中断\_消息位;否则，它会被清除。

**CM\_分部\_资源\_描述符**的**u. 中断**成员包含基于行的中断的说明，而**MessageInterrupt**成员包含对消息信号中断。 下表指示在**CM\_部分\_资源\_描述符**结构中的位置，以查找设置*参数*的成员所需的信息-&gt;**FullySpecified**中断的类型。 有关详细信息，请参阅表后面的代码示例。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>成员</th>
<th>基于行的中断</th>
<th>消息信号中断</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>ShareVector</strong></p></td>
<td><p><strong>ShareDisposition</strong></p></td>
<td><p><strong>ShareDisposition</strong></p></td>
</tr>
<tr class="even">
<td><p><strong>向量</strong></p></td>
<td><p><strong>手杖形</strong></p></td>
<td><p><strong>MessageInterrupt 转换</strong></p></td>
</tr>
<tr class="odd">
<td><p><strong>Irql</strong></p></td>
<td><p><strong>手杖</strong></p></td>
<td><p><strong>MessageInterrupt 级别</strong></p></td>
</tr>
<tr class="even">
<td><p><strong>InterruptMode</strong></p></td>
<td><p>CM_RESOURCE_INTERRUPT_LATCHED<strong>标志</strong>&</p></td>
<td><p>CM_RESOURCE_INTERRUPT_LATCHED<strong>标志</strong>&</p></td>
</tr>
<tr class="odd">
<td><p><strong>ProcessorEnableMask</strong></p></td>
<td><p><strong>手杖. 关联</strong></p></td>
<td><p><strong>MessageInterrupt （& e）</strong></p></td>
</tr>
</tbody>
</table>

 

在 Windows Vista 和更高版本的 Windows 上，驱动程序将仅接收**CM\_部分\_资源\_描述符**结构。

下面的代码示例演示如何使用 CONNECT\_完全\_指定注册*InterruptService*例程。

```cpp
IO_CONNECT_INTERRUPT_PARAMETERS params;

// deviceExtension is a pointer to the driver's device extension. 
//     deviceExtension->IntObj is a PKINTERRUPT.
// deviceInterruptService is a pointer to the driver's InterruptService routine.
// IntResource is a CM_PARTIAL_RESOURCE_DESCRIPTOR structure of either type CmResourceTypeInterrupt or CmResourceTypeMessageInterrupt.
// PhysicalDeviceObject is a pointer to the device's PDO. 
// ServiceContext is a pointer to driver-specified context for the ISR.

RtlZeroMemory( &params, sizeof(IO_CONNECT_INTERRUPT_PARAMETERS) );
params.Version = CONNECT_FULLY_SPECIFIED;
params.FullySpecified.PhysicalDeviceObject = PhysicalDeviceObject;
params.FullySpecified.InterruptObject = &devExt->IntObj;
params.FullySpecified.ServiceRoutine = deviceInterruptService;
params.FullySpecified.ServiceContext = ServiceContext;
params.FullySpecified.FloatingSave = FALSE;
params.FullySpecified.SpinLock = NULL;

if (IntResource->Flags & CM_RESOURCE_INTERRUPT_MESSAGE) {
    // The resource is for a message-signaled interrupt. Use the u.MessageInterrupt.Translated member of IntResource.
 
    params.FullySpecified.Vector = IntResource->u.MessageInterrupt.Translated.Vector;
    params.FullySpecified.Irql = (KIRQL)IntResource->u.MessageInterrupt.Translated.Level;
    params.FullySpecified.SynchronizeIrql = (KIRQL)IntResource->u.MessageInterrupt.Translated.Level;
    params.FullySpecified.ProcessorEnableMask = IntResource->u.MessageInterrupt.Translated.Affinity;
} else {
    // The resource is for a line-based interrupt. Use the u.Interrupt member of IntResource.
 
    params.FullySpecified.Vector = IntResource->u.Interrupt.Vector;
    params.FullySpecified.Irql = (KIRQL)IntResource->u.Interrupt.Level;
    params.FullySpecified.SynchronizeIrql = (KIRQL)IntResource->u.Interrupt.Level;
    params.FullySpecified.ProcessorEnableMask = IntResource->u.Interrupt.Affinity;
}

params.FullySpecified.InterruptMode = (IntResource->Flags & CM_RESOURCE_INTERRUPT_LATCHED ? Latched : LevelSensitive);
params.FullySpecified.ShareVector = (BOOLEAN)(IntResource->ShareDisposition == CmResourceShareShared);

status = IoConnectInterruptEx(&params);

if (!NT_SUCCESS(status)) {
    ...
}
```

 

 




