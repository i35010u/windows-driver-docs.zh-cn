---
title: 访问 ATA 端口 I/O 模型中的分散/聚合列表
description: 访问 ATA 端口 I/O 模型中的分散/聚合列表
ms.assetid: 56221602-9588-47f2-acd9-a11bd5ce02d9
keywords:
- ATA 端口驱动程序 WDK，散播-聚集列表
- 散播-聚集列表 WDK ATA 端口驱动程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 566b9c12d871097b56e9fb5bf0a8fb927a9074a1
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386296"
---
# <a name="access-to-scattergather-lists-in-the-ata-port-io-model"></a>访问 ATA 端口 I/O 模型中的分散/聚合列表


## <span id="ddk_access_to_scatter_gather_lists_in_the_ata_port_i_o_model_kg"></span><span id="DDK_ACCESS_TO_SCATTER_GATHER_LISTS_IN_THE_ATA_PORT_I_O_MODEL_KG"></span>

**请注意**ATA 端口驱动程序和 ATA 微型端口驱动程序模型可能被修改或不可用在将来。 相反，我们建议使用[Storport 驱动程序](https://docs.microsoft.com/windows-hardware/drivers/storage/storport-driver)并[Storport 微型端口](https://docs.microsoft.com/windows-hardware/drivers/storage/storport-miniport-drivers)驱动程序模型。



[ATA 端口 I/O 模型](ata-port-i-o-model.md)，如[Storport I/O 模型](storport-i-o-model.md)，提供了直接访问系统的分散/聚拢列表结构的微型端口驱动程序。 这种直接访问可减少微型端口驱动程序必须向端口驱动程序支持例程来生成其私有散播-聚集列表的调用的次数。

另一方面，SCSI 端口 I/O 模型强制微型端口驱动程序来手动发现并建立通过重复调用其自身散播-聚集列表[ **ScsiPortGetPhysicalAddress** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/srb/nf-srb-scsiportgetphysicaladdress)例程。

ATA 端口微型端口驱动程序可以通过使用直接访问系统的分散/聚拢列表[ **AtaPortGetScatterGatherList** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/irb/nf-irb-ataportgetscattergatherlist)例程。 散播-聚集列出**AtaPortGetScatterGatherList**仅直到 IRB 完成时返回都有效。

微型端口驱动程序不需要释放的内存的分散/集中列出**AtaPortGetScatterGatherList**返回。

微型端口驱动程序[ **IdeHwBuildIo** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/irb/nc-irb-ide_hw_buildio)例程应转换散播-聚集列表中，如有必要。

 

 


