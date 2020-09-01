---
title: 硬件资源简介
description: 硬件资源简介
ms.assetid: 34350031-daae-4213-b157-086a7a55e05b
keywords:
- 启动配置 WDK KMDF
- 逻辑配置 WDK KMDF
- 硬件资源 WDK KMDF，关于硬件资源
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9079b5025710e78dae8b1921fe55511d362f88a2
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89184307"
---
# <a name="introduction-to-hardware-resources"></a>硬件资源简介


用户插入 PnP 设备后， [枚举设备](enumerating-the-devices-on-a-bus.md) 的驱动程序通常会创建一个或多个 [逻辑配置](../kernel/hardware-resources.md#ddk-logical-configurations-kg)，这些配置是设备可以使用的硬件资源的组合。 这些配置包括：

-   一种 *启动配置* ，它列出了系统启动时设备所需的硬件资源。  (PnP 设备，则 BIOS 将提供此信息。 ) 

-   设备可以操作的其他配置。 驱动程序会在 [资源要求列表](../kernel/hardware-resources.md)中对这些附加配置进行分组。 PnP 管理器最终将从该列表中选择要分配给设备的资源。

驱动程序创建逻辑配置后，会将其发送到框架，框架会将它们发送到 PnP 管理器。

接下来，PnP 管理器会确定设备需要的驱动程序，并将其加载（如果尚未加载）。 PnP 管理器将设备的硬件要求列表发送到设备的驱动程序，以便查看。 函数和筛选器驱动程序可以修改此列表并将其发送回 PnP 管理器。

PnP 管理器检查修改的硬件要求列表，并确定哪些指定资源在系统上实际可用。 如果设备要求 PnP 管理器之前分配给另一设备的资源，则 PnP 管理器可能会尝试在系统的设备之间重新 [分发资源](handling-requests-to-stop-a-device.md#redistributing-resources) 。

接下来，PnP 管理器创建 [资源列表](../kernel/hardware-resources.md)，此列表是 PnP 管理器打算分配给设备的资源列表。 PnP 管理器将此列表发送到设备的驱动程序以供查看。 此时，函数和筛选器驱动程序可以从列表中删除资源，但不能向其中添加资源。

最后，PnP 管理器会将资源分配给设备。 框架将资源列表传递到设备的函数和筛选器驱动程序，设备的函数驱动程序将执行必要的初始化，使设备和驱动程序能够访问资源。

以下步骤更详细地介绍了该过程：

1.  [用户插入设备](a-user-plugs-in-a-device.md)。

2.  总线驱动程序检测设备并对其进行 [枚举](enumerating-the-devices-on-a-bus.md) 。

3.  框架调用总线驱动程序的 [*EvtDeviceResourcesQuery*](/windows-hardware/drivers/ddi/wdfpdo/nc-wdfpdo-evt_wdf_device_resources_query) 回调函数，该函数会创建一个描述设备启动配置的 [资源列表](creating-a-resource-list-for-a-boot-configuration.md) 。

4.  框架调用总线驱动程序的 [*EvtDeviceResourceRequirementsQuery*](/windows-hardware/drivers/ddi/wdfpdo/nc-wdfpdo-evt_wdf_device_resource_requirements_query) 回调函数，该函数为设备 [创建资源需求列表](creating-a-resource-requirements-list.md) 。

5.  PnP 管理器会确定设备需要的驱动程序，并将其加载（如果尚未加载），以创建设备的驱动程序堆栈。

6.  PnP 管理器将设备的资源要求列表发送到驱动程序堆栈以供查看。 当列表沿驱动程序堆栈向下传递时，框架将调用每个函数和筛选器驱动程序的 [*EvtDeviceFilterRemoveResourceRequirements*](/windows-hardware/drivers/ddi/wdffdo/nc-wdffdo-evt_wdf_device_filter_resource_requirements) 回调函数。 当列表在堆栈中向上移动时，框架将调用每个函数和筛选器驱动程序的 [*EvtDeviceFilterAddResourceRequirements*](/windows-hardware/drivers/ddi/wdffdo/nc-wdffdo-evt_wdf_device_filter_resource_requirements) 回调函数。 这两个回调函数都可以 [修改资源需求列表](modifying-a-resource-requirements-list.md)。

7.  PnP 管理器为设备创建资源列表，并将其发送到驱动程序堆栈进行查看。 框架调用每个函数和筛选器驱动程序的[*EvtDeviceRemoveAddedResources*](/windows-hardware/drivers/ddi/wdffdo/nc-wdffdo-evt_wdf_device_remove_added_resources)回调函数，该函数将删除驱动程序的*EvtDeviceFilterAddResourceRequirements*回调函数添加的[资源](modifying-a-resource-list.md)，从而使总线驱动程序不会尝试使用它们。

8.  框架从 PnP 管理器接收最终资源列表并存储。

9.  如果驱动程序调用 [**WdfInterruptCreate**](/windows-hardware/drivers/ddi/wdfinterrupt/nf-wdfinterrupt-wdfinterruptcreate) 来创建中断对象，框架将在资源列表中查找中断资源，并将其分配给中断对象。

10. 设备进入未初始化的 D0 状态后，框架将调用每个驱动程序的 [*EvtDevicePrepareHardware*](/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_prepare_hardware) 回调函数，并将设备资源列表的 [原始版本和已翻译](raw-and-translated-resources.md) 版本作为输入参数传递。 驱动程序可以保存资源列表，该列表在框架调用驱动程序的 [*EvtDeviceReleaseHardware*](/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_release_hardware) 回调函数之前有效。

 

