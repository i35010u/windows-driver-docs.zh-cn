---
title: 在筛选器驱动程序中创建设备对象
description: 在筛选器驱动程序中创建设备对象
ms.assetid: f5a4851d-7caf-467d-9500-11f341fdf680
keywords:
- 即插即用 WDK KMDF，筛选器驱动程序
- 插 WDK KMDF，筛选器驱动程序
- 电源管理 WDK KMDF，筛选器驱动程序
- 筛选器驱动程序 WDK KMDF
- 筛选 DOs WDK KMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4937ea8ab634ffc7a87407ab01b670d04bf37100
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67377505"
---
# <a name="creating-device-objects-in-a-filter-driver"></a>在筛选器驱动程序中创建设备对象


每个[筛选器驱动程序](https://docs.microsoft.com/windows-hardware/drivers/kernel/filter-drivers)为每个系统不存在其受支持的设备创建 framework 设备对象。 因为这些设备对象创建的筛选器驱动程序，它们被称为筛选设备对象 (筛选器 DOs)。 每个筛选器做的就是设备的筛选器驱动程序的表示形式。

筛选器驱动程序，如功能的驱动程序，提供[ *EvtDriverDeviceAdd* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)回调函数接收的句柄[ **WDFDEVICE\_INIT**](https://docs.microsoft.com/windows-hardware/drivers/wdf/wdfdevice_init)结构。 该驱动程序可以调用相同的一组[framework 设备对象初始化方法](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/#device-init-methods)函数的驱动程序调用，以将信息存储在 WDFDEVICE\_INIT 结构。 功能的驱动程序，如筛选器驱动程序还可以调用[framework FDO 初始化方法](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/#fdo-init-methods)。

少量的筛选器驱动程序枚举子仅限软件的设备。 此类筛选器驱动程序可以调用[framework PDO 初始化方法](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/#pdo-init-methods)。

筛选器驱动程序必须调用[ **WdfFdoInitSetFilter**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdffdo/nf-wdffdo-wdffdoinitsetfilter)。

创建设备对象的最后一步是调用[ **WdfDeviceCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdevicecreate)。

 

 





