---
title: 关于存储驱动程序
description: 存储驱动程序
ms.assetid: 5512a8f1-20ad-4b78-a60e-7418ac7f2117
keywords:
- 存储驱动程序 WDK
ms.date: 10/08/2019
ms.localizationpriority: medium
ms.openlocfilehash: bb02e9e0b15ac35ce812b253ce6e2f0ab4dea15e
ms.sourcegitcommit: e1ff1dd43b87dfb7349cebf70ed2878dc8d7c794
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/02/2020
ms.locfileid: "75606471"
---
# <a name="about-storage-drivers"></a>关于存储驱动程序

此部分存储驱动程序设计指南包含以下信息：

[存储驱动程序体系结构](storage-driver-architecture.md)

[存储驱动程序和设备对象](storage-drivers-and-device-objects.md)

[存储驱动程序的系统头文件](system-header-files-for-storage-drivers.md)

[对存储驱动程序中的可分页代码的限制](restrictions-on-pageable-code-in-storage-drivers.md)

[查询写入缓存属性](querying-for-the-write-cache-property.md)

[用于存储设备的设备唯一标识符（Duid）](device-unique-identifiers--duids--for-storage-devices.md)

[常规存储 i/o 控制代码](general-storage-io-control-codes.md)

后续部分包含用于设计以下类型的 Windows 内核模式存储驱动程序的准则：

- 特定于供应商的 SCSI HBA 的与操作系统无关的微型端口驱动程序（请参阅[SCSI 微型端口驱动](scsi-miniport-drivers.md)程序）

- 用于非 SCSI 存储适配器的微型端口驱动程序（请参阅[SCSI 微型端口驱动程序](scsi-miniport-drivers.md)）

- 适用于一种新型外设设备的类驱动程序（请参阅[存储类驱动程序](introduction-to-storage-class-drivers.md)）

- 特定于供应商的磁带设备的独立于操作系统的磁带 miniclass 驱动程序（请参阅[磁带驱动程序](tape-drivers-overview.md)）

- 针对特定于供应商的媒体转换器设备的转换器 miniclass 驱动程序（请参阅[更换器驱动](changer-drivers.md)程序）

- 已具有类驱动程序的类型的外围设备的筛选器驱动程序（请参阅[存储筛选器驱动](storage-filter-drivers.md)程序）
