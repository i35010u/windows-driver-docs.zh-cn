---
title: 线性内存空间段
description: 线性内存空间段
ms.assetid: c937eb39-b9ec-454e-98c5-7f5274328226
keywords:
- 内存段 WDK 显示线性的内存空间段
- 线性内存空间段 WDK 显示
- 内存空间段 WDK 显示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: dd6f6f0d76197f83abd89257d97368dfa3bff75a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56522442"
---
# <a name="linear-memory-space-segments"></a>线性内存空间段


## <span id="ddk_linear_memory_space_segments_gg"></span><span id="DDK_LINEAR_MEMORY_SPACE_SEGMENTS_GG"></span>


线性内存空间段是段的显示硬件使用的经典类型。 线性内存空间该段符合以下模型：

-   虚拟化位于图形适配器上的视频内存。

-   由 GPU 直接访问 (也就是说，不使用页映射通过重定向)。

-   管理以线性方式在一维的地址空间中。

驱动程序集**标志**的成员[ **DXGK\_SEGMENTDESCRIPTOR** ](https://msdn.microsoft.com/library/windows/hardware/ff562035)为 0，以指定线性内存空间段结构。 但是，该驱动程序可以设置以下的位域标志，以指示其他段支持：

-   **CpuVisible**来指示段是 CPU 可访问。

-   **UseBanking**来指示段分为银行。

下图显示了线性内存空间段的可视表示形式。

![说明线性内存空间段的关系图](images/memspac.png)

 

 





