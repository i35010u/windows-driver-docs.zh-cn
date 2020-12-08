---
title: 原始资源和已转换的资源
description: 原始资源和已转换的资源
keywords:
- 硬件资源 WDK KMDF，原始资源
- 资源列表 WDK KMDF
- 硬件资源 WDK KMDF，已翻译的资源
- 翻译的资源 WDK KMDF
- 原始资源 WDK KMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d602aebeb8af665a520df7c39ac8f90ed2c5343b
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96827411"
---
# <a name="raw-and-translated-resources"></a>原始资源和已转换的资源


当驱动程序的 [*EvtDeviceRemoveAddedResources*](/windows-hardware/drivers/ddi/wdffdo/nc-wdffdo-evt_wdf_device_remove_added_resources) 或 [*EvtDevicePrepareHardware*](/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_prepare_hardware) 回调函数收到资源列表时，它将接收两个版本的列表。 一个版本表示设备的 *原始资源*，另一个版本表示设备的已 *转换资源*。 这两个版本以相同的顺序表示相同的一组硬件资源。

-   原始资源是由与设备所连接的总线相关的地址标识的资源。 通常，驱动程序将设备提供给设备的驱动程序。

-   翻译资源是由驱动程序用于访问资源的系统物理地址标识的资源。

PCI 总线设备的驱动程序接收按其在设备的 *基本地址注册* (条) 中出现的顺序列出的资源。 但是，其他资源描述符可能会交错在列表中，这样，条形图中索引 *X* 处的资源可能与资源列表中的同一索引位置处的资源不匹配。

有关原始资源和已翻译资源的详细信息，请参阅 [**CM \_ 部分 \_ 资源 \_ 描述符**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_cm_partial_resource_descriptor) 结构的成员说明。

如果设备的已翻译资源列表包含一个资源，而 **Type** 该资源的 CM \_ 部分资源描述符结构的 Type 成员 \_ \_ 设置为 **CmResourceTypeMemory**，则访问该资源的每个驱动程序都必须执行以下操作：

-   驱动程序的 [*EvtDevicePrepareHardware*](/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_prepare_hardware) 回调函数必须调用 [**MmMapIoSpace**](/windows-hardware/drivers/ddi/wdm/nf-wdm-mmmapiospace) ，以将系统物理地址映射到系统虚拟地址。
-   驱动程序的 [*EvtDeviceReleaseHardware*](/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_release_hardware) 回调函数必须调用 [**MmUnmapIoSpace**](/windows-hardware/drivers/ddi/wdm/nf-wdm-mmunmapiospace) 来取消对地址的映射。

有关映射总线相对地址的详细信息，请参阅 [将 Bus-Relative 地址映射到虚拟地址](../kernel/mapping-bus-relative-addresses-to-virtual-addresses.md)。

 

