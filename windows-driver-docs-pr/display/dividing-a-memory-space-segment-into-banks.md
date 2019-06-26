---
title: 将内存空间段分割成内存库
description: 将内存空间段分割成内存库
ms.assetid: 7fdbe511-ae92-44c2-9651-51b3ead11425
keywords:
- 内存段 WDK 显示银行
- 存款的内存 WDK 显示
- 银行 WDK 显示
- 线性内存空间段 WDK 显示
- 内存段 WDK 显示线性的内存空间段
- 将 WDK 显示线性的内存空间段
- 内存空间段 WDK 显示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3267bd33f26eeda38ea3fded96ffb29ef4a97fcc
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67365739"
---
# <a name="dividing-a-memory-space-segment-into-banks"></a>将内存空间段分割成内存库


## <span id="ddk_dividing_a_memory_space_segment_into_banks_gg"></span><span id="DDK_DIVIDING_A_MEMORY_SPACE_SEGMENT_INTO_BANKS_GG"></span>


显示微型端口驱动程序可以向视频中的资源分配的最佳布局的视频内存管理器提供细粒度的提示[线性内存空间段](linear-memory-space-segments.md)除以到存款的内存 （段银行）。 如果该驱动程序将线性内存空间段划分为银行，驱动程序必须设置**UseBanking**中的位域标志**标志**的成员[ **DXGK\_SEGMENTDESCRIPTOR** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_dxgk_segmentdescriptor)段结构。 驱动程序将返回有关存款内存中的提示**HintedBank**的成员[ **DXGK\_ALLOCATIONINFO** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_dxgk_allocationinfo)分配的结构时的视频内存管理器会调用驱动程序的[ **DxgkDdiCreateAllocation** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_createallocation)函数。 有关详细信息，请参阅[创建分配时指定段](specifying-segments-when-creating-allocations.md)。

尽管分配必须完全包含在一个段，分配可以跨越区段内银行的边界。

如果使用银行，驱动程序必须包括与银行的段的整个地址空间。 第一个存储库始终开始段内的偏移量为零，最后一个银行始终结尾处的段的结束。 银行是连续和它们之间没有可用空间。

 

 





