---
title: 处理设备断电 IRP
description: 处理设备断电 IRP
ms.assetid: 2f4591d6-5bd0-45db-b02d-cf9dd59c3888
keywords:
- 设置 power Irp WDK 内核
- 设备设置 power Irp WDK 的内核
- power Irp WDK 内核，设备更改
- 电源关闭 Irp WDK 内核
- 上下文信息 WDK 电源管理
- 关闭电源管理 WDK 内核
- 关闭 power WDK 内核
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5aecf999f961747a9ca4e67ee07ca99d9ec55648
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63331265"
---
# <a name="handling-device-power-down-irps"></a>处理设备断电 IRP





设备电源关闭 IRP 指定次要函数代码[ **IRP\_MN\_设置\_POWER** ](https://msdn.microsoft.com/library/windows/hardware/ff551744)和设备电源状态 (**PowerDeviceD0**， **PowerDeviceD1**， **PowerDeviceD2**，或**PowerDeviceD3**) 即供电小于或等于当前的设备电源状态。 驱动程序必须处理电源关闭 IRP IRP 传输时下设备堆栈。 更高级别的驱动程序必须处理 IRP 之前较低级驱动程序。 具有要执行的特定于设备的任务的驱动程序应立即将 IRP 传递给下一个较低驱动程序。

下图显示所涉及步骤中处理此类 IRP。

![说明处理设备电源关闭请求的关系图](images/devd3.png)

如果指定了 IRP **PowerDeviceD3**，功能驱动程序通常应执行以下任务：

-   调用[ **IoAcquireRemoveLock**](https://msdn.microsoft.com/library/windows/hardware/ff548204)，并传递当前 IRP，以确保该驱动程序不会接收即插即用[ **IRP\_MN\_删除\_设备**](https://msdn.microsoft.com/library/windows/hardware/ff551738)请求，而同时处理 IRP 的能力。

    如果**IoAcquireRemoveLock**返回失败状态，该驱动程序不应继续处理 IRP。 相反，从 Windows Vista 开始，驱动程序应调用[ **IoCompleteRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff548343)完成 IRP，然后返回失败状态。 在 Windows Server 2003、 Windows XP 和 Windows 2000 中，该驱动程序应调用**IoCompleteRequest**若要完成 IRP，然后调用[ **PoStartNextPowerIrp** ](https://msdn.microsoft.com/library/windows/hardware/ff559776)启动接下来 power IRP，，然后返回失败状态。

-   执行之前，必须完成删除设备电源，如关闭设备、 完成或刷新所有挂起的 I/O，禁用中断，任何特定于设备的任务[队列后续传入 Irp](queuing-i-o-requests-while-a-device-is-sleeping.md)，并保存设备从其还原或重新初始化设备上下文。

    该驱动程序并不会导致长时间的延迟 （例如，用户可能会发现不合理的此类设备延迟） 时处理 IRP。

    该驱动程序应排队 I/O 的任何传入请求，直到设备返回到工作状态。

-   可能是检查处的值**Parameters.Power.ShutdownType**。 如果系统处于活动状态，集 power IRP **ShutdownType**提供有关系统 IRP 的信息。 此值的详细信息，请参阅[系统电源操作](system-power-actions.md)。

    休眠路径上的设备的驱动程序必须检查此值。 如果**ShutdownType**是**PowerActionHibernate**，驱动程序应保存将设备还原所需的任何上下文，但不是应关闭设备电源。

-   更改设备的物理电源状态，如果驱动程序能够执行此操作，则相应更改。

-   调用[ **PoSetPowerState** ](https://msdn.microsoft.com/library/windows/hardware/ff559765)通知电源管理器的新设备电源状态。

-   调用[ **IoCopyCurrentIrpStackLocationToNext** ](https://msdn.microsoft.com/library/windows/hardware/ff548387)设置下一步低驱动程序的堆栈位置。

-   设置*IoCompletion*调用的例程[ **PoStartNextPowerIrp** ](https://msdn.microsoft.com/library/windows/hardware/ff559776) ，该值指示该驱动程序已准备好处理 IRP 的下一个幂。 在 Windows 7 和 Windows Vista 不需要此步骤。

-   调用[ **IoCallDriver** ](https://msdn.microsoft.com/library/windows/hardware/ff548336) （在 Windows 7 和 Windows Vista） 或调用[ **PoCallDriver** ](https://msdn.microsoft.com/library/windows/hardware/ff559654) （在 Windows Server 2003、 Windows XP 和 Windows2000) 以将 IRP 传递给下一个较低驱动程序。 必须将 IRP 传递到总线驱动程序，可以完成 IRP。

-   调用[ **IoReleaseRemoveLock** ](https://msdn.microsoft.com/library/windows/hardware/ff549560)释放以前获取的锁。

-   返回状态\_PENDING。

驱动程序必须保存设备上下文的任何信息，并转发 IRP 之前设置新的电源状态。 上下文信息应包含，最小值，请求新的电源状态。 它还应包括驱动程序将需要电源后的任何其他信息。 IRP 已经完成并关闭该设备后，该驱动程序将无法再访问设备和设备上下文不可用。

每个驱动程序必须将 IRP 传递给下一个较低驱动程序。 总线驱动程序将关闭 （如果有此） 的设备，当 IRP 到达总线驱动程序时，调用[ **PoSetPowerState** ](https://msdn.microsoft.com/library/windows/hardware/ff559765)通知电源管理器，并完成 IRP。

但是，如果总线驱动程序服务 （休眠设备），它应检查是否的值**ShutdownType**在 IRP 是 PowerSystemHibernate。 如果因此，总线驱动程序应调用**PoSetPowerState**报告 PowerDeviceD3 但不是应关闭设备电源。 保存休眠文件，以及系统的其余部分后，设备将会关闭。

别忘了向下其子设备功能，总线驱动程序可以选择关闭其总线还电源。 此类行为与设备相关。

如果 IRP 指定任何其他状态 （D0、 D1 或 D2），所需的驱动程序操作是依赖于设备的。 通常情况下，支持这些状态的设备可以快速返回到工作状态 I/O 请求到达时。 此类设备的驱动程序必须完成所有挂起的 I/O 请求、 对任何新请求进行排队和转发到下一步低驱动程序 IRP 之前保存所有必要的上下文。 当 IRP 到达总线驱动程序时，它在请求的状态设置硬件。 处于睡眠状态时，驱动程序无法访问设备。

在某些情况下，函数或筛选器驱动程序可能会收到设备电源设备已处于 D0 状态时指定 PowerDeviceD0 IRP。 该驱动程序应处理此 IRP，像任何其他组 power IRP： 的挂起 I/O 请求完成，传入的 I/O 请求排队，设置[ *IoCompletion* ](https://msdn.microsoft.com/library/windows/hardware/ff548354)例程，并传递到下一步越低 IRP驱动程序。 驱动程序不得，但是，更改设备的硬件设置。 当总线驱动程序接收 IRP 时，它应只需完成 IRP。 IRP 完成后，函数和筛选器驱动程序可以处理任何排队的请求。 排队 I/O IRP 完成之前消除了发生较低的驱动程序尝试更改设备寄存器，而更高版本的驱动程序试图 I/O 的可能性。

 

 




