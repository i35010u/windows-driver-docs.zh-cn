---
title: 访问 Storport I/O 模型中的分散/聚合列表
description: 访问 Storport I/O 模型中的分散/聚合列表
ms.assetid: db05ac58-3317-44b2-9550-e4520537955f
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8cfcad79729c6b80383fd70c8983e496e3781c8d
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386300"
---
# <a name="access-to-scattergather-lists-in-the-storport-io-model"></a>访问 Storport I/O 模型中的分散/聚合列表


## <span id="ddk_access_to_scatter_gather_lists_in_the_storport_i_o_model_kg"></span><span id="DDK_ACCESS_TO_SCATTER_GATHER_LISTS_IN_THE_STORPORT_I_O_MODEL_KG"></span>


SCSI 端口驱动程序具有一组定义的内存范围的分散/聚拢列表结构和 SRB 的物理地址的完全访问权限。 但是，使用 SCSI 端口驱动程序的微型端口驱动程序不这样做。 SCSI 端口 I/O 模型强制微型端口驱动程序来手动发现并建立通过重复调用其自身散播-聚集列表[ **ScsiPortGetPhysicalAddress** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/srb/nf-srb-scsiportgetphysicaladdress)例程。

Storport I/O 模型提供了直接访问系统的分散/聚拢列表结构，减少的微型端口驱动程序必须设置为端口驱动程序支持例程以生成其私有散播-聚集列表的调用次数的微型端口驱动程序。

散播-聚集列出[ **StorPortGetScatterGatherList** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/nf-storport-storportgetscattergatherlist)仅直到 SRB 完成时返回都有效。

微型端口驱动程序不需要释放的内存的分散/集中列出**StorPortGetScatterGatherList**返回。

微型端口驱动程序应执行散播-聚集列表 Storport 微型端口驱动程序中的微型端口驱动程序特定格式向提供的所有必需的转换[ **HwStorBuildIo** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/nc-storport-hw_buildio)例程。

 

 




