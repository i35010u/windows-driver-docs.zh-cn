---
title: 存储端口驱动程序
description: 存储端口驱动程序
ms.assetid: 5ff4916c-7d1f-4b61-a332-6ed89df9db56
keywords:
- 存储端口驱动程序 WDK
- 存储端口驱动程序 WDK，有关存储端口驱动程序
- 端口驱动程序 WDK 存储
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fcdb83e6478b72a3d6592f638ecaaf34de6ed3d7
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67368183"
---
# <a name="storage-port-drivers"></a>存储端口驱动程序


## <span id="ddk_storage_port_drivers_kg"></span><span id="DDK_STORAGE_PORT_DRIVERS_KG"></span>


Microsoft Windows 包含三个系统提供的存储端口驱动程序：

-   [SCSI 端口驱动程序](scsi-port-driver.md)(*Scsiport.sys*)

-   [Storport 驱动程序](storport-driver.md)(*Storport.sys*)、 Windows Server 2003 和更高版本的操作系统中可用

-   [ATA 端口驱动程序](ata-port-driver.md)(*Ataport.sys*)、 Windows Vista 和更高版本的操作系统中可用

Storport 驱动程序是比 SCSI 端口的更高效、 更高的性能驱动程序。 因此应该开发能够与 Storport 驱动程序应尽可能的微型端口驱动程序。 它是对高性能的设备，如基于主机的 RAID 和光纤通道适配器使用 Storport 尤其重要。 Storport 不能用于适配器或不支持即插即用 (PnP) 或必须使用系统 DMA 的设备。 Storport 驱动程序的使用限制的详细列表，请参阅[要求与适配器使用 Storport](requirements-for-using-storport-with-an-adapter.md)。

ATA 端口驱动程序为屏蔽的 ATA 微型端口驱动程序从端口驱动程序使用与更高级别的驱动程序，例如存储类驱动程序进行通信的基于 SCSI 的协议。 例如，附加到 SCSI 端口或 Storport 微型端口驱动程序必须提供 SCSI 端口驱动程序的检测数据。 这不是所需的 ATA 微型端口驱动程序。 ATA 端口驱动程序从 ATA 微型端口驱动程序通过使用 ATA 命令收集所需的数据，组织数据，以便符合为 SCSI 的检测数据格式，并将传递到更高级别的驱动程序的数据，就好像它是 SCSI 检测数据。 ATA 端口驱动程序还将为每个[ **SCSI\_请求\_阻止**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/srb/ns-srb-_scsi_request_block)它接收从更高级别的驱动程序为基于 ATA 的等效调用[**IDE\_请求\_阻止**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/irb/ns-irb-_ide_request_block)。

每个端口驱动程序供应商提供的存储微型端口驱动程序的一组与通信并向一组要调用的微型端口驱动程序的支持例程。 SCSI 端口驱动程序提供的支持例程中所述[SCSI 端口库例程](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)。 Storport 驱动程序提供的支持例程中所述[Storport 驱动程序支持例程](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)。 由 ATA 端口驱动程序提供的支持例程中所述[ATA 端口库例程](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)。

每个端口驱动程序通过调用的例程的每个存储微型端口驱动程序必须实现一组标准的微型端口驱动程序与进行通信。 SCSI 端口驱动程序、 Storport 驱动程序，以及 ATA 端口驱动程序由调用的微型端口驱动程序例程都非常类似于另一个。 这些例程的说明可在[SCSI 微型端口驱动程序例程](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)， [Storport 驱动程序微型端口例程](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)，并[ATA 微型端口驱动程序例程](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)分别.

如果你想存储设备必须早于 Windows Server 2003 支持客户端 Windows 产品，或服务器产品，您必须提供 SCSI 端口微型端口驱动程序。

如果你想存储设备，以支持在 Windows Server 2003 和更高版本的服务器产品系列，可以提供 SCSI 端口微型端口驱动程序或 Storport 微型端口驱动程序。 如果你想要在 Windows Vista 和更高版本的操作系统中安装 ATA 存储设备，则必须提供 ATA 端口微型端口驱动程序。

以下各节介绍 SCSI 端口、 Storport 和 ATA 端口驱动程序和它们之间的区别。

 

 




