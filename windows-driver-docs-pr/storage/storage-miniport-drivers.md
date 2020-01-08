---
title: 存储微型端口驱动程序简介
description: 存储器微型端口驱动程序
ms.assetid: 374d8370-02a9-43ab-ab47-27fa9f4051ea
keywords:
- 存储微型端口驱动程序 WDK
- 微型端口驱动程序 WDK 存储
- 存储驱动程序 WDK，微型端口驱动程序
ms.date: 12/15/2019
ms.localizationpriority: medium
ms.openlocfilehash: 5814bf08d138040ae5ea7ee7629dcde825be058d
ms.sourcegitcommit: e1ff1dd43b87dfb7349cebf70ed2878dc8d7c794
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/02/2020
ms.locfileid: "75606551"
---
# <a name="introduction-to-storage-miniport-drivers"></a>存储微型端口驱动程序简介

供应商提供的存储微型端口驱动程序与系统提供的存储端口驱动程序一起工作，以支持 Windows 上的供应商存储设备。 这些模块之间的通信如下所示：

- 小型端口调用一组存储端口驱动程序提供的支持例程

- 小型端口实现了一组标准例程，用于调用它的存储端口驱动程序，一些是必需的，一些是可选的

SCSI 端口驱动程序、Storport 驱动程序和 ATA 端口驱动程序调用的微型端口驱动程序例程非常类似。

下表列出了存储微型端口驱动程序的类型及其关联的系统提供的端口驱动程序支持库：

| 微型端口驱动程序 | 端口驱动程序 |
| --------------- | ----------- |
| [Storport 微型端口驱动程序](storport-miniport-drivers.md) | [Storport 驱动程序](storport-driver-overview.md)（*storport*），在 Windows Server 2003 和更高版本的操作系统中可用（建议） |
| [SCSI 微型端口驱动程序](scsi-miniport-drivers.md) | [SCSI 端口驱动程序](scsi-port-driver-overview.md)（*Scsiport*） |
| [ATA 微型端口驱动程序](ata-miniport-drivers.md) | [ATA 端口驱动程序](ata-port-driver-overview.md)（*Ataport*），在 Windows Vista 和更高版本的操作系统中可用 |
| [IDE 控制器微型驱动程序](requirements-for-vendor-supplied-ide-controller-minidrivers.md) | 请参阅[IDE 端口驱动程序](ide-port-driver.md) |

存储小型端口驱动程序的最佳做法是避免调用操作系统例程，而不是由适当的端口驱动程序支持提供的支持例程。 例如，存储微型端口驱动程序不应调用[**KeQuerySystemTime**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kequerysystemtime)。 相反，微型端口驱动程序应调用[**ScsiPortQuerySystemTime**](https://docs.microsoft.com/windows-hardware/drivers/ddi/srb/nf-srb-scsiportquerysystemtime)或[**StorPortQuerySystemTime**](https://docs.microsoft.com/windows-hardware/drivers/ddi/storport/nf-storport-storportquerysystemtime)这样的例程。 存储微型端口驱动程序不应调用[**MmGetPhysicalAddress**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-mmgetphysicaladdress)。 相反，微型端口驱动程序应调用[**ScsiPortGetPhysicalAddress**](https://docs.microsoft.com/windows-hardware/drivers/ddi/srb/nf-srb-scsiportgetphysicaladdress)和[**StorPortGetPhysicalAddress**](https://docs.microsoft.com/windows-hardware/drivers/ddi/storport/nf-storport-storportgetphysicaladdress)之类的例程。

不要在微型端口驱动程序中使用[硬件抽象层例程](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff546644(v=vs.85))。
