---
title: 线性孔径空间段
description: 线性孔径空间段
ms.assetid: bf818841-eb73-442e-8745-a59d9c3a527c
keywords:
- 内存段 WDK 显示线性 aperture 空间段
- 线性 aperture 空间段 WDK 显示
- aperture 空间段 WDK 显示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5da5e760db98f5c43cd2bc0f8cea1ace51cdc59a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63354240"
---
# <a name="linear-aperture-space-segments"></a>线性孔径空间段


## <span id="ddk_linear_aperture_space_segments_gg"></span><span id="DDK_LINEAR_APERTURE_SPACE_SEGMENTS_GG"></span>


线性 aperture 空间段是类似于线性内存空间段;但是，aperture 空间段是地址空间，并且不能包含 bits。 用于保存位，必须分配系统内存页，且必须重定向的地址空间范围来指这些页。 显示微型端口驱动程序必须实现[ **DxgkDdiBuildPagingBuffer** ](https://msdn.microsoft.com/library/windows/hardware/ff559587) DXGK 函数\_操作\_映射\_APERTURE\_段和 DXGK\_操作\_UNMAP\_APERTURE\_细分操作类型来处理重定向，并必须公开此函数，如中所述[ **显示微型端口驱动程序 DriverEntry**](https://msdn.microsoft.com/library/windows/hardware/ff556157)。 *DxgkDdiBuildPagingBuffer*函数接收重定向的范围和 MDL 引用所分配的物理系统内存页。

显示微型端口驱动程序通常通过编程是未知的视频内存管理器的页表来实现地址空间范围的重定向。

该驱动程序必须设置**Aperture**中的位域标志**标志**的成员[ **DXGK\_SEGMENTDESCRIPTOR** ](https://msdn.microsoft.com/library/windows/hardware/ff562035)结构，以指定线性 aperture 空间段。 该驱动程序还可以设置以下的位域标志，以指示其他段支持：

-   **CpuVisible**来指示段是 CPU 可访问。

-   **CacheCoherent**来指示段维护缓存一致性，cpu 将段重定向的页。

下图显示了线性 aperture 空间段的可视表示形式。

![说明线性 aperture 空间段的关系图](images/aptrspac.png)

 

 





