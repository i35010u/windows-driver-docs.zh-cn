---
title: ATA 端口的可以与存储类驱动程序交互的接口
description: ATA 端口的可以与存储类驱动程序交互的接口
ms.assetid: 6b22bbb1-f14e-48d9-a00c-c7eae79a078f
keywords:
- ATA 端口驱动程序 WDK、 存储类驱动程序
- 存储类驱动程序 WDK，ATA 端口驱动程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6b5c5f2e58de1865516ace85762552c4473cd6a4
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67368371"
---
# <a name="ata-ports-interface-with-the-storage-class-driver"></a>ATA 端口的可以与存储类驱动程序交互的接口


## <span id="ddk_ata_ports_interface_with_the_storage_class_driver_kg"></span><span id="DDK_ATA_PORTS_INTERFACE_WITH_THE_STORAGE_CLASS_DRIVER_KG"></span>

**请注意**ATA 端口驱动程序和 ATA 微型端口驱动程序模型可能被修改或不可用在将来。 相反，我们建议使用[Storport 驱动程序](https://docs.microsoft.com/windows-hardware/drivers/storage/storport-driver)并[Storport 微型端口](https://docs.microsoft.com/windows-hardware/drivers/storage/storport-miniport-drivers)驱动程序模型。



ATA 端口驱动程序、 SCSI 端口驱动程序和 Storport 驱动程序都使用 Srb 与更高级别的驱动程序，例如存储类驱动程序进行通信。 有关存储类和存储端口驱动程序之间的接口的详细信息，请参阅[SCSI 端口的存储类驱动程序接口](scsi-port-s-interface-with-the-storage-class-driver.md)。

 

 


