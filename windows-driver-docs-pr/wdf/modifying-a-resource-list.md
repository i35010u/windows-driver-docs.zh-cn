---
title: 修改资源列表
description: 修改资源列表
keywords:
- 启动配置资源列表 WDK KMDF，修改
- 硬件资源 WDK KMDF，资源列表
- 资源列表 WDK KMDF，修改
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2f2e2499afe3524594b11c4dac6f64a404a6b658
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96783681"
---
# <a name="modifying-a-resource-list"></a>修改资源列表


如果驱动程序提供了 [*EvtDeviceFilterAddResourceRequirements*](/windows-hardware/drivers/ddi/wdffdo/nc-wdffdo-evt_wdf_device_filter_resource_requirements) 回调函数，它还必须提供 [*EvtDeviceRemoveAddedResources*](/windows-hardware/drivers/ddi/wdffdo/nc-wdffdo-evt_wdf_device_remove_added_resources) 回调函数。 *EvtDeviceRemoveAddedResources* 回调函数删除 *EvtDeviceFilterAddResourceRequirements* 回调函数添加的资源，以便总线驱动程序不会尝试使用它们。

若要修改设备资源列表中的资源描述符，驱动程序应调用以下方法：

-   [**WdfCmResourceListGetCount**](/windows-hardware/drivers/ddi/wdfresource/nf-wdfresource-wdfcmresourcelistgetcount)，用于获取资源说明符的数目。

-   [**WdfCmResourceListGetDescriptor**](/windows-hardware/drivers/ddi/wdfresource/nf-wdfresource-wdfcmresourcelistgetdescriptor)，用于获取对资源描述符的访问权限。

-   [**WdfCmResourceListRemove**](/windows-hardware/drivers/ddi/wdfresource/nf-wdfresource-wdfcmresourcelistremove) 和 [**WdfCmResourceListRemoveByDescriptor**](/windows-hardware/drivers/ddi/wdfresource/nf-wdfresource-wdfcmresourcelistremovebydescriptor)，用于删除资源描述符。

如果驱动程序删除资源，则它必须从 [原始资源列表和已转换资源列表](raw-and-translated-resources.md)中将其删除。

 

