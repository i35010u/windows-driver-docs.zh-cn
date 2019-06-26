---
title: 修改资源要求列表
description: 修改资源要求列表
ms.assetid: 75391dd2-5ae1-4562-97a0-4de21a08b61c
keywords:
- 列出了硬件资源 WDK KMDF，修改资源要求
- 资源要求列表 WDK KMDF，修改
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a4a9a1a5639b67a1264c5536dffd1b8cb0570d33
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67376658"
---
# <a name="modifying-a-resource-requirements-list"></a>修改资源要求列表


PnP 管理器可确保，所有新连接的设备驱动程序后已加载，它将设备的硬件要求列表发送到设备的驱动程序堆栈。

当列表下堆栈传输时，框架将调用每个函数和筛选器驱动程序的[ *EvtDeviceFilterRemoveResourceRequirements* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdffdo/nc-wdffdo-evt_wdf_device_filter_resource_requirements)回调函数，传递形式的硬件要求列表输入的参数。 此回调函数可以从已指定总线驱动程序，但该功能驱动程序确定，则不需要使设备能够运行的硬件要求列表中删除硬件资源。

例如，PCI 总线驱动程序可能符合 PCI 规范中，复制内存空间中的 I/O 空间资源。 如果你的设备可以运行而无需使用 I/O 空间资源，设备的功能驱动程序可以从硬件要求列表中删除 I/O 空间资源。

从要求列表中删除项目，驱动程序可以执行以下操作：

-   调用以下方法来修改资源要求列表中的逻辑配置：
    -   [**WdfIoResourceRequirementsListGetCount**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfresource/nf-wdfresource-wdfioresourcerequirementslistgetcount)，以获取多个逻辑配置。
    -   [**WdfIoResourceRequirementsListGetIoResList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfresource/nf-wdfresource-wdfioresourcerequirementslistgetioreslist)，以获取访问逻辑配置。
    -   [**WdfIoResourceRequirementsListRemove** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfresource/nf-wdfresource-wdfioresourcerequirementslistremove)并[ **WdfIoResourceRequirementsListRemoveByIoResList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfresource/nf-wdfresource-wdfioresourcerequirementslistremovebyioreslist)，以删除逻辑配置。
-   调用以下方法来修改逻辑配置中的资源描述符：
    -   [**WdfIoResourceListGetCount**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfresource/nf-wdfresource-wdfioresourcelistgetcount)，以获取资源说明符的数目。
    -   [**WdfIoResourceListGetDescriptor**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfresource/nf-wdfresource-wdfioresourcelistgetdescriptor)，以获取对资源描述符访问权限。
    -   [**WdfIoResourceListRemove** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfresource/nf-wdfresource-wdfioresourcelistremove)并[ **WdfIoResourceListRemoveByDescriptor**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfresource/nf-wdfresource-wdfioresourcelistremovebydescriptor)，若要删除的资源描述符。

当列表传输到驱动程序堆栈时，框架将调用每个函数和筛选器驱动程序的[ *EvtDeviceFilterAddResourceRequirements* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdffdo/nc-wdffdo-evt_wdf_device_filter_resource_requirements)回调函数，传递的硬件要求作为输入参数的列表。 此回调函数可以添加额外的硬件资源功能驱动程序所需的用于使设备可操作。

若要将项添加到硬件要求列表，驱动程序可以执行以下操作：

-   调用以下方法来修改资源要求列表中的逻辑配置：
    -   [**WdfIoResourceRequirementsListGetCount**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfresource/nf-wdfresource-wdfioresourcerequirementslistgetcount)，以获取多个逻辑配置。
    -   [**WdfIoResourceRequirementsListGetIoResList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfresource/nf-wdfresource-wdfioresourcerequirementslistgetioreslist)，以获取访问逻辑配置。
    -   [**WdfIoResourceListCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfresource/nf-wdfresource-wdfioresourcelistcreate)，以创建新的逻辑配置。
    -   [**WdfIoResourceRequirementsListAppendIoResList** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfresource/nf-wdfresource-wdfioresourcerequirementslistappendioreslist)或[ **WdfIoResourceRequirementsListInsertIoResList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfresource/nf-wdfresource-wdfioresourcerequirementslistinsertioreslist)，以添加新的逻辑配置。
-   调用以下方法来修改逻辑配置中的资源描述符：
    -   [**WdfIoResourceListGetCount**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfresource/nf-wdfresource-wdfioresourcelistgetcount)，以获取资源说明符的数目。
    -   [**WdfIoResourceListGetDescriptor**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfresource/nf-wdfresource-wdfioresourcelistgetdescriptor)，以获取对资源描述符访问权限。
    -   [**WdfIoResourceListAppendDescriptor** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfresource/nf-wdfresource-wdfioresourcelistappenddescriptor)或[ **WdfIoResourceListInsertDescriptor**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfresource/nf-wdfresource-wdfioresourcelistinsertdescriptor)，以添加资源描述符。

 

 





