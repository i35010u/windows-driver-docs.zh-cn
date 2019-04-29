---
title: 使用 IoConnectInterruptEx 的 CONNECT_FULLY_SPECIFIED 版本
description: 使用 IoConnectInterruptEx 的 CONNECT_FULLY_SPECIFIED 版本
ms.assetid: 5b75c32e-77e5-4761-b709-fedb8e33b57a
keywords:
- IoConnectInterruptEx
- CONNECT_FULLY_SPECIFIED
- 手动中断检测 WDK 内核
- 基于行的中断 WDK 内核
- 消息信号中断 WDK 内核
- FullySpecified
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 32aa0c467d8df280816e7a8fbeb08eec8f71c3de
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63359205"
---
# <a name="using-the-connectfullyspecified-version-of-ioconnectinterruptex"></a>使用 CONNECT\_完全\_IoConnectInterruptEx 指定版本


驱动程序可以使用 CONNECT\_完全\_SPECIFIED 新版[ **IoConnectInterruptEx** ](https://msdn.microsoft.com/library/windows/hardware/ff548378)注册[ *InterruptService*](https://msdn.microsoft.com/library/windows/hardware/ff547958)特定中断例程。 驱动程序可以使用 CONNECT\_完全\_从 Windows Vista 开始的指定版本。 通过将链接到 Iointex.lib 库，该驱动程序可以使用 CONNECT\_完全\_Windows 2000，Windows XP 和 Windows Server 2003 中的指定版本。 有关详细信息，请参阅[使用之前为 Windows Vista 的 IoConnectInterruptEx](using-ioconnectinterruptex-prior-to-windows-vista.md)。

该驱动程序指定的连接值\_完全\_为指定*参数 * * *-&gt;版本**，并使用的成员*参数 * * *-&gt;FullySpecified** 来指定该操作的其他参数：

-   *参数 * * *-&gt;FullySpecified.PhysicalDeviceObject** 指定的设备是 PDO，ISR 服务。

-   *参数*-&gt;**FullySpecified.ServiceRoutine**指向*InterruptService*例程，同时*参数* - &gt; **FullySpecified**。**ServiceContext**指定系统将作为传递的值*ServiceContext*参数*InterruptService*。 该驱动程序可以使用此传递上下文信息。 有关传递上下文信息的详细信息，请参阅[提供 ISR 上下文信息](providing-isr-context-information.md)。

-   该驱动程序提供了指向 PKINTERRUPT 变量中的 * 参数 ***-&gt;FullySpecified.InterruptObject**。 **IoConnectInterruptEx**例程将此变量设置为指向中断的中断对象后者可以时要使用[删除 ISR](removing-an-isr.md)。

-   驱动程序可以选择指定在旋转锁*参数 * * *-&gt;FullySpecified.SpinLock** ISR 与同步时要使用的系统 大多数驱动程序可以只需指定**NULL**启用系统分配旋转锁代表该驱动程序。 有关与 ISR 同步的详细信息，请参阅[对设备数据的同步访问](synchronizing-access-to-device-data.md)。

该驱动程序必须指定中断的键属性中的其他成员 * 参数 ***-&gt;FullySpecified**。 系统提供的数组中所需的信息[ **CM\_分部\_资源\_描述符**](https://msdn.microsoft.com/library/windows/hardware/ff541977)结构会在发送时[**IRP\_MN\_启动\_设备**](https://msdn.microsoft.com/library/windows/hardware/ff551749) IRP 到驱动程序。

系统提供的每个中断**CM\_分部\_资源\_描述符**结构**类型**成员等于**CmResourceTypeInterrupt**。 消息信号中断，CM\_资源\_中断\_消息位**标志**成员设置; 否则，清除它。

**U.Interrupt**的成员**CM\_分部\_资源\_描述符**包含说明的基于线条的中断，而**u。MessageInterrupt.Translated**成员包含的消息信号中断的说明。 下表中指示的位置， **CM\_分部\_资源\_描述符**结构，以查找所需设置的成员的信息*参数*- &gt; **FullySpecified**两种类型的中断。 有关详细信息，请参阅表后面的代码示例。

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
<td><p><strong>Vector</strong></p></td>
<td><p><strong>u.Interrupt.Vector</strong></p></td>
<td><p><strong>u.MessageInterrupt.Translated.Vector</strong></p></td>
</tr>
<tr class="odd">
<td><p><strong>Irql</strong></p></td>
<td><p><strong>u.Interrupt.Level</strong></p></td>
<td><p><strong>u.MessageInterrupt.Translated.Level</strong></p></td>
</tr>
<tr class="even">
<td><p><strong>InterruptMode</strong></p></td>
<td><p><strong>标志</strong> &amp; CM_RESOURCE_INTERRUPT_LATCHED</p></td>
<td><p><strong>标志</strong> &amp; CM_RESOURCE_INTERRUPT_LATCHED</p></td>
</tr>
<tr class="odd">
<td><p><strong>ProcessorEnableMask</strong></p></td>
<td><p><strong>u.Interrupt.Affinity</strong></p></td>
<td><p><strong>u.MessageInterrupt.Translated.Affinity</strong></p></td>
</tr>
</tbody>
</table>

 

驱动程序将仅收到**CM\_分部\_资源\_描述符**消息信号中断在 Windows Vista 和更高版本的 Windows 上的结构。

下面的代码示例演示如何注册*InterruptService*例程使用 CONNECT\_完全\_指定。

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

 

 




