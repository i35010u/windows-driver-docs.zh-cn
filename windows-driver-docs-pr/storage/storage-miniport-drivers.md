---
title: 存储器微型端口驱动程序
description: 存储器微型端口驱动程序
ms.assetid: 374d8370-02a9-43ab-ab47-27fa9f4051ea
keywords:
- 存储微型端口驱动程序 WDK
- 微型端口驱动程序 WDK 存储
- 存储驱动程序 WDK，微型端口驱动程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 990d1ca49e6082613eb196b9db64d986bda92072
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67368199"
---
# <a name="storage-miniport-drivers"></a>存储器微型端口驱动程序


## <span id="ddk_storage_miniport_drivers_kg"></span><span id="DDK_STORAGE_MINIPORT_DRIVERS_KG"></span>


本部分包含以下主题：

[SCSI 微型端口驱动程序](scsi-miniport-drivers.md)

[Storport 微型端口驱动程序](storport-miniport-drivers.md)

[IDE 控制器微型驱动程序](ide-controller-minidrivers.md)

[ATA 微型端口驱动程序](ata-miniport-drivers.md)

存储微型端口驱动程序的最佳做法是避免调用操作系统以外的端口驱动程序支持库提供的例程的例程。 例如，存储微型端口驱动程序不应调用[ **KeQuerySystemTime**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kequerysystemtime)。 相反，微型端口驱动程序应调用例程，如[ **ScsiPortQuerySystemTime** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/srb/nf-srb-scsiportquerysystemtime)或[ **StorPortQuerySystemTime**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/nf-storport-storportquerysystemtime)。 存储微型端口驱动程序不应调用[ **MmGetPhysicalAddress**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-mmgetphysicaladdress)。 相反，微型端口驱动程序应调用例程，如[ **ScsiPortGetPhysicalAddress** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/srb/nf-srb-scsiportgetphysicaladdress)并[ **StorPortGetPhysicalAddress**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/nf-storport-storportgetphysicaladdress)。

不要使用[硬件抽象层例程](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff546644(v=vs.85))微型端口驱动程序中。

下面的列表说明了每种类型的存储微型端口驱动程序应使用的端口驱动程序支持库：

-   SCSI 端口微型端口驱动程序：[SCSI 端口库例程](required-and-optional-scsi-miniport-driver-routines.md)

-   Storport 微型端口驱动程序：[Storport 驱动程序支持例程](storport-driver-support-routines.md)

-   IDE 微型端口驱动程序：[PciIdeX 库例程](ide-controller-minidrivers.md)

-   ATA 端口微型端口驱动程序：[ATA 端口库例程](ata-miniport-drivers.md)

 

 




