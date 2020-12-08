---
title: 使用自我管理的 I/O
description: 使用自我管理的 I/O
keywords:
- PnP WDK KMDF，自我托管 i/o
- 即插即用 WDK KMDF，自我托管 i/o
- 电源管理 WDK KMDF，自我托管 i/o
- 自托管 i/o WDK KMDF
- I/o 自助管理 WDK KMDF
- 意外的设备删除 WDK KMDF
- 意外的设备删除 WDK KMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c377cb8e9ceb4bbc12f58ee3e480b16812b7d004
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96802109"
---
# <a name="using-self-managed-io"></a>使用自我管理的 I/O


大多数基于框架的驱动程序都利用了框架为其支持的设备提供的 PnP 和电源管理功能。 换句话说，大多数基于框架的驱动程序允许框架通过执行以下所有操作管理设备的 PnP 和电源状态：

-   提供 [*EvtDeviceD0Entry*](/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_d0_entry) 和 [*EvtDeviceD0Exit*](/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_d0_exit) 回调函数。

-   提供 [*EvtDevicePrepareHardware*](/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_prepare_hardware) 和 [*EvtDeviceReleaseHardware*](/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_release_hardware) 回调函数。

-   对 i/o 请求使用电源管理的队列，这些请求要求设备处于工作状态，并使用对所有其他请求不具有电源管理功能的队列。

然而，一些基于框架的驱动程序将需要更好地了解其设备的状态，包括在以下情况下的驱动程序：

-   驱动程序执行的操作不由驱动程序从框架 i/o 队列接收的一组 i/o 请求决定。

-   驱动程序与较旧的非框架驱动程序通信并直接使用 WDM 接口进行处理。

-   驱动程序接收到的 i/o 请求不能分为两组：那些要求设备处于工作状态的组和不是的请求。

大多数驱动程序并不是上述一种情况，但如果您的驱动程序是，可能需要更直接控制设备的 PnP 和电源管理操作。 此类驱动程序可以使用 *自管理 i/o*。 使用自托管 i/o 意味着将通过一组回调函数通知 () 每次使用一组回调函数时，无论设备是否已插入或拔下，以及设备是否暂时停止。

请注意，驱动程序可以使用自托管 i/o，并仍使用框架的 i/o 队列，如电源管理的队列。 例如，驱动程序可以使用一组自行管理的 i/o 回调函数，而不是对其进行电源管理。

若要使用自托管 i/o，驱动程序会在调用 [**WdfDeviceInitSetPnpPowerEventCallbacks**](/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitsetpnppowereventcallbacks)时注册一组额外的事件回调函数。 这些事件回调函数为：

-   [*EvtDeviceSelfManagedIoInit*](/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_self_managed_io_init)，用于初始化和启动设备的 i/o 操作。

-   [*EvtDeviceSelfManagedIoSuspend*](/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_self_managed_io_suspend)，它将挂起 i/o 操作。

-   [*EvtDeviceSelfManagedIoRestart*](/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_self_managed_io_restart)，它将在挂起后重新启动设备的 i/o 操作。

-   [*EvtDeviceSelfManagedIoFlush*](/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_self_managed_io_flush)，它删除通往 i/o 请求。

-   [*EvtDeviceSelfManagedIoCleanup*](/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_self_managed_io_cleanup)，它释放由 [*EvtDeviceSelfManagedIoInit*](/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_self_managed_io_init)分配的资源。

当设备首次进入工作 (D0) 状态时，框架会调用驱动程序的 [*EvtDeviceSelfManagedIoInit*](/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_self_managed_io_init) 回调函数。 每次用户将设备插入系统并每次重新启动系统时，都会发生这种情况。

在以下三种情况下，驱动程序必须停止设备的 i/o 操作：设备即将进入低功耗状态、即将被删除或已被意外删除。 以下列表详细介绍了上述每种情况：

-   设备即将进入低功耗状态，最终会恢复到其工作状态。

    如果设备即将进入低功耗状态 (因为设备处于空闲状态，则整个系统进入低功耗状态，或者 PnP 管理器正在重新 [分发系统硬件资源](handling-requests-to-stop-a-device.md#redistributing-resources)) ，框架将调用驱动程序的 [*EvtDeviceSelfManagedIoSuspend*](/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_self_managed_io_suspend) 回调函数。 设备重新输入其工作状态后，框架将调用驱动程序的 [*EvtDeviceSelfManagedIoRestart*](/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_self_managed_io_restart) 回调函数。

-   将删除设备。

    为了处理 [用户请求的设备删除](handling-requests-to-stop-a-device.md#a-user-removes-or-disables-a-device)，框架会在停止设备之前调用驱动程序的 [*EvtDeviceSelfManagedIoSuspend*](/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_self_managed_io_suspend) 回调函数。 停止设备后，框架将调用驱动程序的 [*EvtDeviceSelfManagedIoFlush*](/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_self_managed_io_flush) 回调函数。 删除设备后，框架将调用 [*EvtDeviceSelfManagedIoCleanup*](/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_self_managed_io_cleanup) 回调函数。

-   设备已意外删除， (意外删除) 。

    如果设备总线的驱动程序确定设备不再存在，或者堆栈中的另一个驱动程序确定设备未响应，则发现此问题的驱动程序将通知 PnP 管理器。 然后，PnP 管理器通知其他驱动程序设备丢失。 对于基于框架的驱动程序，该框架会接收 PnP 管理器的消息，并调用驱动程序的 [*EvtDeviceSelfManagedIoSuspend*](/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_self_managed_io_suspend)、 [*EvtDeviceSelfManagedIoFlush*](/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_self_managed_io_flush)和 [*EvtDeviceSelfManagedIoCleanup*](/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_self_managed_io_cleanup) 回调函数。

     (驱动程序还可以注册一个 [*EvtDeviceSurpriseRemoval*](/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_surprise_removal) 回调函数。 如果设备处于工作状态 (D0) 在删除时，该框架会在调用自行托管 i/o 回调函数之前调用 *EvtDeviceSurpriseRemoval* 。 如果设备在删除时处于低功耗状态，则在 [*EvtDeviceSelfManagedIoSuspend*](/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_self_managed_io_suspend)之后调用 *EvtDeviceSurpriseRemoval*) 

有关框架调用驱动程序的事件回调函数的顺序的详细信息，请参阅 [PnP 和电源管理方案](pnp-and-power-management-scenarios.md)。

尽管很少需要，但通过访问 [框架中的状态计算机](state-machines-in-the-framework.md)，驱动程序可以更好地控制设备的 PnP 和电源状态。

 

