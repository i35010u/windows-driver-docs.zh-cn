---
title: 用户拔出设备
description: 用户拔出设备
ms.assetid: 85e69401-0128-4641-aa0f-fd7c4f22f395
keywords:
- PnP WDK KMDF，拔出设备
- 即插即用 WDK KMDF，拔出设备
- 有序的设备删除 WDK KMDF
- 拔出设备 WDK KMDF
- 意外的设备删除 WDK KMDF
- 意外的设备删除 WDK KMDF
- 删除设备 WDK KMDF
- 弹出设备 WDK KMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e03da077748558cedb46da32145f2e56847aaf46
ms.sourcegitcommit: b316c97bafade8b76d5d3c30d48496915709a9df
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/13/2020
ms.locfileid: "79242954"
---
# <a name="a-user-unplugs-a-device"></a>用户拔出设备


当系统运行时，用户可以通过以下两种方式之一删除设备：按*序删除*，这意味着用户通知系统将删除设备（例如，使用拔出或弹出硬件程序）;或者是*意外删除*，这意味着用户断开了设备，而无需通知系统。 如果总线支持意外删除（例如 USB），则设备的驱动程序必须能够处理设备突然消失。

### <a href="" id="orderly-removal"></a>有序删除

用户使用系统的拔出或弹出硬件程序请求删除，方法是使用设备管理器禁用设备，或通过推送[ejectable](supporting-ejectable-devices.md)设备的弹出按钮。 框架允许删除或禁用设备，除非驱动程序具有：

-   在设备上打开了名为[**WdfDeviceSetSpecialFileSupport**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicesetspecialfilesupport)的特殊文件。

-   称为[**WdfDeviceSetStaticStopRemove**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicesetstaticstopremove)。

-   提供了一个[*EvtDeviceQueryRemove*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_query_remove)回调函数，并且回调函数已拒绝删除。

对于支持设备的每个函数和筛选器驱动程序，框架按顺序执行以下操作，一次一个驱动程序，从驱动程序堆栈最高的驱动程序开始：

1.  如果驱动程序使用的是自管理 i/o，则框架将调用驱动程序的[*EvtDeviceSelfManagedIoSuspend*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_self_managed_io_suspend)回调函数。

2.  框架将停止驱动程序的所有电源管理 i/o 队列。

3.  如果硬件和驱动程序支持 DMA，框架会为创建的每个 DMA 通道调用驱动程序的[*EvtDmaEnablerSelfManagedIoStop*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdmaenabler/nc-wdfdmaenabler-evt_wdf_dma_enabler_selfmanaged_io_stop)、 [*EvtDmaEnablerFlush*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdmaenabler/nc-wdfdmaenabler-evt_wdf_dma_enabler_flush)和[*EvtDmaEnablerDisable*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdmaenabler/nc-wdfdmaenabler-evt_wdf_dma_enabler_disable)回调函数（如果存在）。

4.  框架调用驱动程序的[*EvtDeviceD0ExitPreInterruptsDisabled*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_d0_exit_pre_interrupts_disabled)回调函数（如果存在），然后为每个中断调用驱动程序的[*EvtInterruptDisable*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_disable)回调函数（如果存在），以便驱动程序可以禁用设备中断。

5.  框架调用驱动程序的[*EvtDeviceD0Exit*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_d0_exit)回调函数（如果存在）。

6.  框架调用驱动程序的[*EvtDeviceReleaseHardware*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_release_hardware)回调函数（如果存在），并向其传递 PnP 管理器已分配给设备的硬件资源列表。

7.  如果驱动程序使用的是自管理 i/o，则框架将调用驱动程序的[*EvtDeviceSelfManagedIoFlush*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_self_managed_io_flush)回调函数。

8.  如果驱动程序使用的是自管理 i/o，则框架将调用驱动程序的[*EvtDeviceSelfManagedIoCleanup*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_self_managed_io_cleanup)回调函数。

