---
title: 存储驱动程序
description: 存储驱动程序
ms.assetid: 5512a8f1-20ad-4b78-a60e-7418ac7f2117
keywords:
- 存储驱动程序 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 200e26dfc878ab56ddfdf84dd776b82a538ce4f5
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63331704"
---
# <a name="storage-drivers"></a>存储驱动程序


## <span id="ddk_storage_drivers_kg"></span><span id="DDK_STORAGE_DRIVERS_KG"></span>


本部分包含以下信息：

[存储驱动程序体系结构](storage-driver-architecture.md)

[存储驱动程序和设备对象](storage-drivers-and-device-objects.md)

[存储驱动程序的系统标头文件](system-header-files-for-storage-drivers.md)

[对存储驱动程序中的可分页代码的限制](restrictions-on-pageable-code-in-storage-drivers.md)

[查询的写缓存属性](querying-for-the-write-cache-property.md)

[设备的存储设备 (Duid) 的唯一标识符](device-unique-identifiers--duids--for-storage-devices.md)

后续各节包含的设计以下类型的 Windows 内核模式存储驱动程序：

-   特定于供应商 SCSI HBA 的独立于操作系统的微型端口驱动程序 (请参阅[SCSI 微型端口驱动程序](scsi-miniport-drivers.md))

-   非 SCSI 存储适配器的微型端口驱动程序 (请参阅[SCSI 微型端口驱动程序](scsi-miniport-drivers.md))

-   一种新型的外围设备的类驱动程序 (请参阅[存储类驱动程序](storage-class-drivers.md))

-   特定于供应商的磁带设备的独立于操作系统的磁带 miniclass 驱动程序 (请参阅[磁带驱动程序](tape-drivers.md))

-   特定于供应商的媒体更换器设备的转换器 miniclass 驱动程序 (请参阅[更换器驱动程序](changer-drivers.md))

-   外围设备已类驱动程序的类型的筛选器驱动程序 (请参阅[存储筛选器驱动程序](storage-filter-drivers.md))

 

 




