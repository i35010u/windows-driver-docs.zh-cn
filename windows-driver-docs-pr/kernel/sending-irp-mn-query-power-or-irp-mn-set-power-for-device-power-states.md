---
title: 发送设备电源状态的 IRP_MN_QUERY_POWER 或 IRP_MN_SET_POWER
description: 发送设备电源状态的 IRP_MN_QUERY_POWER 或 IRP_MN_SET_POWER
keywords:
- IRP_MN_SET_POWER
- IRP_MN_QUERY_POWER
- 设备电源状态 WDK 内核
- 查询-power Irp WDK 电源管理
- power Irp WDK 内核，设备查询
- 查询电源状态
- 队列 Irp
- 设备查询电源 Irp WDK 内核
- 发送电源状态 Irp
- 设置-power Irp WDK 内核
- 设备设置电源 Irp WDK 内核
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 133fd271683d4cacc05f8c2e99cc9b7271c9532a
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96822271"
---
# <a name="sending-irp_mn_query_power-or-irp_mn_set_power-for-device-power-states"></a>发送 IRP \_ MN \_ QUERY \_ power 或 IRP \_ MN \_ \_ 为设备电源状态设置电源





设备电源策略所有者发送设备查询-power IRP ([**irp \_ MN \_ query \_ power**](./irp-mn-query-power.md)) 来确定驱动程序是否可以适应设备电源状态的变化，以及设备集-电源 IRP ([**IRP \_ MN \_ 设置 \_ power**](./irp-mn-set-power.md)) 以更改设备电源状态。  (此驱动程序还可以发送等待/唤醒 IRP，使其设备能够唤醒，以响应外部信号;有关详细信息，请参阅 [支持 Wake-Up 功能的设备](supporting-devices-that-have-wake-up-capabilities.md) 。 ) 

如果满足以下任一条件，则驱动程序应发送 [**IRP \_ MN \_ 查询 \_ 电源**](./irp-mn-query-power.md) 请求：

-   驱动程序接收系统查询-power IRP。

-   驱动程序准备将空闲设备置于睡眠状态，因此，必须查询较低的驱动程序，以确定这是否可行。

如果满足以下任一条件，则驱动程序应发送 [**IRP \_ MN \_ 设置 \_ 电源**](./irp-mn-set-power.md) 请求：

-   驱动程序已确定设备处于空闲状态，可以进入睡眠状态。

-   设备处于睡眠状态，必须重新进入工作状态才能处理等待 i/o。

-   驱动程序接收系统设置-power IRP。