总线驱动程序是堆栈中最后一个调用的驱动程序。 当框架调用总线驱动程序的[*EvtDeviceD0Exit*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_d0_exit)回调函数时，回调函数会将设备（总线的子设备）的电源状态设置为 D3。 总线驱动程序可以通过调用[**WdfDeviceInitSetReleaseHardwareOrderOnFailure**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitsetreleasehardwareorderonfailure)来控制框架调用其[*EvtDeviceReleaseHardware*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_release_hardware)回调函数的时间。

### <a href="" id="surprise-removal"></a>意外删除

用户意外断开设备。 设备总线的总线驱动程序发现设备丢失并调用[**WdfChildListUpdateChildDescriptionAsMissing**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfchildlist/nf-wdfchildlist-wdfchildlistupdatechilddescriptionasmissing)。

对于支持设备的每个函数和筛选器驱动程序，框架按顺序执行以下操作，一次一个驱动程序，从驱动程序堆栈最高的驱动程序开始：

1.  框架调用驱动程序的[*EvtDeviceSurpriseRemoval*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_surprise_removal)回调函数（如果存在）。

2.  如果设备在被拔下时处于正常工作（D0）状态，则该框架将停止所有驱动程序的电源管理 i/o 队列。

3.  如果设备在被拔下时处于正常工作（D0）状态，并且驱动程序使用的是自我托管 i/o，则框架将调用驱动程序的[*EvtDeviceSelfManagedIoSuspend*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_self_managed_io_suspend)回调函数。

4.  如果硬件和驱动程序支持 DMA，框架会为创建的每个 DMA 通道调用驱动程序的[*EvtDmaEnablerSelfManagedIoStop*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdmaenabler/nc-wdfdmaenabler-evt_wdf_dma_enabler_selfmanaged_io_stop)、 [*EvtDmaEnablerFlush*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdmaenabler/nc-wdfdmaenabler-evt_wdf_dma_enabler_flush)和[*EvtDmaEnablerDisable*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdmaenabler/nc-wdfdmaenabler-evt_wdf_dma_enabler_disable)回调函数（如果存在）。

5.  框架调用驱动程序的[*EvtDeviceD0ExitPreInterruptsDisabled*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_d0_exit_pre_interrupts_disabled)和[*EvtInterruptDisable*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_disable)回调函数（如果存在），以便驱动程序可以禁用设备中断。

6.  框架调用驱动程序的[*EvtDeviceD0Exit*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_d0_exit)回调函数（如果存在）。

7.  框架调用驱动程序的[*EvtDeviceReleaseHardware*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_release_hardware)回调函数（如果存在），传递 PnP 管理器已分配给设备的硬件资源的列表。

8.  如果驱动程序使用的是自管理 i/o，则框架将调用驱动程序的[*EvtDeviceSelfManagedIoFlush*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_self_managed_io_flush)回调函数。

9.  如果驱动程序使用的是自管理 i/o，则框架将调用驱动程序的[*EvtDeviceSelfManagedIoCleanup*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_self_managed_io_cleanup)回调函数。

请注意，在任何时候，都可能会意外删除设备。 因此，该框架可能会调用驱动程序的[*EvtDeviceSurpriseRemoval*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_surprise_removal)回调函数，而不是在前面的步骤中所示的时间。 例如，如果用户在[进入低功耗状态](a-device-enters-a-low-power-state.md)时意外断开了设备，则该框架可能会在调用[*EvtDeviceReleaseHardware*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_release_hardware)回调函数后调用[*EvtDeviceSurpriseRemoval*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_surprise_removal)回调函数。 不能以特定顺序调用[*EvtDeviceSurpriseRemoval*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_surprise_removal)回调函数的方式，而不是假定它和其他回调函数。

此外，此框架不会将设备的[*EvtDeviceSurpriseRemoval*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_surprise_removal)回调函数与前面步骤中列出的针对该设备的任何回调函数同步。 因此，当前面列出的另一个回调函数正在运行时， [*EvtDeviceSurpriseRemoval*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_surprise_removal)回调函数可能运行。

 

 





