---
title: 创建分配时指定段
description: 创建分配时指定段
ms.assetid: 31bfbfd9-89e5-42fe-90bc-8ff54bac4f8b
keywords:
- 内存段 WDK 显示，分配创建
- 分配 WDK 显示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 86fdda890a99b56d812a02a0c2431b1668debe7f
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72829443"
---
# <a name="specifying-segments-when-creating-allocations"></a>创建分配时指定段


## <span id="ddk_specifying_segments_for_creating_and_rendering_allocations_gg"></span><span id="DDK_SPECIFYING_SEGMENTS_FOR_CREATING_AND_RENDERING_ALLOCATIONS_GG"></span>


显示微型端口驱动程序指定并返回在视频内存管理器调用驱动程序的[**DxgkDdiCreateAllocation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_createallocation)函数时，它更倾向于视频内存管理器使用的内存段的相关信息。 在对*DxgkDdiCreateAllocation*的调用中，驱动程序将创建视频资源的分配。 驱动程序将返回[**DXGK\_ALLOCATIONINFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_allocationinfo)结构中用于描述分配的受支持段和段首选项的标识符。

在返回的段信息中，视频内存管理器会确定要为给定操作分页的内存段。

 

 





