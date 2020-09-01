---
title: 修改资源列表
description: 修改资源列表
ms.assetid: 571b2990-5627-434e-b8fc-d2564188f544
keywords:
- 启动配置资源列表 WDK KMDF，修改
- 硬件资源 WDK KMDF，资源列表
- 资源列表 WDK KMDF，修改
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 27925b79c8b6070c7d0f948db541513feeb7c4e9
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89193103"
---
# <a name="modifying-a-resource-list"></a>修改资源列表


如果驱动程序提供了 [*EvtDeviceFilterAddResourceRequirements*](/windows-hardware/drivers/ddi/wdffdo/nc-wdffdo-evt_wdf_device_filter_resource_requirements) 回调函数，它还必须提供 [*EvtDeviceRemoveAddedResources*](/windows-hardware/drivers/ddi/wdffdo/nc-wdffdo-evt_wdf_device_remove_added_resources) 回调函数。 *EvtDeviceRemoveAddedResources*回调函数删除*EvtDeviceFilterAddResourceRequirements*回调函数添加的资源，以便总线驱动程序不会尝试使用它们。

若要修改设备资源列表中的资源描述符，驱动程序应调用以下方法：

-   [**WdfCmResourceListGetCount**](/windows-hardware/drivers/ddi/wdfresource/nf-wdfresource-wdfcmresourcelistgetcount)，用于获取资源说明符的数目。

-   [**WdfCmResourceListGetDescriptor**](/windows-hardware/drivers/ddi/wdfresource/nf-wdfresource-wdfcmresourcelistgetdescriptor)，用于获取对资源描述符的访问权限。

-   [**WdfCmResourceListRemove**](/windows-hardware/drivers/ddi/wdfresource/nf-wdfresource-wdfcmresourcelistremove) 和 [**WdfCmResourceListRemoveByDescriptor**](/windows-hardware/drivers/ddi/wdfresource/nf-wdfresource-wdfcmresourcelistremovebydescriptor)，用于删除资源描述符。

如果驱动程序删除资源，则它必须从 [原始资源列表和已转换资源列表](raw-and-translated-resources.md)中将其删除。

 

