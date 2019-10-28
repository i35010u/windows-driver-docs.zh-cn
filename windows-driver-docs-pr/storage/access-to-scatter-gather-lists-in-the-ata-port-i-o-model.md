---
title: 访问 ATA 端口 I/O 模型中的分散/聚合列表
description: 访问 ATA 端口 I/O 模型中的分散/聚合列表
ms.assetid: 56221602-9588-47f2-acd9-a11bd5ce02d9
keywords:
- ATA 端口驱动程序 WDK、散点/收集列表
- 散点/集合列表 WDK ATA 端口驱动程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: be39e32b5330735f90c0546530a19c64c6253ce8
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839617"
---
# <a name="access-to-scattergather-lists-in-the-ata-port-io-model"></a>访问 ATA 端口 I/O 模型中的分散/聚合列表


## <span id="ddk_access_to_scatter_gather_lists_in_the_ata_port_i_o_model_kg"></span><span id="DDK_ACCESS_TO_SCATTER_GATHER_LISTS_IN_THE_ATA_PORT_I_O_MODEL_KG"></span>

**注意**ATA 端口驱动程序和 ATA 微型端口驱动程序模型可能会在将来更改或不可用。 相反，我们建议使用[storport 驱动](https://docs.microsoft.com/windows-hardware/drivers/storage/storport-driver)程序和[storport 微型端口](https://docs.microsoft.com/windows-hardware/drivers/storage/storport-miniport-drivers)驱动程序模型。



[ATA 端口 I/o 模型](ata-port-i-o-model.md)（如[Storport i/o 模型](storport-i-o-model.md)）提供了其可直接访问系统的散播/聚集列表结构的微型端口驱动程序。 这种直接访问可以减少微型端口驱动程序为端口驱动程序支持例程构建专用散播/聚集列表而必须进行的调用数。

另一方面，SCSI 端口 i/o 模型强制使用微型端口驱动程序，通过对[**ScsiPortGetPhysicalAddress**](https://docs.microsoft.com/windows-hardware/drivers/ddi/srb/nf-srb-scsiportgetphysicaladdress)例程的重复调用，手动发现并构建自己的分散/收集列表。

ATA 端口微型端口驱动程序可以使用[**AtaPortGetScatterGatherList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/irb/nf-irb-ataportgetscattergatherlist)例程直接访问系统的散播/聚集列表。 **AtaPortGetScatterGatherList**返回的散点/集合列表仅在 IRB 完成后才有效。

微型端口驱动程序不必释放**AtaPortGetScatterGatherList**返回的散点/集合列表的内存。

如果需要，微型端口驱动程序的[**IdeHwBuildIo**](https://docs.microsoft.com/windows-hardware/drivers/ddi/irb/nc-irb-ide_hw_buildio)例程应转换散点/集合列表。

 

 


