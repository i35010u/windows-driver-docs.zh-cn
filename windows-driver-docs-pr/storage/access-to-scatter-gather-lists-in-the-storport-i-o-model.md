---
title: 访问 Storport I/O 模型中的分散/聚合列表
description: 访问 Storport I/O 模型中的分散/聚合列表
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 27cbce08d974d9f56a34904d4ad9399145f9390e
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96804813"
---
# <a name="access-to-scattergather-lists-in-the-storport-io-model"></a>访问 Storport I/O 模型中的分散/聚合列表


## <span id="ddk_access_to_scatter_gather_lists_in_the_storport_i_o_model_kg"></span><span id="DDK_ACCESS_TO_SCATTER_GATHER_LISTS_IN_THE_STORPORT_I_O_MODEL_KG"></span>


SCSI 端口驱动程序对一组散播/聚集列表结构具有完全访问权限，用于定义 SRB 的内存范围和物理地址。 但是，与 SCSI 端口驱动程序配合使用的微型端口驱动程序不是。 SCSI 端口 i/o 模型强制微型端口驱动程序通过对 [**ScsiPortGetPhysicalAddress**](/windows-hardware/drivers/ddi/srb/nf-srb-scsiportgetphysicaladdress) 例程的重复调用，手动发现并构建自己的分散/收集列表。

Storport i/o 模型提供了其微型端口驱动程序，可直接访问系统的散播/聚集列表结构，从而减少了微型端口驱动程序为端口驱动程序支持例程构建专用散播/聚集列表所需的调用次数。

[**StorPortGetScatterGatherList**](/windows-hardware/drivers/ddi/storport/nf-storport-storportgetscattergatherlist)返回的散点/集合列表仅在 SRB 完成后才有效。

微型端口驱动程序不必释放 **StorPortGetScatterGatherList** 返回的散点/集合列表的内存。

微型端口驱动程序应在微型端口驱动程序的 [**HwStorBuildIo**](/windows-hardware/drivers/ddi/storport/nc-storport-hw_buildio) 例程中执行由 Storport 提供的散播/list 列表的任何必要的转换，并将其转换为特定于微型端口驱动程序的格式。

 

