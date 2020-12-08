---
title: 在筛选器驱动程序中创建设备对象
description: 在筛选器驱动程序中创建设备对象
keywords:
- PnP WDK KMDF，筛选器驱动程序
- 即插即用 WDK KMDF，筛选器驱动程序
- 电源管理 WDK KMDF，筛选器驱动程序
- 筛选器驱动程序 WDK KMDF
- 筛选 DOs WDK KMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: aadf5df123ae1ce92b722fdfb285c70006043386
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96829001"
---
# <a name="creating-device-objects-in-a-filter-driver"></a>在筛选器驱动程序中创建设备对象


每个 [筛选器驱动程序](../kernel/filter-drivers.md) 为系统上存在的每个受支持的设备创建框架设备对象。 由于这些设备对象由筛选器驱动程序创建，因此它们被称为筛选器设备对象 (筛选器 DOs) 。 每个筛选器都是设备的筛选器驱动程序的表示形式。

筛选器驱动程序（如函数驱动程序）提供了一个 [*EvtDriverDeviceAdd*](/windows-hardware/drivers/ddi/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add) 回调函数，该函数接收 [**WDFDEVICE \_ INIT**](./wdfdevice_init.md) 结构的句柄。 驱动程序可以调用一组相同的 [框架设备对象初始化方法](/windows-hardware/drivers/ddi/wdfdevice/#device-init-methods) ，函数驱动程序调用该方法来存储 WDFDEVICE \_ INIT 结构中的信息。 与函数驱动程序一样，筛选器驱动程序还可以调用 [FRAMEWORK FDO 初始化方法](/windows-hardware/drivers/ddi/wdfdevice/#fdo-init-methods)。

少量筛选器驱动程序枚举仅限子软件的设备。 此类筛选器驱动程序可以调用 [框架 PDO 初始化方法](/windows-hardware/drivers/ddi/wdfdevice/#pdo-init-methods)。

筛选器驱动程序必须调用 [**WdfFdoInitSetFilter**](/windows-hardware/drivers/ddi/wdffdo/nf-wdffdo-wdffdoinitsetfilter)。

创建设备对象的最后一步是调用 [**WdfDeviceCreate**](/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicecreate)。

 

