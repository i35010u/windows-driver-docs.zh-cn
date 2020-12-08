---
title: 线性内存空间段
description: 线性内存空间段
keywords:
- 内存段 WDK 显示，线性内存空间段
- 线性内存空间段 WDK 显示
- 内存空间段 WDK 显示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c25f1cc23082b971914036fdd54fcfd736b627f8
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96838999"
---
# <a name="linear-memory-space-segments"></a>线性内存空间段


## <span id="ddk_linear_memory_space_segments_gg"></span><span id="DDK_LINEAR_MEMORY_SPACE_SEGMENTS_GG"></span>


线性内存空间段是显示硬件使用的传统的段类型。 线性内存空间段符合以下模型：

-   虚拟化位于图形适配器上的视频内存。

-   可以通过 GPU (直接访问，而无需通过页映射) 进行重定向。

-   在一维地址空间中以线性方式进行管理。

驱动程序将 [**DXGK \_ SEGMENTDESCRIPTOR**](/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_segmentdescriptor)结构的 **Flags** 成员设置为0，以指定线性内存空间段。 但是，驱动程序可以设置以下位域标志以指示其他段支持：

-   **CpuVisible** ，指示段是 CPU 可访问的。

-   **UseBanking** ，指示段划分为多个槽。

下图显示了线性内存空间段的直观表示形式。

![说明线性内存空间段的关系图](images/memspac.png)

 

