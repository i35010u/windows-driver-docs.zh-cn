---
title: 正在加载 AYUV Alpha 混合图面
description: 正在加载 AYUV Alpha 混合图面
ms.assetid: 93b60622-47af-485c-a1db-9a05783ff698
keywords:
- alpha 混合数据加载 WDK DirectX VA
- 混合型的图片 WDK DirectX VA，alpha 混合数据加载
- AYUV alpha 值混合处理面 WDK DirectX VA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f27309f40e7e9c1a9f178714e0ef257862ca5bf4
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56545863"
---
# <a name="loading-an-ayuv-alpha-blending-surface"></a>正在加载 AYUV Alpha 混合图面


## <span id="ddk_loading_an_ayuv_alpha_blending_surface_gg"></span><span id="DDK_LOADING_AN_AYUV_ALPHA_BLENDING_SURFACE_GG"></span>


AYUV alpha 值混合处理的图面定义为数组的样本的 32 位中的每个[ **DXVA\_AYUVsample2** ](https://msdn.microsoft.com/library/windows/hardware/ff563116)结构。 用于混合包含解码后的视频图片的图形，可以作为源使用此图面。

指定的宽度和高度 AYUV alpha 值混合处理图面中关联[缓冲区描述列表](buffer-description-list.md)。

### <a name="span-idloadinga16-entryyuvpalettespanspan-idloadinga16-entryyuvpalettespanspan-idloadinga16-entryyuvpalettespanloading-a-16-entry-yuv-palette"></a><span id="Loading_a_16-Entry_YUV_Palette"></span><span id="loading_a_16-entry_yuv_palette"></span><span id="LOADING_A_16-ENTRY_YUV_PALETTE"></span>正在加载 16 项 YUV 调色板

16 项 YUV 调色板定义为 16 的数组[ **DXVA\_AYUVsample2** ](https://msdn.microsoft.com/library/windows/hardware/ff563116)结构。 此调色板一起 IA44 或 AI44 alpha 值混合处理的面。 调色板数组发送到在 AYUV alpha 值混合处理示例缓冲区中的加速器 （缓冲区类型 8）。 在这种情况下， **bSampleAlpha8** DXVA 成员\_AYUVsample2 结构的每个示例没有意义，并且必须为零。

YUV 调色板可以用于创建混合包含解码后的视频图片的图形的源。 此面板可用于创建以及图形的源

-   是 IA44/AI44 alpha 值混合处理的表面，*或*

-   DPXD alpha 值混合处理面、 突出显示缓冲区和 DCCMD 数据

### <a name="span-idloadinganayuvsurfacespanspan-idloadinganayuvsurfacespanspan-idloadinganayuvsurfacespanloading-an-ayuv-surface"></a><span id="Loading_an_AYUV_Surface"></span><span id="loading_an_ayuv_surface"></span><span id="LOADING_AN_AYUV_SURFACE"></span>正在加载 AYUV 面

而不被加载只是 16 项调色板，只需直接作为 AYUV 映像指定的图形的内容加载一整个图像的图形。 在这种情况下，AYUV 图发送到在 AYUV alpha 值混合处理示例缓冲区中的加速器 （缓冲区类型 8） 中指定的那样[ **DXVA\_BufferDescription** ](https://msdn.microsoft.com/library/windows/hardware/ff563122)结构。

### <a name="span-idloadingania44ai44alpha-blendingsurfacespanspan-idloadingania44ai44alpha-blendingsurfacespanspan-idloadingania44ai44alpha-blendingsurfacespanloading-an-ia44ai44-alpha-blending-surface"></a><span id="Loading_an_IA44_AI44_Alpha-Blending_Surface"></span><span id="loading_an_ia44_ai44_alpha-blending_surface"></span><span id="LOADING_AN_IA44_AI44_ALPHA-BLENDING_SURFACE"></span>正在加载 IA44/AI44 Alpha 值混合处理的图面

索引的 alpha 4-4 (IA44) alpha 值混合处理面定义为 8 位样本，其中每个结构化为一个字节数组。 此字节被称为*DXVA\_IA44sample*并在中定义*dxva.h*。 4 的最高有效位的此字节包含索引嘿 *SampleIndex4*，并且此字节的 4 个最低有效位包含 alpha 值称为*SampleAlpha4*。

Alpha-索引 4-4 (AI44) alpha 值混合处理面定义为 8 位样本，其中每个结构化为一个字节数组。 此字节被称为*DXVA\_AI44sample*并在中定义*dxva.h*。 包含此字节的 4 个最高有效位的 alpha 值称为*SampleAlpha4* ，并且此字节的 4 个最低有效位包含称为索引*SampleIndex4*。

*SampleIndex4*两个字段*DXVA\_IA44sample*并*DXVA\_AI44sample*包含索引的 16 项调色板示例。

*SampleAlpha4*两个字段*DXVA\_IA44sample*并*DXVA\_AI44sample*包含以下值，以指定的不透明度示例：

-   零表示该示例是透明 (以便的调色板条目*SampleIndex4*生成混合型图片不起)。 为零的值*SampleAlpha4*，blend 指定是使用无需更改的图片值。

-   值为 15，则表示该示例不透明 (以便的调色板条目*SampleIndex4*完全确定生成混合型的图片)。

-   非零值，指示指定 blend 找到由以下表达式：

((*SampleAlpha4*+ 1) X 图\_值 + (15-*SampleAlpha4*) X 图片\_值 + 8) &gt; &gt; 4

指定的宽度和高度 IA44 alpha 值混合处理图面中关联[缓冲区描述列表](buffer-description-list.md)。

 

 





