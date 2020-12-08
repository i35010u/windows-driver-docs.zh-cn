---
title: 优化的纹理 API
description: 优化的纹理 API
keywords:
- 纹理管理 WDK Direct3D，优化纹理
- 优化纹理 WDK Direct3D
- CAPS2_HINTDYNAMIC
- DDSCAPS2_HINTSTATIC
- DDSCAPS2_OPAQUE
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 370f32a4be2011d3ade1abd66378652cf7c49a12
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96837301"
---
# <a name="optimized-texture-api"></a>优化的纹理 API


## <span id="ddk_optimized_texture_api_gg"></span><span id="DDK_OPTIMIZED_TEXTURE_API_GG"></span>


三个新功能指示可以应用于 DirectDrawSurface 对象的优化级别。 在 DirectX 6.0 和更高版本中，只能用这些大写字母来标记纹理。 尽管语义可能不同于纹理，但将来可能会延长优化 surface 模式以涵盖其他类型的表面。

为了解决这些问题， **DirectDrawSurface7：： Create** 方法中提供了三个新标志。 如果未指定这三个标志中的任何一个，则决定是要将 patch 还是 swizzle 留给驱动程序。 这些标志如下所示：

<span id="DDSCAPS2_HINTDYNAMIC"></span><span id="ddscaps2_hintdynamic"></span>DDSCAPS2 \_ HINTDYNAMIC  
向驱动程序指示此表面经常锁定， (例如，每帧一次) 用于使用流式处理视频或过程性纹理。 此上限应该适用于 *所有* 驱动程序枚举纹理表面格式。 驱动程序应避免对这些纹理进行任何转换，尤其是在需要一些开销的情况下。

<span id="DDSCAPS2_HINTSTATIC"></span><span id="ddscaps2_hintstatic"></span>DDSCAPS2 \_ HINTSTATIC  
这向驱动程序表明，可以在 Direct3D SDK 和 DirectDraw SDK 文档 (分别) 在 **IDirect3DDevice7：： Load** 和 **IDirectDrawSurface7：： Blt** 方法中对该图面重新排序/retiled/swizzled。 此操作不会更改纹理的大小。 它的速度相对较快，并且对称，因为应用程序可能仍会锁定这些位 (但) 时，这会导致性能下降。 不允许驱动程序在这些表面上出现锁故障，因此不能使用有损压缩技术。 在这种情况下，MIP 地图图面可以交错。

此上限并未用于在任何情况下强制 swizzling，尤其是那些不会带来性能优势的情况。 有些纹素格式可能会自动 swizzle。

<span id="DDSCAPS2_OPAQUE"></span><span id="ddscaps2_opaque"></span>DDSCAPS2 不 \_ 透明  
这向驱动程序表明，应用程序将不会再访问此表面。 此标志的行为类似于 DDSCAPS2 \_ HINTSTATIC 标志，但添加了允许使用特定于硬件的压缩方案的实际压缩。 此操作的速度相对较慢，但应允许使用简单的对称压缩方案 (例如 YUV 4:2:0，或使用颜色单元格压缩) 来提供从2到6倍的压缩率。 不应在此处使用非对称方案（如 VQ），因为它们会导致不可接受的基准。

该驱动程序可以随意交错使用 MIP map 纹理。 此方法可能只在内部呈现循环之外（例如，当从磁盘中加载纹理时）发出请求。 加载此类纹理后，堆大小报表反映了应用压缩后的内存占用量。 纹理上还有额外的标头开销，因此压缩许多小纹理并不会像预期那样保存尽可能多的内存。

通常，不保证纹理压缩率或此标志隐含的压缩质量。

在以下情况下，用此标志创建的图面将失败：

调用 **IDirectDrawSurface7：： Lock** 方法。

对 **IDirectDrawSurface7：： GetDC** 方法的调用。

Subrectangle blts。

此类图面上的所有 blts。

将数据放入此类图面的唯一方法是使用 **IDirect3DDevice7：： Load** 方法 (Direct3D SDK 文档) 中所述的方法，或完整的 surface blt 调用。 有关 **IDirectDrawSurface7：： Lock** 和 **IDirectDrawSurface7：： GetDC** 的详细信息，请参阅 DirectDraw SDK 文档。

 

 





