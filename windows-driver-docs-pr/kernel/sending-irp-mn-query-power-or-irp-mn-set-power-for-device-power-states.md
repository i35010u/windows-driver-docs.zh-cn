---
title: 发送设备电源状态的 IRP_MN_QUERY_POWER 或 IRP_MN_SET_POWER
description: 发送设备电源状态的 IRP_MN_QUERY_POWER 或 IRP_MN_SET_POWER
ms.assetid: 58f65138-abb9-4bb8-bf9b-14f17347e309
keywords:
- IRP_MN_SET_POWER
- IRP_MN_QUERY_POWER
- 设备电源状态 WDK 内核
- 查询能耗 Irp WDK 电源管理
- power Irp WDK 内核，设备查询
- 查询能耗状态
- 队列的 Irp
- 设备查询 power Irp WDK 内核
- 电源状态 Irp 发送
- 设置 power Irp WDK 内核
- 设备设置 power Irp WDK 的内核
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: e15f682310e29ca2f3a5392b951f00c2633f5bb7
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63342659"
---
# <a name="sending-irpmnquerypower-or-irpmnsetpower-for-device-power-states"></a>发送 IRP\_MN\_查询\_电源或 IRP\_MN\_设置\_的电源可用于设备的电源状态





设备电源策略所有者发送设备查询能耗 IRP ([**IRP\_MN\_查询\_POWER**](https://msdn.microsoft.com/library/windows/hardware/ff551699)) 以确定较低的驱动程序是否可以容纳中的更改设备电源状态和设备组的电源 IRP ([**IRP\_MN\_设置\_POWER**](https://msdn.microsoft.com/library/windows/hardware/ff551744)) 若要更改设备电源状态。 (此驱动程序还可以发送等待/唤醒 IRP，以允许其设备被唤醒以响应外部的信号; 请参阅[支持设备的已唤醒功能](supporting-devices-that-have-wake-up-capabilities.md)有关详细信息。)

驱动程序应发送[ **IRP\_MN\_查询\_POWER** ](https://msdn.microsoft.com/library/windows/hardware/ff551699)请求以下之一为 true 时：

-   驱动程序收到一个系统查询能耗 IRP。

-   该驱动程序正在准备，以便空闲设备置于睡眠状态，因此必须查询较低的驱动程序，以了解这样做因此是否可行。

驱动程序应发送[ **IRP\_MN\_设置\_POWER** ](https://msdn.microsoft.com/library/windows/hardware/ff551744)请求时的以下任何为 true:

-   该驱动程序已确定该设备处于空闲状态且可置于睡眠状态。

-   设备处于睡眠状态，并且必须重新输入来处理正在等待 I/O 的工作状态。

-   驱动程序收到一个系统集 power IRP。

驱动程序必须分配它自己的强大功能 IRP;电源管理器提供了[ **PoRequestPowerIrp** ](https://msdn.microsoft.com/library/windows/hardware/ff559734)例程实现此目的。 作为[规则处理 Power Irp](rules-for-handling-power-irps.md)介绍了， **PoRequestPowerIrp**分配，并将发送 IRP，并结合**IoCallDriver** （在 Windows 7 和 Windows Vista）或**PoCallDriver** (Windows Server 2003 中，Windows XP 和 Windows 2000），可确保正确同步所有电源请求。 调用方**PoRequestPowerIrp**必须在 IRQL 运行&lt;= 调度\_级别。

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

若要发送 IRP，驱动程序调用**PoRequestPowerIrp**，指定指向目标设备对象中的*DeviceObject*，次要 IRP 代码 IRP\_MN\_集\_电源或 IRP\_MN\_查询\_中的 POWER *MinorFunction*，值**DevicePowerState**中<em>PowerState</em>**.类型**，并在设备电源状态<em>PowerState</em>**。状态**。 在 Windows 98 / Me *DeviceObject*必须指定基础设备 PDO; 在 Windows 2000 和更高版本的 Windows 中，此值可以指向 PDO 或 FDO 相同设备堆栈中的驱动程序。

所有其他驱动程序完成 IRP 后，驱动程序必须执行其他任务，则它应传递到中的 power 完成函数的指针*CompletionFunction*。 I/O 管理器调用*CompletionFunction*调用所有后*IoCompletion*例程作为它们传入 IRP 的驱动程序设置向下堆栈。

每当设备电源策略所有者发送设备 power 查询 IRP，它随后应发送设备集 power IRP 的回调例程从 (*CompletionFunction*)，在调用中指定它**PoRequestPowerIrp**。 如果查询成功，集 power IRP 指定查询的能耗状态。 如果查询失败，集 power IRP 重新断言当前设备电源状态。 重新声明的当前状态很重要，因为驱动程序以响应查询，排队 I/O策略所有者必须发送集 power IRP 通知以开始处理排队的 I/O 请求其设备堆栈中的驱动程序。

请记住设备的策略所有者不仅将发送设备电源 IRP 而且还处理 IRP，因为它可以传递设备堆栈。 因此，此类驱动程序通常设置*IoCompletion*例程 (与[ **IoSetCompletionRoutine**](https://msdn.microsoft.com/library/windows/hardware/ff549679)) 作为其 IRP 处理代码的一部分，特别是该设备时注册提供强大支持。 *IoCompletion*具有序列中调用例程*IoCompletion*例程设置的其他驱动程序和前*CompletionFunction*。 有关详细信息，请参阅[设备电源 Irp 的 IoCompletion 例程](iocompletion-routines-for-device-power-irps.md)。

因为 IRP 已经完成的所有驱动程序时*CompletionFunction*调用时， *CompletionFunction*不能调用**IoCallDriver**， **PoCallDriver**，或**PoStartNextPowerIrp**与产生的 IRP。 （它可能会但是，调用这些例程用于不同的电源 IRP。）相反，此例程执行发起 IRP 的驱动程序所需的任何其他操作。 如果该驱动程序以响应系统 IRP，发送设备 IRP *CompletionFunction*可能完成系统 IRP。 有关详细信息，请参阅[处理设备电源策略所有者中系统集 Power IRP](handling-a-system-set-power-irp-in-a-device-power-policy-owner.md)。

以响应对的调用**PoRequestPowerIrp**，电源管理器分配能力 IRP，并将其发送到设备的设备堆栈的顶部。 电源管理器返回指向已分配的 IRP 的指针。

如果不发生任何错误， **PoRequestPowerIrp**将返回状态\_PENDING。 此状态表示 IRP 已成功发送，并且正在等待完成。 如果电源管理器不能分配 IRP，或如果调用方已指定了无效的次要 power IRP 代码，调用将失败。

按设备的基础总线驱动程序，然后按堆栈中每个依次升高的驱动程序，必须首先处理设备保持开机状态的请求。 因此，当发送**PowerDeviceD0**请求，该驱动程序必须确保其*CompletionFunction* IRP 完成后打开设备上执行所需的任务。

当关闭设备电源 (**PowerDeviceD3**)，设备堆栈中的每个驱动程序必须保存所有必要的上下文和任何必需执行的清理操作之前将 IRP 发送到下一步低驱动程序。 上下文信息和清除的范围取决于驱动程序的类型。 功能驱动程序必须保存硬件上下文;筛选器驱动程序可能需要保存其自己软件的上下文。 一个*CompletionFunction*集在此情况下可能需要与已完成 power IRP，关联的操作，但该驱动程序无法访问设备。

 

 




