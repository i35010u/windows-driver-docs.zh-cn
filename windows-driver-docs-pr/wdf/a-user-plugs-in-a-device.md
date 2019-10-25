---
title: 用户插入设备
description: 用户插入设备
ms.assetid: cc047c05-f3aa-4423-98fc-cafd7777e104
keywords:
- PnP WDK KMDF，插入设备
- 即插即用 WDK KMDF，插入设备
- 插入设备 WDK KMDF
- 添加设备 WDK KMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f3c006e5a8699a8573ca468b9d98d7457a69bd78
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841675"
---
# <a name="a-user-plugs-in-a-device"></a>用户插入设备


在以下方案中，设备节点包含 KMDF 总线驱动程序和一个或多个支持 PnP 设备的 KMDF 函数或筛选器驱动程序。

当用户在系统运行时将设备插入总线时，设备的总线驱动程序和框架将执行以下任务：

-   设备的总线驱动程序检测设备并调用[**WdfChildListAddOrUpdateChildDescriptionAsPresent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfchildlist/nf-wdfchildlist-wdfchildlistaddorupdatechilddescriptionaspresent)。 （此过程称为 "动态枚举"。）

-   该框架会调用总线驱动程序的[*EvtChildListCreateDevice*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfchildlist/nc-wdfchildlist-evt_wdf_child_list_create_device)回调函数，以便总线驱动程序可以调用[**WdfDeviceCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicecreate)为物理设备（PDO）创建框架设备对象。

-   框架调用总线驱动程序的[*EvtDeviceResourcesQuery*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfpdo/nc-wdfpdo-evt_wdf_device_resources_query)和[*EvtDeviceResourceRequirementsQuery*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfpdo/nc-wdfpdo-evt_wdf_device_resource_requirements_query)回调函数来确定设备所需的系统硬件资源。

有关 KMDF 总线驱动程序的启动顺序的详细信息，请参阅[总线驱动程序](power-up-sequence-for-a-bus-driver.md)的启动顺序。

接下来，PnP 管理器决定设备需要的其他驱动程序（函数驱动程序和筛选器驱动程序）。 如果尚未加载这些驱动程序，PnP 管理器会加载这些驱动程序并调用其[**DriverEntry**](https://docs.microsoft.com/windows-hardware/drivers/wdf/driverentry-for-kmdf-drivers)例程。 对于每个函数或筛选器驱动程序，将执行以下操作：

-   框架将调用每个附加驱动程序的[*EvtDriverDeviceAdd*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)回调函数，以便驱动程序可以调用[**WdfDeviceCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicecreate)来创建一个框架设备对象，该对象表示驱动程序的设备。 函数驱动程序创建功能设备对象（FDO），筛选器驱动程序创建筛选器设备对象（筛选器）。

-   框架调用每个函数和筛选器驱动程序的[*EvtDeviceFilterRemoveResourceRequirements*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdffdo/nc-wdffdo-evt_wdf_device_filter_resource_requirements)回调函数，然后调用每个驱动程序的[*EvtDeviceFilterAddResourceRequirements*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdffdo/nc-wdffdo-evt_wdf_device_filter_resource_requirements)回调函数。 设备开始之前，框架将调用[*EvtDeviceRemoveAddedResources*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdffdo/nc-wdffdo-evt_wdf_device_remove_added_resources)回调函数。 在 PnP 管理器将资源分配给设备之前，这三个回调函数允许筛选器和函数驱动程序修改设备所需的硬件资源的列表。 有关详细信息，请参阅[基于框架的驱动程序的硬件资源](hardware-resources-for-kmdf-drivers.md)

-   框架可确保设备已达到其工作（D0）电源状态。

-   对于支持设备的每个函数和筛选器驱动程序，框架按顺序执行以下操作，一次一个驱动程序，从驱动程序堆栈中的最低驱动程序开始：
    1.  框架调用驱动程序的[*EvtDevicePrepareHardware*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_prepare_hardware)回调函数（如果存在），并传递 PnP 管理器已分配给设备的硬件资源列表。
    2.  框架调用驱动程序的[*EvtDeviceD0Entry*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_d0_entry)回调函数（如果存在）。
    3.  框架为每个中断调用驱动程序的[*EvtInterruptEnable*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_enable)回调函数（如果存在），然后调用驱动程序的[*EvtDeviceD0EntryPostInterruptsEnabled*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_d0_entry_post_interrupts_enabled)回调函数（如果存在），以便驱动程序可以启用设备中断。
    4.  如果硬件和驱动程序支持 DMA，框架会为创建的每个 DMA 通道调用驱动程序的[*EvtDmaEnablerFill*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdmaenabler/nc-wdfdmaenabler-evt_wdf_dma_enabler_fill)、 [*EvtDmaEnablerEnable*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdmaenabler/nc-wdfdmaenabler-evt_wdf_dma_enabler_enable)和[*EvtDmaEnablerSelfManagedIoStart*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdmaenabler/nc-wdfdmaenabler-evt_wdf_dma_enabler_selfmanaged_io_start)回调函数（如果存在）。
    5.  框架调用驱动程序的[*EvtChildListScanForChildren*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfchildlist/nc-wdfchildlist-evt_wdf_child_list_scan_for_children)回调函数（如果存在）。
    6.  框架启动所有设备的电源托管 i/o 队列。
    7.  如果驱动程序使用的是自管理 i/o，则框架将调用驱动程序的[*EvtDeviceSelfManagedIoInit*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_self_managed_io_init)回调函数。

有关 KMDF 函数或筛选器驱动程序的启动顺序的详细信息，请查看[函数或筛选器驱动程序](power-up-sequence-for-a-function-or-filter-driver.md)的启动顺序。

 

 





