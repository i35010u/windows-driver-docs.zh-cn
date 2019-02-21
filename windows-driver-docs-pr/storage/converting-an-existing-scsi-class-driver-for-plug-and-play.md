---
title: 转换 Plug and play 现有 SCSI 类驱动程序
description: 转换 Plug and play 现有 SCSI 类驱动程序
ms.assetid: b6570eef-f425-4b73-aa8a-7084f53bb10a
keywords:
- 存储类驱动程序 WDK，转换 SCSI 类驱动程序
- 类驱动程序 WDK 存储，将转换 SCSI 类驱动程序
- 存储类驱动程序 WDK，即插即用
- 类驱动程序 WDK 存储，即插即用
- 即插即用 WDK 存储
- 插 WDK 存储
- 转换 SCSI 类驱动程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c5699ca81b8297f3fbb0eb484eb909a37de804f8
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56526212"
---
# <a name="converting-an-existing-scsi-class-driver-for-plug-and-play"></a>转换 Plug and play 现有 SCSI 类驱动程序


## <span id="ddk_converting_an_existing_scsi_class_driver_for_plug_and_play_kg"></span><span id="DDK_CONVERTING_AN_EXISTING_SCSI_CLASS_DRIVER_FOR_PLUG_AND_PLAY_KG"></span>


要作为即插即用驱动程序成功运行，必须按如下所示修改现有的 SCSI 类驱动程序：

-   驱动程序初始化代码必须遵循的规则插驱动程序的初始化。 中的功能**DriverEntry**例程现有 SCSI 驱动程序中进行划分**DriverEntry**， *AddDevice*，和*DispatchPnP*存储类驱动程序，如中所述的例程[存储类驱动程序 DriverEntry 例程](storage-class-driver-s-driverentry-routine.md)，[存储类驱动程序 AddDevice 例程](storage-class-driver-s-adddevice-routine.md)，并[处理存储类驱动程序中的即插即用开始](handling-pnp-start-in-a-storage-class-driver.md)。

-   不能设置代码生成 Srb **PathId**， **TargetId**，和**Lun**字段到目标设备地址，并应初始化这些字段到 0xFF。 设备地址是隐式的 PDO，表示设备和驱动程序必须仅与此类设备对象，通信，因此不需要类驱动程序提供的设备地址。

-   通过发出获取 SCSI 查询和功能数据的代码[ **IOCTL\_SCSI\_获取\_查询\_数据**](https://msdn.microsoft.com/library/windows/hardware/ff560509)和[ **IOCTL\_SCSI\_获取\_功能**](https://msdn.microsoft.com/library/windows/hardware/ff560502)发出请求应[ **IOCTL\_存储\_查询\_属性**](https://msdn.microsoft.com/library/windows/hardware/ff560590)改为检索设备和适配器描述符的请求。

-   该驱动程序必须处理即插即用请求，以启动、 停止和删除设备，并且必须具有一种机制以处理它将影响数据传输或系统操作故障这样的请求。 例如，驱动程序应失败查询、 删除、 查询停止或停止请求，如果其设备包含系统页面文件。 此类驱动程序应处理分页通知请求 (IRP\_MJ\_与 PNP [ **IRP\_MN\_设备\_用法\_通知**](https://msdn.microsoft.com/library/windows/hardware/ff550841)和通知类型**DeviceUsageTypePaging**) 来维护其设备上的页面文件的计数。

-   该驱动程序必须处理请求，以更改设备的电源状态 (IRP\_MJ\_具有 POWER [ **IRP\_MN\_查询\_POWER** ](https://msdn.microsoft.com/library/windows/hardware/ff551699)并[ **IRP\_MN\_设置\_POWER**](https://msdn.microsoft.com/library/windows/hardware/ff551744))，和必须阻止 I/O 设备电源状态转换期间。

 

 




