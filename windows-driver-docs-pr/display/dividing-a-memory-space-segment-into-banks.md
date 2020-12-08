---
title: 将内存空间段分割成内存库
description: 将内存空间段分割成内存库
keywords:
- 内存段 WDK 显示，银行
- 存款内存 WDK 显示
- 银行 WDK 显示
- 线性内存空间段 WDK 显示
- 内存段 WDK 显示，线性内存空间段
- 划分线性内存空间段 WDK 显示
- 内存空间段 WDK 显示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 499c623b5e46b1ca1a0e51aaddc4d264b9b9f69e
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96809201"
---
# <a name="dividing-a-memory-space-segment-into-banks"></a>将内存空间段分割成内存库


## <span id="ddk_dividing_a_memory_space_segment_into_banks_gg"></span><span id="DDK_DIVIDING_A_MEMORY_SPACE_SEGMENT_INTO_BANKS_GG"></span>


显示微型端口驱动程序可以通过将段划分为 (bank) 中的 "存款内存"，为视频内存管理器提供有关在 [线性内存空间段](linear-memory-space-segments.md) 内的视频资源分配的最佳放置的细化提示。 如果驱动程序将线性内存空间分割成 bank，则驱动程序必须在段的 [**DXGK \_ SEGMENTDESCRIPTOR**](/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_segmentdescriptor)结构的 **Flags** 成员中设置 **UseBanking** 位域标志。 当视频内存管理器调用驱动程序的 [**DxgkDdiCreateAllocation**](/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_createallocation)函数时，驱动程序将返回有关 [**DXGK \_ ALLOCATIONINFO**](/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_allocationinfo)结构的 **HintedBank** 成员中的存款 memory 的提示。 有关详细信息，请参阅 [创建分配时指定段](specifying-segments-when-creating-allocations.md)。

尽管分配必须完全包含在一个段中，但分配可以跨越段内的银行边界。

如果使用了 bank，则驱动程序必须涵盖包含银行的分段的整个地址空间。 第一个 bank 始终在段内的偏移量0处开始，最后一个 bank 始终结束于段的末尾。 银行是连续的，它们之间没有可用空间。

 

