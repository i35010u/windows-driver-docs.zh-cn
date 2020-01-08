---
title: 存储筛选器驱动程序简介
description: 存储筛选器驱动程序
ms.assetid: 615e8ff1-d5b2-49da-b024-83bbaff70ded
keywords:
- 存储筛选器驱动程序 WDK
- 筛选器驱动程序 WDK 存储
- 存储驱动程序 WDK，筛选器驱动程序
- SFD WDK 存储
ms.date: 12/15/2019
ms.localizationpriority: medium
ms.openlocfilehash: 688786b6f42ba6c23a899ad204bf2ce1940bedda
ms.sourcegitcommit: e1ff1dd43b87dfb7349cebf70ed2878dc8d7c794
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/02/2020
ms.locfileid: "75606557"
---
# <a name="introduction-to-storage-filter-drivers"></a>存储筛选器驱动程序简介

存储筛选器驱动程序支持系统提供的存储类驱动程序未提供的特定于设备的功能。

本部分包含以下信息：

[存储筛选器驱动程序对 i/o 请求的支持](storage-filter-driver-s-support-of-i-o-requests.md)

[存储筛选器驱动程序的设备类型特定功能](storage-filter-driver-s-device-type-specific-functionality.md)

[存储筛选器驱动程序的 DriverEntry 例程](storage-filter-driver-s-driverentry-routine.md)

[存储筛选器驱动程序的 AddDevice 例程](storage-filter-driver-s-adddevice-routine.md)

[处理存储筛选器驱动程序中的 PnP 启动](handling-pnp-start-in-a-storage-filter-driver.md)

[存储筛选器驱动程序的调度例程](storage-filter-driver-s-dispatch-routines.md)

[存储筛选器驱动程序的 IoCompletion 例程](storage-filter-driver-s-iocompletion-routines.md)

[处理 PnP 寻呼请求](handling-pnp-paging-requests.md)

如果特定设备类型的存储类驱动程序已存在，则可能不需要为相同类型的新设备编写驱动程序。 每个系统提供的存储类驱动程序都设计为支持给定类型的外围设备，并针对多个供应商的设备进行测试。 因此，任何系统提供的存储类驱动程序都可能为其类型需要的另一个设备提供支持。

如果现有的存储类驱动程序不能完全支持其类型的新设备，则可以将新的驱动程序作为存储筛选器驱动程序（SFD），以分层方式在现有系统提供的类驱动程序上进行编写。 SFD 可能会转换读/写请求中的数据、定义额外的 i/o 控制代码（IOCTLs），使用户应用程序能够利用特定设备的其他功能，或解决特定于设备的问题，而无需对泛型类或端口驱动程序进行特定于硬件的更改。

除非新设备要求每个请求以设备特定的方式进行处理，否则，可以在比新的存储类驱动程序更少的时间内开发存储筛选器驱动程序。
