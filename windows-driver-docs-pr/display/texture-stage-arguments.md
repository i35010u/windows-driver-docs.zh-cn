---
title: 纹理阶段参数
description: 纹理阶段参数
ms.assetid: 434a0b88-2fb6-43e3-8a54-48f134a0dbff
keywords:
- 多个纹理 WDK Direct3D，纹理阶段
- 纹理阶段 WDK Direct3D
- 纹理管理 WDK Direct3D，阶段
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 88b1fe8043c0390384b500187101280d236548b2
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63362617"
---
# <a name="texture-stage-arguments"></a>纹理阶段参数


## <span id="ddk_texture_stage_arguments_gg"></span><span id="DDK_TEXTURE_STAGE_ARGUMENTS_GG"></span>


每个值混合处理操作的多个纹理结合了两个输入。 这些可以通过调用所选**IDirect3DDevice7::SetTextureStageState**方法并指定 D3DTEXTURESTAGESTATETYPE 的以下成员之一的枚举类型。

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
<td align="left"><p>第一个输入 alpha 操作的控件。</p></td>
</tr>
<tr class="even">
<td align="left"><p>D3DTSS_ALPHAARG2</p></td>
<td align="left"><p>控制 alpha 操作的第二个输入。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>D3DTSS_COLORARG1</p></td>
<td align="left"><p>第一个输入颜色操作的控件。</p></td>
</tr>
<tr class="even">
<td align="left"><p>D3DTSS_COLORARG2</p></td>
<td align="left"><p>控制颜色操作的第二个输入。</p></td>
</tr>
</tbody>
</table>

 

有关的说明**IDirect3DDevice7::SetTextureStageState**，请参阅 Direct3D SDK 文档。

### <a name="span-idtextureargumentflagsspanspan-idtextureargumentflagsspantexture-argument-flags"></a><span id="texture_argument_flags"></span><span id="TEXTURE_ARGUMENT_FLAGS"></span>纹理参数标志

在每个纹理阶段，任何上述四个参数可以设置使用下表中列出的纹理参数标志。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Flag</th>
<th align="left">含义</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>D3DTA_CURRENT</p></td>
<td align="left"><p>纹理参数是上一混合阶段的结果。 在第一个纹理阶段 （阶段零），此参数等效于 D3DTA_DIFFUSE。 这可以被视为多边形的当前颜色为每个纹理混合到它。 如果上一混合阶段使用的凹凸贴图纹理 （D3DTOP_BUMPENVMAP 操作），系统会选择来自之前凹凸贴图纹理阶段纹理。 (如果<em>s</em>表示当前的纹理阶段，并<em>s-1</em>包含的凹凸贴图纹理，此参数将结果输出成为由纹理阶段<em>s-2</em>。)</p></td>
</tr>
<tr class="even">
<td align="left"><p>D3DTA_DIFFUSE</p></td>
<td align="left"><p>获取从高氏内插器的迭代的颜色数据。 这通常用作上第一个纹理，ARG2，因为此时没有 D3DTA_CURRENT 纹理颜色。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>D3DTA_TEXTURE</p></td>
<td align="left"><p>绑定到此纹理阶段使用的纹理<strong>IDirect3DDevice7::SetTexture</strong>(n，lpTex3) 方法 （Direct3D SDK 文档中介绍），其中<em>n</em>是阶段编号。 <strong>IDirect3DDevice7::SetTexture</strong>定义要在此阶段中使用的纹理，D3DTA_TEXTURE 时的自变量之一的纹理对象。 仅可出现在 D3DTSS_ALPHAARG1 和 D3DTSS_COLORARG1，但不是在 D3DTSS_ALPHAARG1 和 D3DTSS_COLORARG2 D3DTA_TEXTURE。</p></td>
</tr>
<tr class="even">
<td align="left"><p>D3DTA_TFACTOR</p></td>
<td align="left"><p>在使用 D3DRENDERSTATE_TEXTUREFACTOR Direct3D 中设置一个值。</p></td>
</tr>
</tbody>
</table>

 

**请注意**  有些实现可能不能同时使用这两个 D3DTA\_TFACTOR 和 D3DTA\_漫射颜色。

 

### <a name="span-idmodifierflagsspanspan-idmodifierflagsspanmodifier-flags"></a><span id="modifier_flags"></span><span id="MODIFIER_FLAGS"></span>修饰符标志

下表中列出的两个值应与前面标志使用按位 OR 运算符之一结合使用。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">ReplTest1</th>
<th align="left">含义</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>D3DTA_ALPHAREPLICATE</p></td>
<td align="left"><p>指示此参数应具有其复制到之前在此操作中使用的所有颜色通道的 alpha 通道。 如果只有一个组件使用的纹理，它是自动复制到这些操作的所有颜色通道。 无需为 ALPHA_ARGs，指定此标志，但使用它不会生成错误。</p></td>
</tr>
<tr class="even">
<td align="left"><p>D3DTA_COMPLEMENT</p></td>
<td align="left"><p>指示此参数，应反转操作。</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-iddefaultsspanspan-iddefaultsspandefaults"></a><span id="defaults"></span><span id="DEFAULTS"></span>默认值

如果应用程序未填入一个状态，使用以下默认值。 定义了这些默认值，以使多个纹理操作更方便，而可靠的代码始终完全指定所需的状态。

D3DTSS\_COLORARG1 和 D3DTSS\_ALPHAARG1 均默认设置 D3DTA\_纹理，如果已设置相应的纹理。 如果已为此阶段，不设置任何纹理，则这两项都默认为 D3DTA\_漫射。

D3DTSS\_COLORARG2 和 D3DTSS\_ALPHAARG2 默认为 D3DTA\_当前。 请注意该 D3DTA\_当前默认为 D3DTA\_漫射上第一阶段 (D3DTA 说明中所注明的除外\_当前)。

ARG2 默认为 D3DTA\_漫射、 但被忽略，因为该操作将默认为 D3DTOP\_SELECTARG1。

D3DTA\_漫射 0xFFFFFFF 到默认值，如果在灵活的顶点数据格式 (FVF) 中指定无漫射颜色。

D3DTA\_反射默认值为 0x00000000，如果在 FVF 数据中不指定任何反射颜色。

D3DTA\_当前默认为 D3DTA\_漫射如果这是第一阶段，除非上一混合阶段是 D3DTOP\_BUMPENVMAP 或 D3DTOP\_BUMPENVMAPLUMINANCE 颜色操作。 在这种情况下，将发生以下情况：

-   如果上一阶段是 D3DTOP\_BUMPENVMAP 或 D3DTOP\_BUMPENVMAPLUMINANCE，则此参数是在上一阶段之前阶段的结果。

-   在第二个纹理阶段 （第一阶段），此参数默认为 D3DTA\_漫射。

D3DTA\_纹理是一个值，D3DTSS\_COLORARG1 或 D3DTSS\_ALPHAARG1 任何的状态阶段或默认值为 0x0，如果没有纹理绑定到此阶段。

 

 





