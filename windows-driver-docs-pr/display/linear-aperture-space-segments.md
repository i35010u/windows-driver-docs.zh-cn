---
title: 线性孔径空间段
description: 线性孔径空间段
ms.assetid: bf818841-eb73-442e-8745-a59d9c3a527c
keywords:
- 内存段 WDK 显示，线性口径-空间段
- 线性口径-空间段 WDK 显示
- 口径空间段 WDK 显示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1c1e6dc127e9d976b44cbee473273cf399f2b374
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89065814"
---
# <a name="linear-aperture-space-segments"></a>线性孔径空间段


## <span id="ddk_linear_aperture_space_segments_gg"></span><span id="DDK_LINEAR_APERTURE_SPACE_SEGMENTS_GG"></span>


线性口径区类似于线性内存空间段;但是，口径区只是一个地址空间，不能保存位。 若要保存位，必须分配系统内存页，且必须重定向地址空间范围以引用这些页。 显示微型端口驱动程序必须实现[**DxgkDdiBuildPagingBuffer**](/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_buildpagingbuffer) DXGK \_ 操作 \_ 映射口径段的 DxgkDdiBuildPagingBuffer 函数 \_ \_ ，并实现 DXGK \_ 操作取消 \_ 映射 \_ \_ 片段段操作类型以处理重定向，并且必须按照[**显示微型端口驱动程序 DriverEntry**](./driverentry-of-display-miniport-driver.md)中所述公开此功能。 *DxgkDdiBuildPagingBuffer*函数接收要重定向的范围以及引用已分配的物理系统内存页的 MDL。

显示微型端口驱动程序通常通过编程页面表来完成地址空间范围的重定向，这对于视频内存管理器来说是未知的。

驱动程序必须在[**DXGK \_ SEGMENTDESCRIPTOR**](/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_segmentdescriptor)结构的**Flags**成员中设置**口径**位域标志，才能指定线性口径区。 驱动程序还可以设置以下位域标志以指示其他段支持：

-   **CpuVisible** ，指示段是 CPU 可访问的。

-   **CacheCoherent** ，以指示段将维护与段所重定向的页的 CPU 的缓存一致性。

下图显示了线性光圈空间段的直观表示形式。

![说明线性口径区的关系图](images/aptrspac.png)

 

