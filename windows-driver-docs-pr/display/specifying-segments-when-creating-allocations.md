---
title: 创建分配时指定段
description: 创建分配时指定段
ms.assetid: 31bfbfd9-89e5-42fe-90bc-8ff54bac4f8b
keywords:
- 内存段 WDK 显示，分配创建
- 分配 WDK 显示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2186ca0e2f57633fd8ad791e445ed9c9c69f3f1e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56522096"
---
# <a name="specifying-segments-when-creating-allocations"></a>创建分配时指定段


## <span id="ddk_specifying_segments_for_creating_and_rendering_allocations_gg"></span><span id="DDK_SPECIFYING_SEGMENTS_FOR_CREATING_AND_RENDERING_ALLOCATIONS_GG"></span>


指定显示微型端口驱动程序，并返回它时视频内存管理器会调用驱动程序的首选视频内存管理器使用有关其内存段的信息[ **DxgkDdiCreateAllocation** ](https://msdn.microsoft.com/library/windows/hardware/ff559606)函数。 在调用*DxgkDdiCreateAllocation*，驱动程序创建的视频资源分配。 该驱动程序返回的受支持的段和段中的首选项标识符[ **DXGK\_ALLOCATIONINFO** ](https://msdn.microsoft.com/library/windows/hardware/ff560960)描述了分配的结构。

从返回的段信息的视频内存管理器确定要为给定操作的页面中的相应的内存段。

 

 





