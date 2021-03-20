---
title: 关于存储微型端口驱动程序
description: 存储器微型端口驱动程序
keywords:
- 存储微型端口驱动程序 WDK
- 微型端口驱动程序 WDK 存储
- 存储驱动程序 WDK，微型端口驱动程序
ms.date: 03/16/2021
ms.localizationpriority: medium
ms.openlocfilehash: 81185171ff4878f7e3e6c58a61f143bbdde67bb9
ms.sourcegitcommit: 76a7b604f13cf419ff21518337913820a703347f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/20/2021
ms.locfileid: "104719548"
---
# <a name="about-storage-miniport-drivers"></a>关于存储微型端口驱动程序

供应商提供的存储微型端口驱动程序与系统提供的存储端口驱动程序 [一起工作](communicating-with-a-storage-port-driver.md) ，以支持 Windows 上的供应商存储设备。

下表列出了存储微型端口驱动程序的类型及其关联的系统提供的端口驱动程序支持库：

| 微型端口驱动程序 | 端口驱动程序 |
| --------------- | ----------- |
| [Storport 微型端口驱动程序](storport-miniport-drivers.md) | [Storport 驱动程序](storport-driver-overview.md) (*Storport.sys*) ，在 Windows Server 2003 和更高版本的操作系统中可用 (建议使用)  |
| [SCSI 微型端口驱动程序](scsi-miniport-drivers.md) | [SCSI 端口驱动程序](scsi-port-driver-overview.md) (*Scsiport.sys*)  |
| [ATA 微型端口驱动程序](ata-miniport-drivers.md) | [ATA 端口驱动程序](ata-port-driver-overview.md) (*Ataport.sys*) ，在 Windows Vista 和更高版本的操作系统中可用 |
| [IDE 控制器微型驱动程序](requirements-for-vendor-supplied-ide-controller-minidrivers.md) | 请参阅 [IDE 端口驱动程序](ide-port-driver.md) |
