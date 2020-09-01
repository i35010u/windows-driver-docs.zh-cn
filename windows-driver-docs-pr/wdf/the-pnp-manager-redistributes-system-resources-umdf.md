---
title: 'PnP 管理器将系统资源重新分发 (UMDF 1) '
description: PnP 管理器重新分发系统资源
ms.assetid: c8e6277b-b1e5-449f-b5a0-f5a46b46e56e
keywords:
- 电源管理方案 WDK UMDF，PnP 管理器重新分发系统资源
- 重新分发系统资源方案 WDK UMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 75a421b605d2d85f5ae4e108152030ed547d091c
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89191411"
---
# <a name="the-pnp-manager-redistributes-system-resources-umdf-1"></a>PnP 管理器将系统资源重新分发 (UMDF 1) 


[!include[UMDF 1 Deprecation](../includes/umdf-1-deprecation.md)]

如果用户将设备添加到系统，并且设备需要 PnP 管理器已分配给另一个设备的系统资源，则 PnP 管理器会尝试重新分配资源。

在此过程中，PnP 管理器会停止设备，并使其进入工作 (D0) 状态。 然后，它将新的资源列表传递到设备，以便它们可以使用新资源重新启动。

重新分发资源时，如果某个设备的基于 UMDF 的驱动程序提供了 [**IPnpCallback：： OnQueryStop**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-ipnpcallback-onquerystop) 回调函数，并且回调函数拒绝了重新分配，则 PnP 管理器将不会更改设备的资源分配。

<a href="" id="power-down-sequence"></a>**关机顺序**  
对于支持正在停止的设备的每个基于 UMDF 的函数和筛选器驱动程序，框架按顺序执行以下操作，一次一个驱动程序，从驱动程序堆栈最高的驱动程序开始：

1.  如果驱动程序使用的是自管理 i/o，则框架将调用驱动程序的 [**IPnpCallbackSelfManagedIo：： OnSelfManagedIoSuspend**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-ipnpcallbackselfmanagedio-onselfmanagediosuspend) 回调函数。

2.  框架停止所有设备的电源托管 i/o 队列。

3.  如果) 存在该驱动程序，则框架将调用该驱动程序的 [**IPnpCallback：： OnD0Exit**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-ipnpcallback-ond0exit) 回调函数 (。

4.  框架将调用驱动程序的 [**IPnpCallbackHardware：： OnReleaseHardware**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-ipnpcallbackhardware-onreleasehardware) 回调函数 (如果它存在) 传递 PnP 管理器已分配给设备的硬件资源的列表。

若要查看显示这些步骤的关系图，请参阅 [断开 a 设备中用户](a-user-unplugs-a-device.md)的有序删除图形。

<a href="" id="power-up-sequence-------"></a>**通电顺序**   
对于支持设备的每个基于 UMDF 的函数和筛选器驱动程序，框架按顺序执行以下操作，一次一个驱动程序，从驱动程序堆栈中最低的驱动程序开始：

1.  如果) 存在驱动程序的 [**IPnpCallbackHardware：： OnPrepareHardware**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-ipnpcallbackhardware-onpreparehardware) 回调函数，则框架将调用该驱动程序的：：回调 (函数，同时传递 PnP 管理器已分配给该设备的硬件资源的列表。

2.  如果) 存在该驱动程序，则框架将调用该驱动程序的 [**IPnpCallback：： OnD0Entry**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-ipnpcallback-ond0entry) 回调函数 (。

3.  框架将重新启动所有设备的电源托管 i/o 队列。

4.  如果驱动程序使用的是自管理 i/o，则框架将调用驱动程序的 [**IPnpCallbackSelfManagedIo：： OnSelfManagedIoRestart**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-ipnpcallbackselfmanagedio-onselfmanagediorestart) 回调函数。

若要查看显示这些步骤的关系图，请参阅 [用户插入设备](a-user-plugs-in-a-device.md)。

 

