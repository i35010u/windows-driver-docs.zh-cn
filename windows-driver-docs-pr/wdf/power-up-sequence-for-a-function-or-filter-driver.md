---
title: 函数或筛选器驱动程序的启动顺序
description: 函数或筛选器驱动程序的启动顺序
ms.assetid: 3E904641-A1E2-400C-A201-2D1D2D359657
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ee3e01022ba97e1c3778204f41b5a34ddb68186d
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67376339"
---
# <a name="power-up-sequence-for-a-function-or-filter-driver"></a>函数或筛选器驱动程序的启动顺序


下图显示了使设备为完全可操作的状态，从该图底部的设备插入状态时框架调用 KMDF 函数或筛选器驱动程序的事件回调函数的顺序：

![函数或筛选器驱动程序的设备枚举和增益道具序列](images/fdo-fido-powerup.png)

广泛的水平线将标记中启动设备所涉及的步骤。 图左侧列描述相应步骤，并在右侧列列出完成该操作的事件回调。

在该图底部，设备不存在系统上。 框架在用户插入设备，首先调用驱动程序的[ *EvtDriverDeviceAdd* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)回调，以便该驱动程序可以创建一个设备对象来表示该设备。 框架将继续进行向上访问序列，直到该设备正常调用驱动程序的回调例程。 请记住，框架会因此调用图中所示的自下而上的顺序中的事件回调[ *EvtDeviceFilterRemoveResourceRequirements* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdffdo/nc-wdffdo-evt_wdf_device_filter_resource_requirements)之前调用[ *EvtDeviceFilterAddResourceRequirements* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdffdo/nc-wdffdo-evt_wdf_device_filter_resource_requirements) ，依此类推。 如果设备已停止来重新平衡资源，或以物理方式存在，但在低功耗状态，并非所有的步骤是必需的如图所示。

 

 





