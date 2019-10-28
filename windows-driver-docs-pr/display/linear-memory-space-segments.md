---
title: 线性内存空间段
description: 线性内存空间段
ms.assetid: c937eb39-b9ec-454e-98c5-7f5274328226
keywords:
- 内存段 WDK 显示，线性内存空间段
- 线性内存空间段 WDK 显示
- 内存空间段 WDK 显示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2b2434a41cb91a47ea46d17612e9bd4e7fe9c21f
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840392"
---
# <a name="linear-memory-space-segments"></a>线性内存空间段


## <span id="ddk_linear_memory_space_segments_gg"></span><span id="DDK_LINEAR_MEMORY_SPACE_SEGMENTS_GG"></span>


线性内存空间段是显示硬件使用的传统的段类型。 线性内存空间段符合以下模型：

-   虚拟化位于图形适配器上的视频内存。

-   可以通过 GPU 直接访问（即，不通过页映射进行重定向）。

-   在一维地址空间中以线性方式进行管理。

驱动程序将[**DXGK\_SEGMENTDESCRIPTOR**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_segmentdescriptor)结构的**Flags**成员设置为0，以指定线性内存空间段。 但是，驱动程序可以设置以下位域标志以指示其他段支持：

-   **CpuVisible** ，指示段是 CPU 可访问的。

-   **UseBanking** ，指示段划分为多个槽。

下图显示了线性内存空间段的直观表示形式。

![说明线性内存空间段的关系图](images/memspac.png)

 

 





