---
title: 存储器微型端口驱动程序
description: 存储器微型端口驱动程序
ms.assetid: 374d8370-02a9-43ab-ab47-27fa9f4051ea
keywords:
- 存储微型端口驱动程序 WDK
- 微型端口驱动程序 WDK 存储
- 存储驱动程序 WDK，微型端口驱动程序
ms.date: 10/08/2019
ms.localizationpriority: medium
ms.openlocfilehash: bd8ec22ccf78f1ae947dfcb0fb98fa81f64e7ae8
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844466"
---
# <a name="storage-miniport-drivers"></a>存储器微型端口驱动程序

本部分包含以下主题：

[SCSI 微型端口驱动程序](scsi-miniport-drivers.md)

[Storport 微型端口驱动程序](storport-miniport-drivers.md)

[IDE 控制器微型驱动程序](ide-controller-minidrivers.md)

[ATA 微型端口驱动程序](ata-miniport-drivers.md)

存储小型端口驱动程序的最佳做法是避免调用操作系统例程，而不是由适当的端口驱动程序支持提供的支持例程。 例如，存储微型端口驱动程序不应调用[**KeQuerySystemTime**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kequerysystemtime)。 相反，微型端口驱动程序应调用[**ScsiPortQuerySystemTime**](https://docs.microsoft.com/windows-hardware/drivers/ddi/srb/nf-srb-scsiportquerysystemtime)或[**StorPortQuerySystemTime**](https://docs.microsoft.com/windows-hardware/drivers/ddi/storport/nf-storport-storportquerysystemtime)这样的例程。 存储微型端口驱动程序不应调用[**MmGetPhysicalAddress**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-mmgetphysicaladdress)。 相反，微型端口驱动程序应调用[**ScsiPortGetPhysicalAddress**](https://docs.microsoft.com/windows-hardware/drivers/ddi/srb/nf-srb-scsiportgetphysicaladdress)和[**StorPortGetPhysicalAddress**](https://docs.microsoft.com/windows-hardware/drivers/ddi/storport/nf-storport-storportgetphysicaladdress)之类的例程。

不要在微型端口驱动程序中使用[硬件抽象层例程](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff546644(v=vs.85))。

以下列表说明了系统提供的、每种类型的存储微型端口驱动程序应使用的端口驱动程序支持库：

| 微型端口驱动程序 | 端口驱动程序 |
| --------------- | ----------- |
| Storport 微型端口驱动程序  | [Storport 驱动程序](storport-driver-overview.md)（*storport*），在 Windows Server 2003 和更高版本的操作系统中可用（建议） |
| SCSI 端口微型端口驱动程序 | [SCSI 端口驱动程序](scsi-port-driver-overview.md)（*Scsiport*） |
| ATA 端口微型端口驱动程序  | [ATA 端口驱动程序](ata-port-driver-overview.md)（*Ataport*），在 Windows Vista 和更高版本的操作系统中可用 |
| IDE 微型端口驱动程序       | 请参阅[IDE 端口驱动程序](ide-port-driver.md) |
