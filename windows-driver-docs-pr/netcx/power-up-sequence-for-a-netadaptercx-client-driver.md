---
title: NetAdapterCx 客户端驱动程序的启动顺序
description: NetAdapterCx 客户端驱动程序的启动顺序
ms.assetid: 86694F6B-9AE4-4FDB-A4BB-9B7ACBC0B1DA
keywords:
- NetAdapterCx 客户端驱动程序的通电顺序，NetAdapterCx 客户端驱动程序的通电顺序，NetCx 客户端驱动程序的开机序列
ms.date: 08/07/2018
ms.localizationpriority: medium
ms.openlocfilehash: 338fdff71b81c017161d4715b6cccec54eb0dc6b
ms.sourcegitcommit: d30691c8276f7dddd3f8333e84744ddeea1e1020
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/19/2019
ms.locfileid: "75209009"
---
# <a name="power-up-sequence-for-a-netadaptercx-client-driver"></a>NetAdapterCx 客户端驱动程序的启动顺序

下图显示了当设备到完全操作状态时，NetAdapterCx 调用客户端驱动程序的事件回调函数的顺序，从图底部的设备到达状态开始：

<img src="images/netadaptercx-powerup.png" alt="Device enumeration and power-up sequence for NetAdapterCx client driver" title="NetAdapterCx 客户端驱动程序的设备枚举和通电顺序" style="width: 600px;"/>

大水平行用于标记启动设备所涉及的步骤。 图左侧的列描述了步骤，右侧的列列出了完成该步骤的事件回调。 用蓝色文本标记的步骤特定于 NetAdapterCx，而其他步骤则适用于所有基于 WDF 的驱动程序。

在图的底部，设备上不存在设备。 当用户插入设备时，框架首先调用驱动程序的[*EvtDriverDeviceAdd*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)回调，以便驱动程序可以创建设备对象来表示设备。 此框架通过在整个序列中向上遍历来继续调用驱动程序的回调例程，直到设备正常运行。 请记住，框架按下图所示的下向下顺序调用事件回调，因此在[*EvtDeviceFilterAddResourceRequirements*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdffdo/nc-wdffdo-evt_wdf_device_filter_resource_requirements)之前调用[*EvtDeviceFilterRemoveResourceRequirements*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdffdo/nc-wdffdo-evt_wdf_device_filter_resource_requirements) 。 如果设备已停止重新平衡资源，或者物理上存在但处于低功耗状态，则不需要执行所有步骤，如图所示。

