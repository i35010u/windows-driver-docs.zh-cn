---
title: 原始资源和已转换的资源
description: 原始资源和已转换的资源
ms.assetid: dfc1376d-7a1a-421c-82ae-e183cac77ec8
keywords:
- 硬件资源 WDK KMDF，原始资源
- 资源列出了 WDK KMDF
- 硬件资源 WDK KMDF，翻译后的资源
- 已翻译的资源 WDK KMDF
- 原始资源 WDK KMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d670968e08cdbae0e5dc5699bc987fcb0dc221c0
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67376305"
---
# <a name="raw-and-translated-resources"></a>原始资源和已转换的资源


当驱动程序的[ *EvtDeviceRemoveAddedResources* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdffdo/nc-wdffdo-evt_wdf_device_remove_added_resources)或[ *EvtDevicePrepareHardware* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_prepare_hardware)回调函数接收资源列表中，它会收到两个版本的列表。 一个版本表示的设备*原始资源*，和另一个表示设备的*资源转换*。 这两个版本表示同一组中的顺序相同的硬件资源。

-   原始资源是由相对于该设备连接到总线的地址标识的资源。 通常情况下，程序设备驱动程序提供这些地址到设备。

-   翻译后的资源是由系统驱动程序用于访问资源的物理地址标识的资源。

PCI 总线设备驱动程序接收到设备中出现的顺序列出的资源*基本地址注册*（条形图）。 但是，可能会更多资源描述符交错在列表中，以便索引处的资源*X*栏中可能不匹配资源列表中的同一个索引位置处的资源。

有关原始和已翻译的资源的详细信息，请参阅成员的说明[ **CM\_分部\_资源\_描述符**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_cm_partial_resource_descriptor)结构。

如果设备的翻译资源列表包含具有的资源**类型**CM 成员\_分部\_资源\_描述符结构设置为**CmResourceTypeMemory**，每个访问该资源的驱动程序必须执行以下操作：

-   在驱动程序[ *EvtDevicePrepareHardware* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_prepare_hardware)回调函数必须调用[ **MmMapIoSpace** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-mmmapiospace)将映射到系统物理地址系统虚拟地址。
-   在驱动程序[ *EvtDeviceReleaseHardware* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_release_hardware)回调函数必须调用[ **MmUnmapIoSpace** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-mmunmapiospace)取消地址的映射。

有关映射总线相对地址的详细信息，请参阅[映射到的虚拟地址的总线相对地址](https://docs.microsoft.com/windows-hardware/drivers/kernel/mapping-bus-relative-addresses-to-virtual-addresses)。

 

 





