---
title: PnP 管理器重新分发系统资源
description: PnP 管理器重新分发系统资源
ms.assetid: c8e6277b-b1e5-449f-b5a0-f5a46b46e56e
keywords:
- 电源管理方案 WDK UMDF，PnP 管理器重新分发系统资源
- 重新分发系统资源方案 WDK UMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f2ab0d6a3bbfe4e93dd7dd1d3054eb98c3dea39a
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72831616"
---
# <a name="the-pnp-manager-redistributes-system-resources"></a>PnP 管理器重新分发系统资源


[!include[UMDF 1 Deprecation](../umdf-1-deprecation.md)]

如果用户将设备添加到系统，并且设备需要 PnP 管理器已分配给另一个设备的系统资源，则 PnP 管理器会尝试重新分配资源。

在此过程中，PnP 管理器会停止设备并使其进入工作（D0）状态。 然后，它将新的资源列表传递到设备，以便它们可以使用新资源重新启动。

重新分发资源时，如果设备的一个基于 UMDF 的驱动程序提供了[**IPnpCallback：： OnQueryStop**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-ipnpcallback-onquerystop)回调函数，并且回调函数否决了重新分配，则 PnP 管理器将不会更改设备的资源分配.

<a href="" id="power-down-sequence"></a>**关机顺序**  
对于支持正在停止的设备的每个基于 UMDF 的函数和筛选器驱动程序，框架按顺序执行以下操作，一次一个驱动程序，从驱动程序堆栈最高的驱动程序开始：

1.  如果驱动程序使用的是自管理 i/o，则框架将调用驱动程序的[**IPnpCallbackSelfManagedIo：： OnSelfManagedIoSuspend**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-ipnpcallbackselfmanagedio-onselfmanagediosuspend)回调函数。

2.  框架停止所有设备的电源托管 i/o 队列。

3.  框架调用驱动程序的[**IPnpCallback：： OnD0Exit**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-ipnpcallback-ond0exit)回调函数（如果存在）。

4.  框架调用驱动程序的[**IPnpCallbackHardware：： OnReleaseHardware**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-ipnpcallbackhardware-onreleasehardware)回调函数（如果存在），传递 PnP 管理器已分配给设备的硬件资源的列表。

若要查看显示这些步骤的关系图，请参阅[断开 a 设备中用户](a-user-unplugs-a-device.md)的有序删除图形。

<a href="" id="power-up-sequence-------"></a>**开机序列**   
对于支持设备的每个基于 UMDF 的函数和筛选器驱动程序，框架按顺序执行以下操作，一次一个驱动程序，从驱动程序堆栈中最低的驱动程序开始：

1.  框架调用驱动程序的[**IPnpCallbackHardware：： OnPrepareHardware**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-ipnpcallbackhardware-onpreparehardware)回调函数（如果存在），传递 PnP 管理器已分配给设备的硬件资源的列表。

2.  框架调用驱动程序的[**IPnpCallback：： OnD0Entry**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-ipnpcallback-ond0entry)回调函数（如果存在）。

3.  框架将重新启动所有设备的电源托管 i/o 队列。

4.  如果驱动程序使用的是自管理 i/o，则框架将调用驱动程序的[**IPnpCallbackSelfManagedIo：： OnSelfManagedIoRestart**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-ipnpcallbackselfmanagedio-onselfmanagediorestart)回调函数。

若要查看显示这些步骤的关系图，请参阅[用户插入设备](a-user-plugs-in-a-device.md)。

 

 





