---
title: 访问 Storport I/O 模型中的分散/聚合列表
description: 访问 Storport I/O 模型中的分散/聚合列表
ms.assetid: db05ac58-3317-44b2-9550-e4520537955f
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bfb2869588ac800e24bf7262c194d6169dc6f2e8
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845540"
---
# <a name="access-to-scattergather-lists-in-the-storport-io-model"></a>访问 Storport I/O 模型中的分散/聚合列表


## <span id="ddk_access_to_scatter_gather_lists_in_the_storport_i_o_model_kg"></span><span id="DDK_ACCESS_TO_SCATTER_GATHER_LISTS_IN_THE_STORPORT_I_O_MODEL_KG"></span>


SCSI 端口驱动程序对一组散播/聚集列表结构具有完全访问权限，用于定义 SRB 的内存范围和物理地址。 但是，与 SCSI 端口驱动程序配合使用的微型端口驱动程序不是。 SCSI 端口 i/o 模型强制微型端口驱动程序通过对[**ScsiPortGetPhysicalAddress**](https://docs.microsoft.com/windows-hardware/drivers/ddi/srb/nf-srb-scsiportgetphysicaladdress)例程的重复调用，手动发现并构建自己的分散/收集列表。

Storport i/o 模型提供了其微型端口驱动程序，可直接访问系统的散播/聚集列表结构，从而减少了微型端口驱动程序为端口驱动程序支持例程构建专用散播/聚集列表所需的调用次数。

[**StorPortGetScatterGatherList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/storport/nf-storport-storportgetscattergatherlist)返回的散点/集合列表仅在 SRB 完成后才有效。

微型端口驱动程序不必释放**StorPortGetScatterGatherList**返回的散点/集合列表的内存。

微型端口驱动程序应在微型端口驱动程序的[**HwStorBuildIo**](https://docs.microsoft.com/windows-hardware/drivers/ddi/storport/nc-storport-hw_buildio)例程中执行由 Storport 提供的散播/list 列表的任何必要的转换，并将其转换为特定于微型端口驱动程序的格式。

 

 




