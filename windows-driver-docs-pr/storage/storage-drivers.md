---
title: 关于存储驱动程序
description: 存储驱动程序
keywords:
- 存储驱动程序 WDK
ms.date: 10/08/2019
ms.localizationpriority: medium
ms.openlocfilehash: c66c37c8311f90c2edb196b1d85e20590a6a506b
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96799305"
---
# <a name="about-storage-drivers"></a>关于存储驱动程序

此部分存储驱动程序设计指南包含以下信息：

[存储驱动程序体系结构](storage-driver-architecture.md)

[存储驱动程序和设备对象](storage-drivers-and-device-objects.md)

[存储驱动程序的系统标头文件](system-header-files-for-storage-drivers.md)

[对存储驱动程序中的可分页代码的限制](restrictions-on-pageable-code-in-storage-drivers.md)

[查询写缓存属性](querying-for-the-write-cache-property.md)

[用于存储设备的设备唯一标识符 (Duid) ](device-unique-identifiers--duids--for-storage-devices.md)

[常规存储 I/O 控制代码](general-storage-io-control-codes.md)

后续部分包含用于设计以下类型的 Windows 内核模式存储驱动程序的准则：

- 特定于供应商的 SCSI HBA 的与操作系统无关的微型端口驱动程序 (参阅 [SCSI 微型端口驱动程序](scsi-miniport-drivers.md)) 

- 非 SCSI 存储适配器的微型端口驱动程序 (参阅 [SCSI 微型端口驱动程序](scsi-miniport-drivers.md)) 

- 一种新型外设设备的类驱动程序 (参阅 [存储类驱动程序](introduction-to-storage-class-drivers.md)) 

- 特定于供应商的磁带设备的独立于操作系统的磁带 miniclass 驱动程序 (参阅 [磁带驱动程序](tape-drivers-overview.md)) 

- 用于特定于供应商的媒体转换器设备的 miniclass driver 驱动程序 (参阅 [更换器驱动](changer-drivers.md) 程序) 

- 某个类型的外围设备的筛选器驱动程序已具有类驱动程序 (参阅 [存储筛选器驱动程序](storage-filter-drivers.md)) 
