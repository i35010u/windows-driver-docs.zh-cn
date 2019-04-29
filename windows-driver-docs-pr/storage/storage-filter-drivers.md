---
title: 存储筛选器驱动程序
description: 存储筛选器驱动程序
ms.assetid: 615e8ff1-d5b2-49da-b024-83bbaff70ded
keywords:
- 存储筛选器驱动程序 WDK
- 筛选器驱动程序 WDK 存储
- 存储驱动程序 WDK，筛选器驱动程序
- SFD WDK 存储
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d2600d7b828c92d48b2a05431ae2f62d4ecfc8c8
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63354522"
---
# <a name="storage-filter-drivers"></a>存储筛选器驱动程序


## <span id="ddk_storage_filter_drivers_kg"></span><span id="DDK_STORAGE_FILTER_DRIVERS_KG"></span>


本部分包含以下信息：

[存储筛选器驱动程序支持的输入/输出请求](storage-filter-driver-s-support-of-i-o-requests.md)

[存储筛选器驱动程序的设备类型特定的功能](storage-filter-driver-s-device-type-specific-functionality.md)

[存储筛选器驱动程序 DriverEntry 例程](storage-filter-driver-s-driverentry-routine.md)

[存储筛选器驱动程序 AddDevice 例程](storage-filter-driver-s-adddevice-routine.md)

[处理存储筛选器驱动程序中的即插即用开始](handling-pnp-start-in-a-storage-filter-driver.md)

[存储筛选器驱动程序调度例程](storage-filter-driver-s-dispatch-routines.md)

[存储筛选器驱动程序 IoCompletion 例程](storage-filter-driver-s-iocompletion-routines.md)

[处理分页请求即插即用](handling-pnp-paging-requests.md)

如果为特定类型的设备已存在存储类驱动程序，它可能不必编写相同类型的新设备的驱动程序。 每个系统提供的存储类驱动程序设计为支持给定类型的外围设备和针对多个供应商的设备进行测试。 因此，任何系统提供的存储类驱动程序可能会提供所有支持的其类型的要求的另一台设备。

如果现有的存储类驱动程序不完全支持其类型的新设备，新的驱动程序可以编写为存储筛选器驱动程序 (SFD) 的分层或过现有的系统提供的类驱动程序。 SFD 可能转换数据在读/写请求定义其他 I/O 控制代码 (Ioctl) 使用户应用程序能够充分利用特定设备的其他功能或解决而无需特定于设备的问题对泛型类或端口驱动程序的特定于硬件的更改。

除非新设备需要的每个请求进行处理以特定于设备的方式，可以在更少时间比新的存储类驱动程序中开发存储筛选器驱动程序。

 

 




