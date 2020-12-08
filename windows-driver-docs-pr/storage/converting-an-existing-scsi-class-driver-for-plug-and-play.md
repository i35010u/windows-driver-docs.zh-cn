---
title: 转换现有的即插即用型 SCSI 类驱动程序
description: 转换现有的即插即用型 SCSI 类驱动程序
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
ms.openlocfilehash: d31012344e2f0cc18d0dabce42571850d23ab20e
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96804717"
---
# <a name="converting-an-existing-scsi-class-driver-for-plug-and-play"></a>转换现有的即插即用型 SCSI 类驱动程序


## <span id="ddk_converting_an_existing_scsi_class_driver_for_plug_and_play_kg"></span><span id="DDK_CONVERTING_AN_EXISTING_SCSI_CLASS_DRIVER_FOR_PLUG_AND_PLAY_KG"></span>


若要成功运行为 PnP 驱动程序，必须修改现有的 SCSI 类驱动程序，如下所示：

-   驱动程序初始化代码必须遵循即插即用驱动程序的初始化规则。 现有 SCSI 驱动程序的 **DriverEntry** 例程中的功能划分为存储类驱动程序的 **DriverEntry**、 *AddDevice* 和 *DispatchPnP* 例程，如存储类 [驱动程序的 DriverEntry 例程](storage-class-driver-s-driverentry-routine.md)、 [存储类驱动程序的 AddDevice 例程](storage-class-driver-s-adddevice-routine.md)以及 [处理存储类驱动程序中的 PnP 启动中](handling-pnp-start-in-a-storage-class-driver.md)所述。

-   生成 SRBs 的代码不得将 **PathId**、 **TargetId** 和 **Lun** 字段设置为目标设备地址，并应将这些字段初始化为0xff。 设备地址在代表设备的 PDO 中是隐式的，驱动程序必须仅与此类设备对象通信，因此类驱动程序不需要提供设备地址。

-   通过发出 [**ioctl \_ scsi \_ get \_ 查询 \_ 数据**](/windows-hardware/drivers/ddi/ntddscsi/ni-ntddscsi-ioctl_scsi_get_inquiry_data) 和 [**IOCTL \_ scsi \_ get \_ 功能**](/windows-hardware/drivers/ddi/ntddscsi/ni-ntddscsi-ioctl_scsi_get_capabilities) 请求来获取 SCSI 查询和功能数据的代码应发出 [**ioctl \_ 存储 \_ 查询 \_ 属性**](/windows-hardware/drivers/ddi/ntddstor/ni-ntddstor-ioctl_storage_query_property) 请求来检索设备和适配器描述符。

-   驱动程序必须处理 PnP 请求，以启动、停止和删除设备，并且必须具有一种机制，以便在处理此类请求时会干扰数据传输或系统操作时失败。 例如，如果驱动程序的设备包含系统页文件，则该驱动程序应使查询删除、查询停止或停止请求失败。 此类驱动程序应 \_ \_ 使用 [**irp \_ MN \_ 设备 \_ 使用 \_ 通知**](../kernel/irp-mn-device-usage-notification.md) 和 **DeviceUsageTypePaging**) 的通知类型处理寻呼通知 (请求，以维护其设备上页面文件的计数。

-   驱动程序必须处理请求以更改设备的电源状态 (IRP \_ MJ \_ Power with [**irp \_ MN \_ QUERY \_ power**](../kernel/irp-mn-query-power.md) and [**irp \_ MN \_ SET \_ power**](../kernel/irp-mn-set-power.md)) ，在电源状态转换期间必须阻止对设备的 i/o。

 

