---
title: 优化的纹理 API
description: 优化的纹理 API
ms.assetid: 58d42807-3f52-415e-a06a-2ed408c20fb0
keywords:
- 纹理管理 WDK Direct3D，优化纹理
- 优化的纹理 WDK Direct3D
- CAPS2_HINTDYNAMIC
- DDSCAPS2_HINTSTATIC
- DDSCAPS2_OPAQUE
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f704390e71e4d13bc0d7c3fb72c7aca4b2d52cb0
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63379851"
---
# <a name="optimized-texture-api"></a>优化的纹理 API


## <span id="ddk_optimized_texture_api_gg"></span><span id="DDK_OPTIMIZED_TEXTURE_API_GG"></span>


三种新功能指示可以应用于 DirectDrawSurface 对象的优化的级别。 可以使用这些 caps 位标记在 DirectX 6.0 和更高版本，仅纹理。 优化的图面上模式可能会扩展在将来以涵盖其他类型的图面，尽管语义可能与纹理相同。

若要解决这些问题，三个新的标记中提供了**DirectDrawSurface7::创建**方法。 当这三个标识都没有指定，决定是否对修补程序或 swizzle 应由驱动程序。 这些标志如下所示：

<span id="DDSCAPS2_HINTDYNAMIC"></span><span id="ddscaps2_hintdynamic"></span>DDSCAPS2\_HINTDYNAMIC  
指示该驱动程序与流式处理视频或过程化纹理如使用此图面已锁定通常情况下，（例如，一次每一帧）。 此值应适用于*所有*驱动程序枚举纹理图面上的格式。 该驱动程序应避免任何转换，以便这些纹理，尤其是需要一些系统开销。

<span id="DDSCAPS2_HINTSTATIC"></span><span id="ddscaps2_hintstatic"></span>DDSCAPS2\_HINTSTATIC  
这将指示在图面可以是重新排序/retiled/swizzled 中的驱动程序**IDirect3DDevice7::Load**并**IDirectDrawSurface7::Blt** （Direct3D SDK 和 DirectDraw 中描述的方法SDK 文档中，分别)。 此操作不更改纹理的大小。 它是相对较快，和对称的因为该应用程序仍可能会锁定这些位 （尽管这会的性能造成影响时执行此操作）。 驱动程序不允许失败这些图面上的锁，因此不能使用有损压缩技术。 在这种情况下可能互相交错 MIP 映射图面。

此值不是强制 swizzling 在任何情况下，尤其是那些在其上的任何性能优势会发生。 某些纹素格式可能会以静默方式失败到 swizzle。

<span id="DDSCAPS2_OPAQUE"></span><span id="ddscaps2_opaque"></span>DDSCAPS2\_OPAQUE  
这向驱动程序表明，将再次将应用程序通过访问此图面。 此标志的行为类似于 DDSCAPS2\_HINTSTATIC 标志，但只允许实际的压缩增加了使用特定于硬件的压缩方案。 此操作是相对较慢，但应该允许简单、 对称压缩方案 (如 YUV 4:2:0 或颜色单元格压缩)，才能使用提供的压缩率从 2 到 6 倍。 非对称的方案，例如 VQ 应此处不能使用因为它们会导致不可接受的基准。

驱动程序，可以任意交错 MIP 映射纹理。 此方法可能应仅请求之外如何时从磁盘加载纹理的内部呈现循环。 堆大小报告此类纹理加载之后反映减少的内存占用，如果应用了压缩。 纹理上没有其他标头的开销，因此压缩许多小纹理不会保存尽可能多的内存是预期。

一般情况下，就有关纹理压缩率或压缩质量权限隐含的此标志不能保证。

在以下情况下，创建具有此标志的图面失败：

调用**IDirectDrawSurface7::Lock**方法。

调用**IDirectDrawSurface7::GetDC**方法。

到此类表面 subrectangle blts。

通过此类界面的所有 blts。

若要将数据放入此类表面的唯一方法是使用**IDirect3DDevice7::Load**方法 （Direct3D SDK 文档中介绍） 或完全图面上的 blt 调用。 有关详细信息**IDirectDrawSurface7::Lock**并**IDirectDrawSurface7::GetDC**，请参阅 DirectDraw SDK 文档。

 

 





