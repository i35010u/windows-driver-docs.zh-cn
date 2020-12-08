---
title: 使用 IoConnectInterruptEx 的 CONNECT_FULLY_SPECIFIED 版本
description: 使用 IoConnectInterruptEx 的 CONNECT_FULLY_SPECIFIED 版本
keywords:
- IoConnectInterruptEx
- CONNECT_FULLY_SPECIFIED
- 手动中断检测 WDK 内核
- 基于行的中断 WDK 内核
- 消息-已发出信号中断 WDK 内核
- FullySpecified
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3bf4cc9b937cdf40d8ab1c3cbd0b8a46c6ecabb4
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96803761"
---
# <a name="using-the-connect_fully_specified-version-of-ioconnectinterruptex"></a>使用 IoConnectInterruptEx 的 CONNECT \_ 完全 \_ 指定版本


驱动程序可以使用 IoConnectInterruptEx 的 CONNECT \_ 完全 \_ 指定版本 [**IoConnectInterruptEx**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioconnectinterruptex)向特定中断注册 [*InterruptService*](/windows-hardware/drivers/ddi/wdm/nc-wdm-kservice_routine)例程。 驱动程序可以使用 \_ \_ 从 Windows Vista 开始的连接完全指定的版本。 通过链接到 Iointex 库，驱动程序可以使用 \_ \_ windows 2000、windows XP 和 windows Server 2003 中的 CONNECT 完全指定版本。 有关详细信息，请参阅 [Windows Vista 之前的使用 IoConnectInterruptEx](using-ioconnectinterruptex-prior-to-windows-vista.md)。

驱动程序指定值为 \_ \_ *parameters * * * * &gt; 版本**，并使用参数的成员 ** * *- &gt; FullySpecified** 来指定操作的其他参数：

-   *Parameters * * *- &gt;FullySpecified. PhysicalDeviceObject** 指定 ISR 服务的设备的 PDO。

-   *Parameters* - 参数 &gt;**FullySpecified ServiceRoutine** 指向 *InterruptService* 例程，而 *参数* - &gt; **FullySpecified**。**ServiceContext** 指定系统作为 *ServiceContext* 参数传递到 *InterruptService* 的值。 驱动程序可以使用它来传递上下文信息。 有关传递上下文信息的详细信息，请参阅 [提供 ISR 上下文信息](providing-isr-context-information.md)。

-   驱动程序提供指向 * Parameters ***- &gt; FullySpecified. InterruptObject** 中的 PKINTERRUPT 变量的指针。 **IoConnectInterruptEx** 例程将此变量设置为指向中断的中断对象，可在 [删除 ISR](removing-an-isr.md)时使用该对象。

-   驱动程序可以选择在参数中指定一个自旋锁 ** * * &gt; FullySpecified**，以便在与 ISR 同步时使用系统。 大多数驱动程序可以仅指定 **NULL** ，使系统能够代表驱动程序分配自旋锁。 有关与 ISR 同步的详细信息，请参阅 [同步对设备数据的访问](synchronizing-access-to-device-data.md)。

驱动程序必须在 * Parameters ***- &gt; FullySpecified** 的其他成员中指定中断的键属性。 系统在将 [**IRP \_ MN \_ 启动 \_ 设备**](./irp-mn-start-device.md)irp 发送到驱动程序时，提供 [**CM \_ 部分 \_ 资源 \_ 描述符**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_cm_partial_resource_descriptor)结构的必要信息。

系统为每个中断提供一个 **CM \_ 部分 \_ 资源 \_ 描述符** 结构，其 **类型** 成员等于 **CmResourceTypeInterrupt**。 对于消息发出信号中断， \_ \_ \_ 将设置 **标志** 成员的 CM 资源中断消息位; 否则，将清除该消息。

**CM \_ 部分 \_ 资源 \_ 描述符** 的 " **u. 中断**" 成员包含基于行的中断的说明，而 **MessageInterrupt** 成员包含消息终止中断的说明。 下表指示在 **CM \_ 部分 \_ 资源 \_ 描述符** 结构中查找为 *Parameters* - &gt; 这两种类型的中断设置参数 **FullySpecified** 的成员所需的信息。 有关详细信息，请参阅表后面的代码示例。

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
<td><p><strong>标志</strong> & CM_RESOURCE_INTERRUPT_LATCHED</p></td>
<td><p><strong>标志</strong> & CM_RESOURCE_INTERRUPT_LATCHED</p></td>
</tr>
<tr class="odd">
<td><p><strong>ProcessorEnableMask</strong></p></td>
<td><p><strong>手杖. 关联</strong></p></td>
<td><p><strong>MessageInterrupt （& e）</strong></p></td>
</tr>
</tbody>
</table>

 

对于 Windows Vista 和更高版本的 Windows 上的消息发出的中断，驱动程序将只接收 **CM \_ 部分 \_ 资源 \_ 说明符** 结构。

下面的代码示例演示如何使用完全指定 *InterruptService* 的 CONNECT 注册 InterruptService \_ 例程 \_ 。

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

 

