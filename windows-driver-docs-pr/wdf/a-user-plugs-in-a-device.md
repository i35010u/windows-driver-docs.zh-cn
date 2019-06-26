---
title: 用户插入设备
description: 用户插入设备
ms.assetid: cc047c05-f3aa-4423-98fc-cafd7777e104
keywords:
- 即插即用 WDK KMDF，插入的设备
- 插 WDK KMDF，插入的设备
- 插入设备 WDK KMDF
- 添加设备 WDK KMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: db4fb925401ceb5f776ea37d5da2b8d749b7ac0d
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385328"
---
# <a name="a-user-plugs-in-a-device"></a>用户插入设备


在以下方案中，设备节点包含 KMDF 总线驱动程序和一个或多个 KMDF 函数或筛选器驱动程序支持的即插即用设备。

当用户将设备插入到总线，系统运行时，设备的总线驱动程序和框架将执行以下任务：

-   设备的总线驱动程序检测到该设备并调用[ **WdfChildListAddOrUpdateChildDescriptionAsPresent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfchildlist/nf-wdfchildlist-wdfchildlistaddorupdatechilddescriptionaspresent)。 （此过程称为"动态枚举"。）

-   框架将调用总线驱动程序[ *EvtChildListCreateDevice* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfchildlist/nc-wdfchildlist-evt_wdf_child_list_create_device)回调函数，因此总线驱动程序可以调用[ **WdfDeviceCreate** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdevicecreate)若要创建物理设备 (PDO) 是 framework 的设备对象。

-   框架将调用总线驱动程序[ *EvtDeviceResourcesQuery* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfpdo/nc-wdfpdo-evt_wdf_device_resources_query)并[ *EvtDeviceResourceRequirementsQuery* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfpdo/nc-wdfpdo-evt_wdf_device_resource_requirements_query)回调若要确定设备需要的系统硬件资源的函数。

KMDF 总线驱动程序的启动顺序的详细信息，请参阅[总线驱动程序的增益道具序列](power-up-sequence-for-a-bus-driver.md)。

接下来，即插即用管理器确定 （函数驱动程序和筛选器驱动程序） 的其他驱动程序设备要求。 如果尚未加载这些驱动程序，即插即用管理器来加载它们并调用其[ **DriverEntry** ](https://docs.microsoft.com/windows-hardware/drivers/wdf/driverentry-for-kmdf-drivers)例程。 对于每个函数或筛选器驱动程序中，执行下列操作：

-   框架将调用每个附加驱动程序[ *EvtDriverDeviceAdd* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)回调函数，以便该驱动程序可以调用[ **WdfDeviceCreate** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdevicecreate)来创建 framework 设备对象表示的设备驱动程序。 功能的驱动程序创建功能的设备对象 (FDO) 和筛选器驱动程序创建 （筛选器执行操作） 的筛选器设备对象。

-   框架将调用每个函数和筛选器驱动程序的[ *EvtDeviceFilterRemoveResourceRequirements* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdffdo/nc-wdffdo-evt_wdf_device_filter_resource_requirements)回调函数，然后每个驱动程序的[ *EvtDeviceFilterAddResourceRequirements* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdffdo/nc-wdffdo-evt_wdf_device_filter_resource_requirements)回调函数。 立即启动设备之前，框架将调用[ *EvtDeviceRemoveAddedResources* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdffdo/nc-wdffdo-evt_wdf_device_remove_added_resources)回调函数。 这三个回调函数允许的筛选器和函数的驱动程序可以修改设备要求之前的即插即用的管理器将资源分配给设备, 的硬件资源的列表。 有关详细信息，请参阅[基于框架的驱动程序的硬件资源](hardware-resources-for-kmdf-drivers.md)

-   框架将确保设备已达到其工作 (D0) 电源状态。

-   对于每个函数和筛选器驱动程序支持设备，该框架执行以下操作，在序列中，使用驱动程序的最低驱动程序堆栈中启动一个时，驱动程序：
    1.  框架将调用的驱动程序[ *EvtDevicePrepareHardware* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_prepare_hardware)回调函数 （如果存在），并将传递的即插即用的管理员分配给设备的硬件资源的列表。
    2.  框架将调用的驱动程序[ *EvtDeviceD0Entry* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_d0_entry)回调函数 （如果存在）。
    3.  框架将调用的驱动程序[ *EvtInterruptEnable* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_enable)回调函数 （如果存在） 为每个中断，然后它调用的驱动程序[ *EvtDeviceD0EntryPostInterruptsEnabled* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_d0_entry_post_interrupts_enabled)回调函数 （如果存在），以便该驱动程序可以启用设备中断。
    4.  如果硬件和驱动程序支持 DMA，框架将调用的驱动程序[ *EvtDmaEnablerFill*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdmaenabler/nc-wdfdmaenabler-evt_wdf_dma_enabler_fill)， [ *EvtDmaEnablerEnable*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdmaenabler/nc-wdfdmaenabler-evt_wdf_dma_enabler_enable)，和[ *EvtDmaEnablerSelfManagedIoStart* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdmaenabler/nc-wdfdmaenabler-evt_wdf_dma_enabler_selfmanaged_io_start)回调函数 （如果存在） 用于创建每个 DMA 通道。
    5.  框架将调用的驱动程序[ *EvtChildListScanForChildren* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfchildlist/nc-wdfchildlist-evt_wdf_child_list_scan_for_children)回调函数 （如果存在）。
    6.  在框架开始的所有设备的电源管理的 I/O 队列。
    7.  如果该驱动程序使用的自托管的 I/O，框架将调用的驱动程序[ *EvtDeviceSelfManagedIoInit* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_self_managed_io_init)回调函数。

强化序列 KMDF 函数或筛选器驱动程序，有关详细信息[函数或筛选器驱动程序的启动顺序](power-up-sequence-for-a-function-or-filter-driver.md)。

 

 





