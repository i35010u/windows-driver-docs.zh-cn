---
title: 加载 AYUV Alpha 混合图面
description: 加载 AYUV Alpha 混合图面
keywords:
- alpha-blend 数据加载 WDK DirectX VA
- 混合图片 WDK DirectX VA，alpha-blend 数据加载
- AYUV alpha-混合 surface WDK DirectX VA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e027410234511d8160463390594c25ea4f3b8ab0
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96792283"
---
# <a name="loading-an-ayuv-alpha-blending-surface"></a>加载 AYUV Alpha 混合图面


## <span id="ddk_loading_an_ayuv_alpha_blending_surface_gg"></span><span id="DDK_LOADING_AN_AYUV_ALPHA_BLENDING_SURFACE_GG"></span>


AYUV alpha 混合图面在 [**DXVA \_ AYUVsample2**](/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_ayuvsample2) 结构中定义为32位的样本数组。 此图面可用作将图形与已解码视频图片混合的源。

AYUV alpha 混合表面的宽度和高度在 "关联的 [缓冲区说明" 列表](buffer-description-list.md)中指定。

### <a name="span-idloading_a_16-entry_yuv_palettespanspan-idloading_a_16-entry_yuv_palettespanspan-idloading_a_16-entry_yuv_palettespanloading-a-16-entry-yuv-palette"></a><span id="Loading_a_16-Entry_YUV_Palette"></span><span id="loading_a_16-entry_yuv_palette"></span><span id="LOADING_A_16-ENTRY_YUV_PALETTE"></span>加载 16-Entry YUV 调色板

16-entry YUV 调色板定义为 16 [**DXVA \_ AYUVsample2**](/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_ayuvsample2) 结构的数组。 此调色板与 IA44 或 AI44 alpha 混合图面一起使用。 将调色板数组发送到 AYUV alpha 混合示例缓冲区 (缓冲区类型 8) 中的快捷键。 在这种情况下 **bSampleAlpha8** ， \_ 每个示例的 DXVA AYUVsample2 结构的 bSampleAlpha8 成员没有意义，并且必须为零。

YUV 调色板可用于创建使用解码视频图片来混合图形的源。 此调色板可用于创建图形源以及

-   IA44/AI44 alpha-混合图面， *或*

-   DPXD alpha 混合图面、高光缓冲区和 DCCMD 数据

### <a name="span-idloading_an_ayuv_surfacespanspan-idloading_an_ayuv_surfacespanspan-idloading_an_ayuv_surfacespanloading-an-ayuv-surface"></a><span id="Loading_an_AYUV_Surface"></span><span id="loading_an_ayuv_surface"></span><span id="LOADING_AN_AYUV_SURFACE"></span>加载 AYUV 图面

除了仅加载16项调色板外，整个图像图形都可以直接加载为 AYUV 图像来指定图形内容。 在这种情况下，会将 AYUV 图形发送到 AYUV alpha 混合样本缓冲区中的快捷键 (缓冲区类型 8) ，如 [**DXVA \_ BufferDescription**](/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_bufferdescription) 结构中所指定。

### <a name="span-idloading_an_ia44_ai44_alpha-blending_surfacespanspan-idloading_an_ia44_ai44_alpha-blending_surfacespanspan-idloading_an_ia44_ai44_alpha-blending_surfacespanloading-an-ia44ai44-alpha-blending-surface"></a><span id="Loading_an_IA44_AI44_Alpha-Blending_Surface"></span><span id="loading_an_ia44_ai44_alpha-blending_surface"></span><span id="LOADING_AN_IA44_AI44_ALPHA-BLENDING_SURFACE"></span>加载 IA44/AI44 Alpha-Blending 图面

4-4 (IA44) alpha 混合图面的索引-混合图面定义为一个8位样本数组，其中每个示例都构造为一个字节。 此字节称为 *DXVA \_ IA44sample* ，在 *DXVA* 中定义。 此字节的4个最高有效位包含一个称为 *SampleIndex4* 的索引，此字节的4个最小有效位包含一个称为 *SampleAlpha4* 的 alpha 值。

Alpha 索引 4-4 (AI44) alpha-混合图面定义为一个8位样本数组，其中每个示例都构造为一个字节。 此字节称为 *DXVA \_ AI44sample* ，在 *DXVA* 中定义。 此字节的4个最高有效位包含一个称为 *SampleAlpha4* 的 alpha 值，此字节的4个最小有效位包含一个称为 *SampleIndex4* 的索引。

*DXVA \_ IA44sample* 和 *DXVA \_ AI44sample* 的 *SampleIndex4* 字段包含示例的16项调色板的索引。

*DXVA \_ IA44sample* 和 *DXVA \_ AI44sample* 的 *SampleAlpha4* 字段包含以下值，用于指定示例的不透明度：

-   零指示示例是透明的 (以便 *SampleIndex4* 的调色板项对所生成的混合图片) 不起作用。 对于 *SampleAlpha4* 的零值，指定的 blend 是使用图片值而不进行更改。

-   值为15表示示例是不透明的 (以便 *SampleIndex4* 的调色板项完全确定) 生成的混合图片。

-   非零值指示通过以下表达式找到指定的 blend：

 ( # B1 *SampleAlpha4*+ 1) X 图形 \_ 值 + (15-*SampleAlpha4*) X 图片 \_ 值 + 8) &gt; &gt; 4

IA44 alpha 混合表面的宽度和高度在 "关联的 [缓冲区说明" 列表](buffer-description-list.md)中指定。

 

