---
title: ATA 端口驱动程序
description: ATA 端口驱动程序
ms.assetid: c7b9d794-a8cb-4bdd-bb93-bff473ea26a7
keywords:
- 存储端口驱动程序 WDK，ATA 端口驱动程序
- ATA 端口驱动程序 WDK
- ATA 端口驱动程序 WDK，有关 ATA 端口驱动程序
- IDE 控制器 WDK ATA 端口驱动程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e644b187f6c5be9626e852907f220adedc2e230d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63380127"
---
# <a name="ata-port-driver"></a>ATA 端口驱动程序


## <span id="ddk_ata_port_driver_kg"></span><span id="DDK_ATA_PORT_DRIVER_KG"></span>


**请注意**ATA 端口驱动程序和 ATA 微型端口驱动程序模型可能被修改或不可用在将来。 相反，我们建议使用[Storport 驱动程序](https://msdn.microsoft.com/windows/hardware/drivers/storage/storport-driver)并[Storport 微型端口](https://msdn.microsoft.com/windows/hardware/drivers/storage/storport-miniport-drivers)驱动程序模型。


除了[SCSI 端口驱动程序](scsi-port-driver.md)并[Storport 驱动程序](storport-driver.md)，Windows Vista 和更高版本的 Windows 操作系统提供了 ATA 端口驱动程序 (*Ataport.sys*)，尤其适合与 IDE 控制器一起使用的存储端口驱动程序。

ATA 端口驱动程序和其他系统提供的存储端口驱动程序之间最明显的差别是 ATA 端口驱动程序使用与其他驱动程序进行通信的协议。 所有其他系统提供的存储端口驱动程序使用 SCSI 请求块 (Srb) 进行通信都具有更高级别的驱动程序，例如存储类驱动程序，并与微型端口驱动程序。 ATA 端口驱动程序使用 Srb 与仅限更高级别的驱动程序进行通信。 与进行通信的微型端口驱动程序，ATA 端口使用名为的 IDE 请求块 (IRB) 定义的数据包[ **IDE\_请求\_块**](https://msdn.microsoft.com/library/windows/hardware/ff559140)结构。 IRBs 是更好地设计比 Srb ATA 设备的特征。

ATA 端口驱动程序和其他系统提供的存储驱动程序的另一个区别是 ATA 端口驱动程序为屏蔽 ATA 微型端口驱动程序从由 SCSI 标准定义某些要求。 例如，ATA 端口驱动程序使用 ATA 命令从 ATA 微型端口驱动程序收集 SCSI 检测数据的等效项，将数据转换，使其符合 SCSI 检测数据格式，并将数据传递到更高级别的驱动程序，就好像 SCSI 检测数据。 因此，ATA 微型端口驱动程序不需要响应来自 SCSI 检测数据的更高级别的驱动程序直接的请求。

ATA 微型端口驱动程序接口与 SCSI 端口驱动程序接口非常相似。 因此，如果您已编写 SCSI 微型端口驱动程序，您应能够轻松地了解如何编写 ATA 微型端口驱动程序。 当前 ATA/ATAPI 技术，如串行 ATA (SATA) 的驱动程序应使用更高的性能 Storport 微型端口接口。

ATA 端口驱动程序，以及操作系统提供了默认的 ATA 微型端口驱动程序和默认控制器微型驱动程序。 系统提供的默认驱动程序适用于大多数控制器硬件，并且我们强烈建议尽可能使用默认微型驱动程序。

 

 


