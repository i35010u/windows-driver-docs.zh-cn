---
title: 转换现有的即插即用型 SCSI 类驱动程序
description: 转换现有的即插即用型 SCSI 类驱动程序
ms.assetid: b6570eef-f425-4b73-aa8a-7084f53bb10a
keywords:
- 存储类驱动程序 WDK，转换 SCSI 类驱动程序
- 类驱动程序 WDK 存储，转换 SCSI 类驱动程序
- 存储类驱动程序 WDK、PnP
- 类驱动程序 WDK 存储，PnP
- PnP WDK 存储
- 即插即用 WDK 存储
- 转换 SCSI 类驱动程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 09c2d3e4f278870aa9a7be39906ec26189b3e624
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844579"
---
# <a name="converting-an-existing-scsi-class-driver-for-plug-and-play"></a>转换现有的即插即用型 SCSI 类驱动程序


## <span id="ddk_converting_an_existing_scsi_class_driver_for_plug_and_play_kg"></span><span id="DDK_CONVERTING_AN_EXISTING_SCSI_CLASS_DRIVER_FOR_PLUG_AND_PLAY_KG"></span>


若要成功运行为 PnP 驱动程序，必须修改现有的 SCSI 类驱动程序，如下所示：

-   驱动程序初始化代码必须遵循即插即用驱动程序的初始化规则。 现有 SCSI 驱动程序的**DriverEntry**例程中的功能划分为存储类驱动程序的**DriverEntry**、 *AddDevice*和*DispatchPnP*例程，如[存储类驱动程序的 DriverEntry 中所述。例程](storage-class-driver-s-driverentry-routine.md)、[存储类驱动程序的 AddDevice 例程](storage-class-driver-s-adddevice-routine.md)，并[处理存储类驱动程序中的 PnP 启动](handling-pnp-start-in-a-storage-class-driver.md)。

-   生成 SRBs 的代码不得将**PathId**、 **TargetId**和**Lun**字段设置为目标设备地址，并应将这些字段初始化为0xff。 设备地址在代表设备的 PDO 中是隐式的，驱动程序必须仅与此类设备对象通信，因此类驱动程序不需要提供设备地址。

-   通过发出 Ioctl\_SCSI\_获取 SCSI 查询和功能数据的代码，该代码可获取[ **\_查询\_数据**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddscsi/ni-ntddscsi-ioctl_scsi_get_inquiry_data)和[**IOCTL\_scsi\_获取\_功能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddscsi/ni-ntddscsi-ioctl_scsi_get_capabilities)请求应发出[**IOCTL\_存储\_查询**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddstor/ni-ntddstor-ioctl_storage_query_property)改为检索设备和适配器描述符\_属性请求。

-   驱动程序必须处理 PnP 请求，以启动、停止和删除设备，并且必须具有一种机制，以便在处理此类请求时会干扰数据传输或系统操作时失败。 例如，如果驱动程序的设备包含系统页文件，则该驱动程序应使查询删除、查询停止或停止请求失败。 此类驱动程序应处理寻呼通知请求（IRP\_MJ\_PNP，并使用[**irp\_MN\_设备\_使用情况\_通知**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-device-usage-notification)和通知类型为**DeviceUsageTypePaging**）来维护页面文件。

-   驱动程序必须处理请求以更改设备的电源状态（IRP\_MJ\_POWER with [**irp\_MN\_查询\_power**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-power) and [**IRP**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-set-power)\_\_\_，而且必须在电源状态转换期间阻止设备的 i/o。

 

 