驱动程序不得分配其自己的 power IRP;出于此目的，电源管理器提供了 [**PoRequestPowerIrp**](/windows-hardware/drivers/ddi/wdm/nf-wdm-porequestpowerirp) 例程。 作为 [处理电源 irp 的规则](calling-iocalldriver-versus-calling-pocalldriver.md) 说明， **PoRequestPowerIrp** 分配并发送 IRP，并结合 Windows 7 和 Windows Vista 中的 **IoCallDriver** () 或 windows Server 2003、windows XP 和 windows 2000) 中的 **PoCallDriver** (，确保所有电源请求均正确同步。 **PoRequestPowerIrp** 的调用方必须以 IRQL &lt; = 调度 \_ 级别运行。

下面是此例程的原型：

```cpp
NTSTATUS
PoRequestPowerIrp (
    IN PDEVICE_OBJECT DeviceObject,
    IN UCHAR MinorFunction,
    IN POWER_STATE PowerState,
    IN PREQUEST_POWER_COMPLETE CompletionFunction,
    IN PVOID Context,
    OUT PIRP *Irp OPTIONAL
    );
```

若要发送 IRP，驱动程序将 **调用 PoRequestPowerIrp**，并在 *DeviceObject* 中指定指向目标设备对象的指针，次要 IRP 代码 IRP \_ MN \_ 将 \_ power 或 IRP \_ MN \_ QUERY \_ power in MinorFunction，DevicePowerState 中的值 <em>PowerState</em> **PowerState** *MinorFunction***。键入**，并在 <em>PowerState</em>中输入设备电源状态 **。状态**。 在 Windows 98/Me 中， *DeviceObject* 必须指定基础设备的 PDO;在 Windows 2000 和更高版本的 Windows 中，此值可以指向同一设备堆栈中的 PDO 或驱动程序的 FDO。

如果驱动程序必须在所有其他驱动程序完成 IRP 后执行其他任务，则它应将指针传递到 *CompletionFunction* 中的电源完成函数。 在调用由驱动程序设置的所有 *IoCompletion* 例程后，i/o 管理器将调用 *CompletionFunction* ，因为它们将 IRP 向下传递。

每当设备电源策略所有者发送设备 power query IRP 时，它应随后从回调例程发送设备集电源 IRP， (*CompletionFunction*) 在调用 **PoRequestPowerIrp** 时指定的。 如果查询成功，则设置电源 IRP 会指定查询的电源状态。 如果查询失败，则设置电源 IRP 会重新断言当前设备电源状态。 重新断言当前状态很重要，因为驱动程序会在响应查询时排队 i/o;策略所有者必须发送集电源 IRP，以将设备堆栈中的驱动程序通知到开始处理排队 i/o 请求。

请记住，设备的策略所有者不仅会发送设备电源 IRP，还会在系统向下传递到设备堆栈时处理 IRP。 因此，此类驱动程序通常会在其 IRP 处理代码的一部分中设置 *IoCompletion* 例程 ([**IoSetCompletionRoutine**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iosetcompletionroutine)) ，尤其是在设备通电时。 *IoCompletion* 例程按序列调用， *IoCompletion* 例程由其他驱动程序和 *CompletionFunction* 之前设置。 有关详细信息，请参阅 [IoCompletion 例程 For Device Power irp](iocompletion-routines-for-device-power-irps.md)。

由于在调用 *CompletionFunction* 时已由所有驱动程序完成了 IRP，因此 *CompletionFunction* 不能使用它所发起的 IRP 调用 **IoCallDriver**、 **PoCallDriver** 或 **PoStartNextPowerIrp** 。 但 (它可能会为其他电源 IRP 调用这些例程。 ) 相反，此例程执行发起 IRP 的驱动程序所需的任何其他操作。 如果驱动程序已发送设备 IRP 来响应系统 IRP， *CompletionFunction* 可能会完成系统 irp。 有关详细信息，请参阅 [在设备电源策略所有者中处理 System Set-Power IRP](handling-a-system-set-power-irp-in-a-device-power-policy-owner.md)。

为响应对 **PoRequestPowerIrp** 的调用，电源管理器会分配一个 power IRP，并将其发送到设备的设备堆栈顶部。 Power manager 将返回指向分配的 IRP 的指针。

如果未发生错误，则 **PoRequestPowerIrp** 返回状态 " \_ 挂起"。 此状态表示 IRP 已成功发送并等待完成。 如果电源管理器无法分配 IRP，或者如果调用方指定了无效的次要电源 IRP 代码，则调用失败。

必须首先通过设备的基础总线驱动程序处理设备，然后再按照堆栈中的每个更高的驱动程序处理设备的电源请求。 因此，在发送 **PowerDeviceD0** 请求时，驱动程序必须确保在完成 IRP 并打开设备后，其 *CompletionFunction* 执行所需的任务。

 (**PowerDeviceD3**) 关闭设备时，设备堆栈中的每个驱动程序都必须保存其所有必要的上下文，并在将 IRP 发送到下一个较低版本的驱动程序之前执行任何必要的清理。 上下文信息和清理的范围取决于驱动程序的类型。 函数驱动程序必须保存硬件上下文;筛选器驱动程序可能需要保存其自己的软件上下文。 在这种情况下， *CompletionFunction* 集可以执行与已完成的电源 IRP 关联的操作，但驱动程序无法访问设备。

 

