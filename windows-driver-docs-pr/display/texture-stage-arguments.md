---
title: 纹理阶段参数
description: 纹理阶段参数
keywords:
- 多纹理 WDK Direct3D，纹理阶段
- 纹理阶段 WDK Direct3D
- 纹理管理 WDK Direct3D，阶段
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9cb2782e6448e5a2913c96a3f8352a03bc262071
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96801815"
---
# <a name="texture-stage-arguments"></a>纹理阶段参数


## <span id="ddk_texture_stage_arguments_gg"></span><span id="DDK_TEXTURE_STAGE_ARGUMENTS_GG"></span>


每个多纹理混合操作都结合了两个输入。 为此，可以调用 **IDirect3DDevice7：： SetTextureStageState** 方法并指定 D3DTEXTURESTAGESTATETYPE 枚举类型的以下成员之一。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">枚举器</th>
<th align="left">含义</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>D3DTSS_ALPHAARG1</p></td>
<td align="left"><p>控制第一次输入到 alpha 运算。</p></td>
</tr>
<tr class="even">
<td align="left"><p>D3DTSS_ALPHAARG2</p></td>
<td align="left"><p>控制到 alpha 操作的第二个输入。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>D3DTSS_COLORARG1</p></td>
<td align="left"><p>控制首次输入到颜色操作。</p></td>
</tr>
<tr class="even">
<td align="left"><p>D3DTSS_COLORARG2</p></td>
<td align="left"><p>控制颜色操作的第二个输入。</p></td>
</tr>
</tbody>
</table>

 

有关 **IDirect3DDevice7：： SetTextureStageState** 的说明，请参阅 Direct3D SDK 文档。

### <a name="span-idtexture_argument_flagsspanspan-idtexture_argument_flagsspantexture-argument-flags"></a><span id="texture_argument_flags"></span><span id="TEXTURE_ARGUMENT_FLAGS"></span>纹理参数标志

在每个纹理阶段，都可以使用下表中列出的纹理参数标志设置前面四个参数中的任何一个。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">标志</th>
<th align="left">含义</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>D3DTA_CURRENT</p></td>
<td align="left"><p>纹理参数是上一个混合阶段的结果。 在第一个纹理阶段 (阶段零) ，此参数与 D3DTA_DIFFUSE 等效。 在将每个纹理混合到多边形上时，可以将此视为多边形的当前颜色。 如果上一个混合阶段使用凹凸地图纹理 (D3DTOP_BUMPENVMAP 操作) ，则系统会在凹凸地图纹理之前从该阶段选择纹理。  (如果 <em>s</em> 表示当前纹理阶段，而 <em>s-1</em> 包含凹凸地图纹理，则此参数将成为纹理阶段 <em>s-2</em>的结果输出。 ) </p></td>
</tr>
<tr class="even">
<td align="left"><p>D3DTA_DIFFUSE</p></td>
<td align="left"><p>从 Gouraud interpolators 获取的循环颜色数据。 这通常用作第一个纹理上的 ARG2，因为此时没有 D3DTA_CURRENT 纹理颜色。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>D3DTA_TEXTURE</p></td>
<td align="left"><p>使用 <strong>IDirect3DDevice7：： SetTexture</strong> (n，lpTex3) )  (方法绑定到此纹理阶段的纹理，其中 <em>n</em> 是阶段编号。 <strong>IDirect3DDevice7：： SetTexture</strong> 定义 D3DTA_TEXTURE 是参数之一时要用于此阶段中的纹理的纹理对象。 D3DTA_TEXTURE 只能存在于 D3DTSS_ALPHAARG1 和 D3DTSS_COLORARG1，而不能存在于 D3DTSS_ALPHAARG1 和 D3DTSS_COLORARG2 中。</p></td>
</tr>
<tr class="even">
<td align="left"><p>D3DTA_TFACTOR</p></td>
<td align="left"><p>在 Direct3D 中使用 D3DRENDERSTATE_TEXTUREFACTOR 设置的值。</p></td>
</tr>
</tbody>
</table>

 

**注意**   某些实现可能不能同时使用 D3DTA \_ TFACTOR 和 D3DTA \_ 漫射色。

 

### <a name="span-idmodifier_flagsspanspan-idmodifier_flagsspanmodifier-flags"></a><span id="modifier_flags"></span><span id="MODIFIER_FLAGS"></span>修饰符标志

下表中列出的两个值应使用按位 "或" 运算符与上述标志之一结合使用。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">“值”</th>
<th align="left">含义</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>D3DTA_ALPHAREPLICATE</p></td>
<td align="left"><p>指示在此操作中使用之前，此参数应将其 alpha 通道复制到所有颜色通道。 如果这是仅有一个组件的纹理，则会自动将其复制到这些操作的所有颜色通道。 不需要为 ALPHA_ARGs 指定此标志，但使用该标志不会产生错误。</p></td>
</tr>
<tr class="even">
<td align="left"><p>D3DTA_COMPLEMENT</p></td>
<td align="left"><p>指示应对此操作进行相反的操作。</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-iddefaultsspanspan-iddefaultsspandefaults"></a><span id="defaults"></span><span id="DEFAULTS"></span>出厂

如果应用程序未填充状态，则使用以下默认值。 尽管已定义这些默认值以使多个纹理操作更方便，但可靠的代码始终会完全指定所需状态。

\_ \_ 如果设置了相应的纹理，D3DTSS COLORARG1 和 D3DTSS ALPHAARG1 都默认为 D3DTA \_ 纹理。 如果没有为此阶段设置纹理，则这两个都默认为 D3DTA \_ 漫射。

D3DTSS \_ COLORARG2 和 D3DTSS \_ ALPHAARG2 默认为 D3DTA \_ CURRENT。 请注意，默认情况下，D3DTA \_ current 默认为 D3DTA \_ 漫射 (第一阶段的 D3DTA，但描述 \_ CURRENT) 。

ARG2 默认为 D3DTA \_ 漫射，但被忽略，因为此操作默认为 D3DTOP \_ SELECTARG1。

\_如果在灵活顶点格式 (FVF) 数据中未指定漫射颜色，则 D3DTA 漫射默认为0xFFFFFFF。

\_如果未在 FVF 数据中指定镜面颜色，则 D3DTA 反射默认为0x00000000。

\_如果这是第一个阶段，D3DTA CURRENT 默认值为 D3DTA \_ 漫射，但上一个混合阶段为 D3DTOP \_ BUMPENVMAP 或 D3DTOP \_ BUMPENVMAPLUMINANCE color 操作时除外。 在这种情况下，将发生以下情况：

-   如果前一阶段是 D3DTOP \_ BUMPENVMAP 或 D3DTOP \_ BUMPENVMAPLUMINANCE，则此参数是上一阶段之前阶段的结果。

-   在第二个纹理阶段 (第一个) 阶段，此参数默认为 D3DTA \_ 漫射。

D3DTA \_ 纹理是 \_ 任何阶段的 D3DTSS COLORARG1 或 D3DTSS \_ ALPHAARG1 状态的值，如果未绑定到此阶段，则默认为0x0。

 

 





