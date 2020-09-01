---
title: 存储端口驱动程序简介
description: 存储端口驱动程序
ms.assetid: 5ff4916c-7d1f-4b61-a332-6ed89df9db56
keywords:
- 存储端口驱动程序 WDK
- 存储端口驱动程序 WDK，关于存储端口驱动程序
- 端口驱动程序 WDK 存储
ms.date: 12/15/2019
ms.localizationpriority: medium
ms.openlocfilehash: eb894a7dc857a7d774908f365b06c78f7972306e
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89189431"
---
# <a name="introduction-to-storage-port-drivers"></a>存储端口驱动程序简介

Microsoft Windows 包含三个系统提供的存储端口驱动程序：

- [Storport 驱动程序](storport-driver-overview.md) (*Storport.sys*) ，在 Windows Server 2003 和更高版本的操作系统中可用 (建议使用) 

- [SCSI 端口驱动程序](scsi-port-driver-overview.md) (*Scsiport.sys*) 

- [ATA 端口驱动程序](ata-port-driver-overview.md) (*Ataport.sys*) ，在 Windows Vista 和更高版本的操作系统中可用

Storport 驱动程序比 SCSI 端口更有效、性能更高。 因此，应尽可能地开发与 Storport 驱动程序配合使用的微型端口驱动程序。 尤其重要的是，将 Storport 用于高性能设备，例如基于主机的 RAID 和光纤通道适配器。 Storport 不能用于不支持即插即用 (PnP) 或必须使用系统 DMA 的适配器或设备。 有关使用 Storport 驱动程序的详细限制列表，请参阅对 [适配器使用 storport 的要求](requirements-for-using-storport-with-an-adapter.md)。

ATA 端口驱动程序从基于 SCSI 的协议中防护 ATA 微型端口驱动程序，端口驱动程序使用该协议与较高级别的驱动程序（如存储类驱动程序）进行通信。 例如，连接到 SCSI 端口或 Storport 的微型端口驱动程序必须向端口驱动程序提供 SCSI 识别数据。 这不是 ATA 微型端口驱动程序所必需的。 ATA 端口驱动程序使用 ATA 命令从 ATA 微型端口驱动程序收集必要的数据，对数据进行组织，使其符合 SCSI 感知数据格式，并将数据传递到更高级别的驱动程序，就像它是 SCSI 感知数据一样。 ATA 端口驱动程序还会将其从更高级别的驱动程序接收的每个 [SCSI_REQUEST_BLOCK](/windows-hardware/drivers/ddi/srb/ns-srb-_scsi_request_block) 转换为基于 ATA 的等效项（称为 [IDE_REQUEST_BLOCK](/windows-hardware/drivers/ddi/irb/ns-irb-_ide_request_block)）。

每个端口驱动程序与一组供应商提供的存储微型端口驱动程序通信，并为微型端口驱动程序调用提供一组支持例程。 每个端口驱动程序通过调用每个存储微型端口驱动程序必须实现的一组标准例程，与其微型端口驱动程序通信。 SCSI 端口驱动程序、Storport 驱动程序和 ATA 端口驱动程序调用的微型端口驱动程序例程非常类似。 可在以下部分中找到端口驱动程序支持例程和微型端口驱动程序例程的列表：

| 端口驱动程序 | 支持例程 | 微型端口驱动程序例程 |
| ----------- | ---------------- | ------------------------ |
| Storport 驱动程序 | [Storport 驱动程序支持例程](storport-driver-support-routines.md) | [Storport 驱动程序微型端口例程](storport-miniport-driver-routines.md) |
| SCSI 端口驱动程序 | [SCSI 端口驱动程序支持例程](scsi-port-driver-support-routines.md) | [SCSI 微型端口驱动程序例程](scsi-miniport-driver-routines.md) |
| ATA 端口驱动程序 | [ATA 端口驱动程序支持例程](ata-miniport-drivers.md) | [ATA 微型端口驱动程序例程](ata-miniport-drivers.md) |

如果希望在客户端 Windows 产品上或在早于 Windows Server 2003 的服务器产品上支持存储设备，则必须提供 SCSI 端口微型端口驱动程序。

如果希望在 Windows Server 2003 和更高版本的服务器产品系列上支持存储设备，可以提供 Storport 微型端口驱动程序或 SCSI 微型端口驱动程序。 如果要在 Windows Vista 和更高版本的操作系统中安装 ATA 存储设备，则必须提供 ATA 端口微型端口驱动程序。

以下各节介绍了 Storport、SCSI 端口和 ATA 端口驱动程序以及它们之间的区别。