---
title: 使用自我管理的 I/O
description: 使用自我管理的 I/O
ms.assetid: 539b3618-44bb-41fd-a9f2-ed6a377c94e2
keywords:
- PnP WDK KMDF，自托管 I/O
- 即插即用 WDK KMDF，自托管 I/O
- 电源管理 WDK KMDF 自托管 I/O
- 自托管的 I/O WDK KMDF
- I/O 自助管理 WDK KMDF
- 感到惊讶设备删除 WDK KMDF
- 意外的设备删除 WDK KMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bed2027391c02350452736ef6d5466a4fa3f6c61
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63391839"
---
# <a name="using-self-managed-io"></a>使用自我管理的 I/O


大多数基于框架的驱动程序充分利用它们支持的设备的框架的 PnP 和电源管理功能。 换而言之，大多数基于框架的驱动程序让框架管理设备的即插即用和电源状态，通过执行以下所有操作：

-   提供[ *EvtDeviceD0Entry* ](https://msdn.microsoft.com/library/windows/hardware/ff540848)并[ *EvtDeviceD0Exit* ](https://msdn.microsoft.com/library/windows/hardware/ff540855)回调函数。

-   提供[ *EvtDevicePrepareHardware* ](https://msdn.microsoft.com/library/windows/hardware/ff540880)并[ *EvtDeviceReleaseHardware* ](https://msdn.microsoft.com/library/windows/hardware/ff540890)回调函数。

-   使用电源管理队列的 I/O 请求的要求设备在其工作状态，并使用不是所有其他请求的电源管理的队列。

但是，一些基于框架的驱动程序将需要更清楚地知道他们的设备，在以下情况下包括驱动程序的状态：

-   由驱动程序框架 I/O 队列中接收的 I/O 请求的一组不确定，驱动程序执行的操作。

-   驱动程序与较旧的、 非 framework 驱动程序进行通信，直接与 WDM 接口处理。

-   驱动程序接收的 I/O 请求无法拆分为两个组： 那些要求在其工作状态中并且没有设备。

大多数驱动程序不在上述情况下，之一，但如果您的驱动程序，它可能需要更直接控制设备的即插即用和电源管理操作。 可以使用此类驱动程序*自行管理 I/O*。 使用自托管的 I/O 意味着只要有一个如果接通电源或拔出，其设备，只要该设备是暂时停止 （通过一组回调函数） 的方式通知驱动程序。

请注意，驱动程序可以使用自我管理的 I/O 仍使用框架的 I/O 队列，为电源管理队列。 例如，驱动程序可以使用框架的 I/O 队列，不电源管理，使用一组自托管 I/O 回调函数。

若要使用自托管的 I/O，该驱动程序注册一组额外的事件回调函数时，它调用[ **WdfDeviceInitSetPnpPowerEventCallbacks**](https://msdn.microsoft.com/library/windows/hardware/ff546135)。 这些事件回调函数包括：

-   [*EvtDeviceSelfManagedIoInit*](https://msdn.microsoft.com/library/windows/hardware/ff540902)，它初始化并启动设备的 I/O 操作。

-   [*EvtDeviceSelfManagedIoSuspend*](https://msdn.microsoft.com/library/windows/hardware/ff540907)的挂起 I/O 操作。

-   [*EvtDeviceSelfManagedIoRestart*](https://msdn.microsoft.com/library/windows/hardware/ff540905)，这将重新启动设备的 I/O 操作后已挂起。

-   [*EvtDeviceSelfManagedIoFlush*](https://msdn.microsoft.com/library/windows/hardware/ff540901)，这将删除未服务输入/输出请求。

-   [*EvtDeviceSelfManagedIoCleanup*](https://msdn.microsoft.com/library/windows/hardware/ff540898)，其中释放资源，所分配的[ *EvtDeviceSelfManagedIoInit*](https://msdn.microsoft.com/library/windows/hardware/ff540902)。

你的设备为第一次输入其工作 (D0) 状态，框架将调用您的驱动程序[ *EvtDeviceSelfManagedIoInit* ](https://msdn.microsoft.com/library/windows/hardware/ff540902)回调函数。 每次用户将设备插入系统和每次重新启动系统时，将发生这种情况。

有三种情况下，驱动程序必须在其中停止设备的 I/O 操作： 即将进入低功耗状态的设备，它将被删除，或已意外删除。 以下列表检查每个这种情况下，在详细信息：

-   设备将进入低功耗状态，并最终又返回到其工作状态。

    当你的设备将进入低功耗状态 (因为你的设备处于空闲状态，整个系统即将进入低功耗状态，或者 PnP 管理器是[重新发布系统硬件资源](handling-requests-to-stop-a-device.md#redistributing-resources))，框架将调用你驱动程序的[ *EvtDeviceSelfManagedIoSuspend* ](https://msdn.microsoft.com/library/windows/hardware/ff540907)回调函数。 设备重新输入其工作状态后，框架将调用您的驱动程序[ *EvtDeviceSelfManagedIoRestart* ](https://msdn.microsoft.com/library/windows/hardware/ff540905)回调函数。

-   设备已被移除。

    若要处理[用户请求设备删除](handling-requests-to-stop-a-device.md#a-user-removes-or-disables-a-device)，框架将调用您的驱动程序[ *EvtDeviceSelfManagedIoSuspend* ](https://msdn.microsoft.com/library/windows/hardware/ff540907)之前停止设备的回调函数。 停止后该设备，框架将调用您的驱动程序[ *EvtDeviceSelfManagedIoFlush* ](https://msdn.microsoft.com/library/windows/hardware/ff540901)回调函数。 删除设备后，框架将调用[ *EvtDeviceSelfManagedIoCleanup* ](https://msdn.microsoft.com/library/windows/hardware/ff540898)回调函数。

-   已意外删除设备 （感到惊讶删除）。

    如果设备的总线驱动程序确定设备不再存在，或者在堆栈中的另一个驱动程序确定设备未响应，发现了问题的驱动程序可以通知即插即用管理器。 然后，PnP 管理器会通知驱动程序的其余部分设备将消失。 基于框架的驱动程序，请框架接收即插即用管理器的消息并调用您的驱动程序[ *EvtDeviceSelfManagedIoSuspend*](https://msdn.microsoft.com/library/windows/hardware/ff540907)， [ *EvtDeviceSelfManagedIoFlush*](https://msdn.microsoft.com/library/windows/hardware/ff540901)，并[ *EvtDeviceSelfManagedIoCleanup* ](https://msdn.microsoft.com/library/windows/hardware/ff540898)回调函数。

    (您的驱动程序还可以注册[ *EvtDeviceSurpriseRemoval* ](https://msdn.microsoft.com/library/windows/hardware/ff540913)回调函数。 如果设备已在其工作 (D0) 状态中删除时，框架将调用*EvtDeviceSurpriseRemoval*自托管的 I/O 回调函数在调用之前。 如果设备处于低功耗状态删除时， *EvtDeviceSurpriseRemoval*后，会调用[ *EvtDeviceSelfManagedIoSuspend*](https://msdn.microsoft.com/library/windows/hardware/ff540907))

有关在其中框架调用驱动程序的事件回调函数的顺序的详细信息，请参阅[PnP 和电源管理方案](pnp-and-power-management-scenarios.md)。

尽管很少会有必要，该框架允许驱动程序具有更多控制设备的即插即用和电源状态，通过访问[状态机 framework 中的](state-machines-in-the-framework.md)。

 

 





