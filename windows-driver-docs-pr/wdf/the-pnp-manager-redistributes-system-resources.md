---
title: PnP 管理器重新分发系统资源
description: PnP 管理器重新分发系统资源
ms.assetid: fc88ae0a-5b78-4292-a101-29d2fc383555
keywords:
- PnP WDK KMDF，重新分发资源
- 即插即用 WDK KMDF，重新分发资源
- 资源重新分发 WDK KMDF
- 重新分发资源 WDK KMDF
- 关机顺序 WDK KMDF
- 开机序列 WDK KMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 952270ec663ff81831b1920305c61094b9197e62
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89191393"
---
# <a name="the-pnp-manager-redistributes-system-resources"></a>PnP 管理器重新分发系统资源


如果用户将设备添加到系统，并且设备需要 PnP 管理器已分配给另一个设备的系统资源，则 PnP 管理器会尝试重新分配资源。

在此过程中，PnP 管理器会停止设备，并使其进入工作 (D0) 状态。 然后，它将新的资源列表传递到设备，以便它们可以使用新资源重新启动。

重新分发资源时，如果某个设备的驱动程序具有以下各项，PnP 管理器将不会更改设备的资源分配：

-   在设备上打开了名为 [**WdfDeviceSetSpecialFileSupport**](/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicesetspecialfilesupport) 的特殊文件。

-   称为 [**WdfDeviceSetStaticStopRemove**](/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicesetstaticstopremove)。

-   提供了一个 [*EvtDeviceQueryStop*](/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_query_stop) 回调函数，并且回调函数否决了重新分配。

### <a name="power-down-sequence"></a>关机顺序

对于支持正在停止的设备的每个函数和筛选器驱动程序，框架按顺序执行以下操作，一次一个驱动程序，从驱动程序堆栈最高的驱动程序开始：

1.  如果驱动程序使用的是自管理 i/o，则框架将调用驱动程序的 [*EvtDeviceSelfManagedIoSuspend*](/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_self_managed_io_suspend) 回调函数。

2.  框架停止所有设备的电源托管 i/o 队列。

3.  如果硬件和驱动程序支持 DMA，框架将为创建的每个 DMA 通道调用驱动程序的 [*EvtDmaEnablerSelfManagedIoStop*](/windows-hardware/drivers/ddi/wdfdmaenabler/nc-wdfdmaenabler-evt_wdf_dma_enabler_selfmanaged_io_stop)、 [*EvtDmaEnablerFlush*](/windows-hardware/drivers/ddi/wdfdmaenabler/nc-wdfdmaenabler-evt_wdf_dma_enabler_flush)和 [*EvtDmaEnablerDisable*](/windows-hardware/drivers/ddi/wdfdmaenabler/nc-wdfdmaenabler-evt_wdf_dma_enabler_disable) 回调函数。

4.  如果 (存在驱动程序的 [*EvtDeviceD0ExitPreInterruptsDisabled*](/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_d0_exit_pre_interrupts_disabled) 和 [*EvtInterruptDisable*](/windows-hardware/drivers/ddi/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_disable) 回调函数) 以便驱动程序可以禁用设备中断，则调用该函数。

5.  如果) 存在驱动程序 (，则框架将调用该驱动程序的 [*EvtDeviceD0Exit*](/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_d0_exit) 回调函数。

6.  如果) 该驱动程序已分配给该设备的硬件资源列表，则框架将调用该驱动程序的 [*EvtDeviceReleaseHardware*](/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_release_hardware) 回调函数 (。

总线驱动程序是堆栈中最底层的驱动程序，最后调用。 当框架调用总线驱动程序的[*EvtDeviceD0Exit*](/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_d0_exit)回调函数时，它会将句柄传递给表示设备 PDO 的框架设备对象和**WdfPowerDeviceD3Final**的*TargetState*值。 总线驱动程序可以通过调用[**WdfDeviceInitSetReleaseHardwareOrderOnFailure**](/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitsetreleasehardwareorderonfailure)来控制框架调用其[*EvtDeviceReleaseHardware*](/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_release_hardware)回调函数的时间。

### <a name="power-up-sequence"></a>通电顺序

第一个名为的驱动程序是总线驱动程序。 当框架调用总线驱动程序的 [*EvtDeviceD0Entry*](/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_d0_entry) 回调函数时，回调函数会将该设备 (总线的子设备恢复) 其工作 (D0) 状态。

对于支持设备的每个函数和筛选器驱动程序，框架按顺序执行以下操作，一次一个驱动程序，从驱动程序堆栈中的最低驱动程序开始：

1.  如果) 存在驱动程序的 [*EvtDevicePrepareHardware*](/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_prepare_hardware) 回叫函数，则框架将调用该驱动程序的回调 (函数，同时传递 PnP 管理器已分配给该设备的硬件资源的列表。

2.  如果) 存在驱动程序 (，则框架将调用该驱动程序的 [*EvtDeviceD0Entry*](/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_d0_entry) 回调函数。

3.  框架将调用驱动程序的 [*EvtInterruptEnable*](/windows-hardware/drivers/ddi/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_enable) 和 [*EvtDeviceD0EntryPostInterruptsEnabled*](/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_d0_entry_post_interrupts_enabled) 回调函数 (如果它们存在) 以便驱动程序能够启用设备中断。

4.  如果硬件和驱动程序支持 DMA，框架将为创建的每个 DMA 通道调用驱动程序的 [*EvtDmaEnablerFill*](/windows-hardware/drivers/ddi/wdfdmaenabler/nc-wdfdmaenabler-evt_wdf_dma_enabler_fill)、 [*EvtDmaEnablerEnable*](/windows-hardware/drivers/ddi/wdfdmaenabler/nc-wdfdmaenabler-evt_wdf_dma_enabler_enable)和 [*EvtDmaEnablerSelfManagedIoStart*](/windows-hardware/drivers/ddi/wdfdmaenabler/nc-wdfdmaenabler-evt_wdf_dma_enabler_selfmanaged_io_start) 回调函数。

5.  如果) 存在驱动程序 (，则框架将调用该驱动程序的 [*EvtChildListScanForChildren*](/windows-hardware/drivers/ddi/wdfchildlist/nc-wdfchildlist-evt_wdf_child_list_scan_for_children) 回调函数。

6.  框架将重新启动所有设备的电源托管 i/o 队列。

7.  如果驱动程序使用的是自管理 i/o，则框架将调用驱动程序的 [*EvtDeviceSelfManagedIoRestart*](/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_self_managed_io_restart) 回调函数。

 

