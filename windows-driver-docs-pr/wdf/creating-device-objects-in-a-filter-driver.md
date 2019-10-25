---
title: 在筛选器驱动程序中创建设备对象
description: 在筛选器驱动程序中创建设备对象
ms.assetid: f5a4851d-7caf-467d-9500-11f341fdf680
keywords:
- PnP WDK KMDF，筛选器驱动程序
- 即插即用 WDK KMDF，筛选器驱动程序
- 电源管理 WDK KMDF，筛选器驱动程序
- 筛选器驱动程序 WDK KMDF
- 筛选 DOs WDK KMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0752e13ee7dc6447a373ad826747afe3cab90b1a
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844686"
---
# <a name="creating-device-objects-in-a-filter-driver"></a>在筛选器驱动程序中创建设备对象


每个[筛选器驱动程序](https://docs.microsoft.com/windows-hardware/drivers/kernel/filter-drivers)为系统上存在的每个受支持的设备创建框架设备对象。 由于这些设备对象由筛选器驱动程序创建，因此称为筛选设备对象（筛选器 DOs）。 每个筛选器都是设备的筛选器驱动程序的表示形式。

筛选器驱动程序（如函数驱动程序）提供了一个[*EvtDriverDeviceAdd*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)回调函数，该函数接收[**WDFDEVICE\_INIT**](https://docs.microsoft.com/windows-hardware/drivers/wdf/wdfdevice_init)结构的句柄。 驱动程序可以调用一组相同的[框架设备对象初始化方法](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/#device-init-methods)，这些方法用于函数驱动程序调用以将信息存储在 WDFDEVICE\_INIT 结构中。 与函数驱动程序一样，筛选器驱动程序还可以调用[FRAMEWORK FDO 初始化方法](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/#fdo-init-methods)。

少量筛选器驱动程序枚举仅限子软件的设备。 此类筛选器驱动程序可以调用[框架 PDO 初始化方法](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/#pdo-init-methods)。

筛选器驱动程序必须调用[**WdfFdoInitSetFilter**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdffdo/nf-wdffdo-wdffdoinitsetfilter)。

创建设备对象的最后一步是调用[**WdfDeviceCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicecreate)。

 

 





