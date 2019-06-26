---
title: 创建分配时指定段
description: 创建分配时指定段
ms.assetid: 31bfbfd9-89e5-42fe-90bc-8ff54bac4f8b
keywords:
- 内存段 WDK 显示，分配创建
- 分配 WDK 显示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 56c7362a14741ba4ca5a7dce396a2fddedf6d915
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67376061"
---
# <a name="specifying-segments-when-creating-allocations"></a>创建分配时指定段


## <span id="ddk_specifying_segments_for_creating_and_rendering_allocations_gg"></span><span id="DDK_SPECIFYING_SEGMENTS_FOR_CREATING_AND_RENDERING_ALLOCATIONS_GG"></span>


指定显示微型端口驱动程序，并返回它时视频内存管理器会调用驱动程序的首选视频内存管理器使用有关其内存段的信息[ **DxgkDdiCreateAllocation** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_createallocation)函数。 在调用*DxgkDdiCreateAllocation*，驱动程序创建的视频资源分配。 该驱动程序返回的受支持的段和段中的首选项标识符[ **DXGK\_ALLOCATIONINFO** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_dxgk_allocationinfo)描述了分配的结构。

从返回的段信息的视频内存管理器确定要为给定操作的页面中的相应的内存段。

 

 





