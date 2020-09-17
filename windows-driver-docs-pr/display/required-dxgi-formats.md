---
title: 必需的 DXGI 格式
description: 本主题介绍了 Microsoft Direct3D 功能级别在用户模式显示驱动程序上放置的要求。
ms.assetid: 1CB419B9-DD5E-492F-AAAC-CFFFDE247F7F
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b94d6d081fb2e33a5994be48575aaccee63dcb12
ms.sourcegitcommit: b84d760d4b45795be12e625db1d5a4167dc2c9ee
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/17/2020
ms.locfileid: "90715992"
---
# <a name="required-dxgi-formats"></a>必需的 DXGI 格式


本主题介绍了 Microsoft Direct3D 功能级别在用户模式显示驱动程序上放置的要求。

第一个表的第一列和第二列显示驱动程序必须支持的所有 Direct3D 格式类型。 第三列显示 Direct3D [**D3D10 \_ format \_ 支持**](/windows/win32/api/d3d10/ne-d3d10-d3d10_format_support) 和/或 D3D11 格式的所有关联常量 [**值 \_ \_ 支持**](/windows/win32/api/d3d11/ne-d3d11-d3d11_format_support) 驱动程序必须支持的枚举。 第四列显示驱动程序必须支持每种格式的最小 Direct3D 功能级别。

第二个表显示每个枚举值的 Direct3D 10Level 9 支持算法。

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">D3D9 格式 (D3DDDIFMT_ * 和/或 D3DDECLTYPE<em></th>
<th align="left">D3D10 + API 等效 (DXGI_FORMAT_ </em>) </th>
<th align="left">必需 D3D10_ 或 D3D11_ FORMAT_SUPPORT_ 的枚举值</th>
<th align="left">所需的最小 Direct3D 级别</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left">A32B32G32R32F 或 D3DDECLTYPE_FLOAT4</td>
<td align="left">R32G32B32A32_FLOAT</td>
<td align="left"><p>IA_VERTEX_BUFFER</p>
<p>TEXTURE2D</p>
<p>TEXTURE3D</p>
<p>TEXTURECUBE</p>
<p>SHADER_LOAD</p>
<p>MIP</p>
<p>MIP_AUTOGEN</p>
<p>RENDER_TARGET</p>
<p>CPU_LOCKABLE</p></td>
<td align="left"><p>9_1</p>
<p>9_2</p>
<p>9_3</p>
<p>9_3</p>
<p>9_2</p>
<p>9_3</p>
<p>9_3</p>
<p>9_2</p>
<p>9_2</p></td>
</tr>
<tr class="even">
<td align="left">D3DDECLTYPE_FLOAT3</td>
<td align="left">R32G32B32_FLOAT</td>
<td align="left"><p>IA_VERTEX_BUFFER</p></td>
<td align="left"><p>9_1</p></td>
</tr>
<tr class="odd">
<td align="left">A16B16G16R16F 或 D3DDECLTYPE_FLOAT16_4</td>
<td align="left">R16G16B16A16_FLOAT</td>
<td align="left"><p>IA_VERTEX_BUFFER</p>
<p>TEXTURE2D</p>
<p>TEXTURE3D</p>
<p>TEXTURECUBE</p>
<p>SHADER_LOAD</p>
<p>MIP</p>
<p>MIP_AUTOGEN</p>
<p>RENDER_TARGET</p>
<p>BLENDABLE</p>
<p>CPU_LOCKABLE</p></td>
<td align="left"><p>9_3</p>
<p>9_2</p>
<p>9_2</p>
<p>9_2</p>
<p>9_2</p>
<p>9_2</p>
<p>9_2</p>
<p>9_2</p>
<p>9_3</p>
<p>9_2</p></td>
</tr>
<tr class="even">
<td align="left">A16B16G16R16 或 D3DDECLTYPE_USHORT4N</td>
<td align="left">R16G16B16A16_UNORM</td>
<td align="left"><p>TEXTURE2D</p>
<p>TEXTURE3D</p>
<p>TEXTURECUBE</p>
<p>SHADER_LOAD</p>
<p>SHADER_SAMPLE</p>
<p>MIP</p>
<p>MIP_AUTOGEN</p>
<p>RENDER_TARGET</p>
<p>CPU_LOCKABLE</p></td>
<td align="left"><p>9_2</p>
<p>9_2</p>
<p>9_2</p>
<p>9_2</p>
<p>9_2</p>
<p>9_2</p>
<p>9_2</p>
<p>9_2</p>
<p>9_2</p></td>
</tr>
<tr class="odd">
<td align="left">Q16W16V16U16 或 D3DDECLTYPE_SHORT4N</td>
<td align="left">R16G16B16A16_SNORM</td>
<td align="left"><p>IA_VERTEX_BUFFER</p></td>
<td align="left"><p>9_1</p></td>
</tr>
<tr class="even">
<td align="left">D3DDECLTYPE_SHORT4</td>
<td align="left">R16G16B16A16_SINT</td>
<td align="left"><p>IA_VERTEX_BUFFER</p></td>
<td align="left"><p>9_1</p></td>
</tr>
<tr class="odd">
<td align="left">G32R32F 或 D3DDECLTYPE_FLOAT2</td>
<td align="left">R32G32_FLOAT</td>
<td align="left"><p>IA_VERTEX_BUFFER</p>
<p>TEXTURE2D</p>
<p>TEXTURE3D</p>
<p>TEXTURECUBE</p>
<p>SHADER_LOAD</p>
<p>RENDER_TARGET</p>
<p>CPU_LOCKABLE</p></td>
<td align="left"><p>9_1</p>
<p>9_3</p>
<p>9_3</p>
<p>9_3</p>
<p>9_3</p>
<p>9_3</p>
<p>9_3</p></td>
</tr>
<tr class="even">
<td align="left">D3DDECLTYPE_UBYTE4</td>
<td align="left">R8G8B8A8_UINT</td>
<td align="left"><p>IA_VERTEX_BUFFER</p></td>
<td align="left"><p>9_1</p></td>
</tr>
<tr class="odd">
<td align="left">A8R8G8B8 或 D3DDECLTYPE_UBYTE4N</td>
<td align="left">R8G8B8A8_UNORM</td>
<td align="left"><p>IA_VERTEX_BUFFER</p>
<p>TEXTURE2D</p>
<p>TEXTURE3D</p>
<p>TEXTURECUBE</p>
<p>SHADER_LOAD</p>
<p>SHADER_SAMPLE</p>
<p>MIP</p>
<p>MIP_AUTOGEN</p>
<p>RENDER_TARGET</p>
<p>BLENDABLE</p>
<p>CPU_LOCKABLE</p>
<p>DISPLAY</p>
<p>BACK_BUFFER_CAST</p></td>
<td align="left"><p>9_1</p>
<p>9_1</p>
<p>9_1</p>
<p>9_1</p>
<p>9_1</p>
<p>9_1</p>
<p>9_1</p>
<p>9_1</p>
<p>9_1</p>
<p>9_1</p>
<p>9_1</p>
<p>9_1</p>
<p>9_1</p></td>
</tr>
<tr class="even">
<td align="left">A8R8G8B8</td>
<td align="left">R8G8B8A8_UNORM_SRGB</td>
<td align="left"><p>TEXTURE2D</p>
<p>TEXTURE3D</p>
<p>TEXTURECUBE</p>
<p>SHADER_LOAD</p>
<p>SHADER_SAMPLE</p>
<p>MIP</p>
<p>MIP_AUTOGEN</p>
<p>RENDER_TARGET</p>
<p>BLENDABLE</p>
<p>CPU_LOCKABLE</p>
<p>DISPLAY</p>
<p>BACK_BUFFER_CAST</p></td>
<td align="left"><p>9_1</p>
<p>9_1</p>
<p>9_1</p>
<p>9_1</p>
<p>9_1</p>
<p>9_1</p>
<p>9_1</p>
<p>9_1</p>
<p>9_1</p>
<p>9_1</p>
<p>9_1</p>
<p>9_1</p></td>
</tr>
<tr class="odd">
<td align="left">Q8W8V8U8</td>
<td align="left">R8G8B8A8_SNORM</td>
<td align="left"><p>TEXTURE2D</p>
<p>TEXTURECUBE</p>
<p>SHADER_LOAD</p>
<p>SHADER_SAMPLE</p>
<p>MIP</p>
<p>CPU_LOCKABLE</p></td>
<td align="left"><p>9_1</p>
<p>9_1</p>
<p>9_1</p>
<p>9_1</p>
<p>9_1</p>
<p>9_1</p></td>
</tr>
<tr class="even">
<td align="left">A8R8G8B8</td>
<td align="left">B8G8R8A8_UNORM</td>
<td align="left"><p>TEXTURE2D</p>
<p>TEXTURE3D</p>
<p>TEXTURECUBE</p>
<p>SHADER_LOAD</p>
<p>SHADER_SAMPLE</p>
<p>MIP</p>
<p>MIP_AUTOGEN</p>
<p>RENDER_TARGET</p>
<p>BLENDABLE</p>
<p>CPU_LOCKABLE</p>
<p>DISPLAY</p>
<p>BACK_BUFFER_CAST</p></td>
<td align="left"><p>9_1</p>
<p>9_1</p>
<p>9_1</p>
<p>9_1</p>
<p>9_1</p>
<p>9_1</p>
<p>9_1</p>
<p>9_1</p>
<p>9_1</p>
<p>9_1</p>
<p>9_1</p>
<p>9_1</p></td>
</tr>
<tr class="odd">
<td align="left">X8R8G8B8</td>
<td align="left">B8G8R8X8_UNORM</td>
<td align="left"><p>TEXTURE2D</p>
<p>TEXTURE3D</p>
<p>TEXTURECUBE</p>
<p>SHADER_LOAD</p>
<p>SHADER_SAMPLE</p>
<p>MIP</p>
<p>MIP_AUTOGEN</p>
<p>RENDER_TARGET</p>
<p>BLENDABLE</p>
<p>CPU_LOCKABLE</p></td>
<td align="left"><p>9_1</p>
<p>9_1</p>
<p>9_1</p>
<p>9_1</p>
<p>9_1</p>
<p>9_1</p>
<p>9_1</p>
<p>9_1</p>
<p>9_1</p>
<p>9_1</p></td>
</tr>
<tr class="even">
<td align="left">A8R8G8B8</td>
<td align="left">B8G8R8A8_UNORM_SRGB</td>
<td align="left"><p>TEXTURE2D</p>
<p>TEXTURE3D</p>
<p>TEXTURECUBE</p>
<p>SHADER_LOAD</p>
<p>SHADER_SAMPLE</p>
<p>MIP</p>
<p>MIP_AUTOGEN</p>
<p>RENDER_TARGET</p>
<p>BLENDABLE</p>
<p>CPU_LOCKABLE</p>
<p>DISPLAY</p>
<p>BACK_BUFFER_CAST</p></td>
<td align="left"><p>9_1</p>
<p>9_1</p>
<p>9_1</p>
<p>9_1</p>
<p>9_1</p>
<p>9_1</p>
<p>9_1</p>
<p>9_1</p>
<p>9_1</p>
<p>9_1</p>
<p>9_1</p>
<p>9_1</p></td>
</tr>
<tr class="odd">
<td align="left">X8R8G8B8</td>
<td align="left">B8G8R8X8_UNORM_SRGB</td>
<td align="left"><p>TEXTURE2D</p>
<p>TEXTURE3D</p>
<p>TEXTURECUBE</p>
<p>SHADER_LOAD</p>
<p>SHADER_SAMPLE</p>
<p>MIP</p>
<p>MIP_AUTOGEN</p>
<p>RENDER_TARGET</p>
<p>BLENDABLE</p>
<p>CPU_LOCKABLE</p></td>
<td align="left"><p>9_1</p>
<p>9_1</p>
<p>9_1</p>
<p>9_1</p>
<p>9_1</p>
<p>9_1</p>
<p>9_1</p>
<p>9_1</p>
<p>9_1</p>
<p>9_1</p></td>
</tr>
<tr class="even">
<td align="left">G16R16F 或 D3DDECLTYPE_FLOAT16_2</td>
<td align="left">R16G16_FLOAT</td>
<td align="left"><p>IA_VERTEX_BUFFER</p>
<p>TEXTURE2D</p>
<p>TEXTURE3D</p>
<p>TEXTURECUBE</p>
<p>SHADER_LOAD</p>
<p>MIP</p>
<p>MIP_AUTOGEN</p>
<p>RENDER_TARGET</p>
<p>CPU_LOCKABLE</p></td>
<td align="left"><p>9_3</p>
<p>9_2</p>
<p>9_2</p>
<p>9_2</p>
<p>9_2</p>
<p>9_2</p>
<p>9_2</p>
<p>9_2</p>
<p>9_2</p></td>
</tr>
<tr class="odd">
<td align="left">G16R16 或 D3DDECLTYPE_USHORT2N</td>
<td align="left">R16G16_UNORM</td>
<td align="left"><p>TEXTURE2D</p>
<p>TEXTURE3D</p>
<p>TEXTURECUBE</p>
<p>SHADER_LOAD</p>
<p>SHADER_SAMPLE</p>
<p>MIP</p>
<p>MIP_AUTOGEN</p>
<p>RENDER_TARGET</p>
<p>CPU_LOCKABLE</p></td>
<td align="left"><p>9_2</p>
<p>9_2</p>
<p>9_2</p>
<p>9_2</p>
<p>9_2</p>
<p>9_2</p>
<p>9_2</p>
<p>9_2</p>
<p>9_2</p></td>
</tr>
<tr class="even">
<td align="left">V16U16 或 D3DDECLTYPE_SHORT2N</td>
<td align="left">R16G16_SNORM</td>
<td align="left"><p>IA_VERTEX_BUFFER</p>
<p>TEXTURE2D</p>
<p>TEXTURE3D</p>
<p>TEXTURECUBE</p>
<p>SHADER_LOAD</p>
<p>SHADER_SAMPLE</p>
<p>MIP</p>
<p>CPU_LOCKABLE</p></td>
<td align="left"><p>9_1</p>
<p>9_1</p>
<p>9_2</p>
<p>9_2</p>
<p>9_1</p>
<p>9_2</p>
<p>9_1</p>
<p>9_1</p></td>
</tr>
<tr class="odd">
<td align="left">D3DDECLTYPE_SHORT2</td>
<td align="left">R16G16_SINT</td>
<td align="left"><p>IA_VERTEX_BUFFER</p></td>
<td align="left"><p>9_1</p></td>
</tr>
<tr class="even">
<td align="left">R32F 或 D3DDECLTYPE_FLOAT1</td>
<td align="left">R32_FLOAT</td>
<td align="left"><p>IA_VERTEX_BUFFER</p>
<p>TEXTURE2D</p>
<p>TEXTURE3D</p>
<p>TEXTURECUBE</p>
<p>SHADER_LOAD</p>
<p>MIP</p>
<p>MIP_AUTOGEN</p>
<p>RENDER_TARGET</p>
<p>CPU_LOCKABLE</p></td>
<td align="left"><p>9_1</p>
<p>9_2</p>
<p>9_2</p>
<p>9_2</p>
<p>9_2</p>
<p>9_2</p>
<p>9_2</p>
<p>9_2</p>
<p>9_2</p></td>
</tr>
<tr class="odd">
<td align="left"></td>
<td align="left">R32_UINT</td>
<td align="left"><p>IA_INDEX_BUFFER</p></td>
<td align="left"><p>9_1</p></td>
</tr>
<tr class="even">
<td align="left">S8D24 或 D24S8</td>
<td align="left">D24_UNORM_S8_UINT</td>
<td align="left"><p>TEXTURE2D</p>
<p>DEPTH_STENCIL</p></td>
<td align="left"><p>9_1</p>
<p>9_1</p></td>
</tr>
<tr class="odd">
<td align="left">L16</td>
<td align="left">R16_UNORM</td>
<td align="left"><p>TEXTURE2D</p>
<p>TEXTURE3D</p>
<p>TEXTURECUBE</p>
<p>SHADER_LOAD</p>
<p>SHADER_SAMPLE</p>
<p>MIP</p>
<p>CPU_LOCKABLE</p></td>
<td align="left"><p>9_2</p>
<p>9_2</p>
<p>9_2</p>
<p>9_2</p>
<p>9_2</p>
<p>9_2</p>
<p>9_2</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left">R16_UINT</td>
<td align="left"><p>IA_INDEX_BUFFER</p></td>
<td align="left"><p>9_1</p></td>
</tr>
<tr class="odd">
<td align="left">D16 或 D16_LOCKABLE</td>
<td align="left">D16_UNORM</td>
<td align="left"><p>TEXTURE2D</p>
<p>DEPTH_STENCIL</p></td>
<td align="left"><p>9_1</p>
<p>9_1</p></td>
</tr>
<tr class="even">
<td align="left">V8U8</td>
<td align="left">R8G8_SNORM</td>
<td align="left"><p>TEXTURE2D</p>
<p>SHADER_LOAD</p>
<p>SHADER_SAMPLE</p>
<p>MIP</p>
<p>CPU_LOCKABLE</p></td>
<td align="left"><p>9_1</p>
<p>9_1</p>
<p>9_1</p>
<p>9_1</p>
<p>9_1</p></td>
</tr>
<tr class="odd">
<td align="left">L8</td>
<td align="left">R8_UNORM</td>
<td align="left"><p>TEXTURE2D</p>
<p>TEXTURE3D</p>
<p>TEXTURECUBE</p>
<p>SHADER_LOAD</p>
<p>SHADER_SAMPLE</p>
<p>MIP</p>
<p>CPU_LOCKABLE</p></td>
<td align="left"><p>9_1</p>
<p>9_1</p>
<p>9_1</p>
<p>9_1</p>
<p>9_1</p>
<p>9_1</p>
<p>9_1</p></td>
</tr>
<tr class="even">
<td align="left">DXT1</td>
<td align="left">BC1_UNORM 或 BC1_UNORM_SRGB</td>
<td align="left"><p>TEXTURE2D</p>
<p>TEXTURECUBE</p>
<p>SHADER_LOAD</p>
<p>SHADER_SAMPLE</p>
<p>MIP</p>
<p>CPU_LOCKABLE</p></td>
<td align="left"><p>9_1</p>
<p>9_1</p>
<p>9_1</p>
<p>9_1</p>
<p>9_1</p>
<p>9_1</p></td>
</tr>
<tr class="odd">
<td align="left">DXT2</td>
<td align="left">BC2_UNORM 或 BC2_UNORM_SRGB</td>
<td align="left"><p>TEXTURE2D</p>
<p>TEXTURECUBE</p>
<p>SHADER_LOAD</p>
<p>SHADER_SAMPLE</p>
<p>MIP</p>
<p>CPU_LOCKABLE</p></td>
<td align="left"><p>9_1</p>
<p>9_1</p>
<p>9_1</p>
<p>9_1</p>
<p>9_1</p>
<p>9_1</p></td>
</tr>
<tr class="even">
<td align="left">DXT4</td>
<td align="left">BC3_UNORM 或 BC3_UNORM_SRGB</td>
<td align="left"><p>TEXTURE2D</p>
<p>TEXTURECUBE</p>
<p>SHADER_LOAD</p>
<p>SHADER_SAMPLE</p>
<p>MIP</p>
<p>CPU_LOCKABLE</p></td>
<td align="left"><p>9_1</p>
<p>9_1</p>
<p>9_1</p>
<p>9_1</p>
<p>9_1</p>
<p>9_1</p></td>
</tr>
</tbody>
</table>

 

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">必需 D3D10_ 或 D3D11_ FORMAT_SUPPORT_ 的枚举值</th>
<th align="left">Direct3D 10Level 9 中的支持算法</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>BACK_BUFFER_CAST</p></td>
<td align="left"><p>对于支持显示的任何格式，假定为 true。</p></td>
</tr>
<tr class="even">
<td align="left"><p>BLENDABLE</p></td>
<td align="left"><p>无 FORMATOP_NOALPHABLEND</p></td>
</tr>
<tr class="odd">
<td align="left"><p>CPU_LOCKABLE</p></td>
<td align="left"><p>假定值始终为 true。</p></td>
</tr>
<tr class="even">
<td align="left"><p>DISPLAY</p></td>
<td align="left"><p>硬编码。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>IA_VERTEX_BUFFER</p></td>
<td align="left"><p>D3DDTCAPS_ * (参阅注意。 ) </p></td>
</tr>
<tr class="even">
<td align="left"><p>MIP</p></td>
<td align="left"><p>无 FORMATOP_NOTEXCOORDWRAPNORMIP</p></td>
</tr>
<tr class="odd">
<td align="left"><p>MIP_AUTOGEN</p></td>
<td align="left"><p> (参阅 Note。 ) </p></td>
</tr>
<tr class="even">
<td align="left"><p>RENDER_TARGET</p></td>
<td align="left"><p>FORMATOP_OFFSCREEN_RENDERTARGET</p></td>
</tr>
<tr class="odd">
<td align="left"><p>SHADER_LOAD</p></td>
<td align="left"><p>假定为所有非深度格式。</p></td>
</tr>
<tr class="even">
<td align="left"><p>SHADER_SAMPLE</p></td>
<td align="left"><p> (参阅 Note。 ) </p></td>
</tr>
<tr class="odd">
<td align="left"><p>TEXTURE2D</p></td>
<td align="left"><p>FORMATOP_TEXTURE</p></td>
</tr>
<tr class="even">
<td align="left"><p>TEXTURE3D</p></td>
<td align="left"><p>FORMATOP_VOLUMETEXTURE</p></td>
</tr>
<tr class="odd">
<td align="left"><p>TEXTURECUBE</p></td>
<td align="left"><p>FORMATOP_CUBETEXTURE</p></td>
</tr>
</tbody>
</table>

 

**注意**   下面更详细地介绍了在 Direct3D 10Level 9 中支持算法的要求：
-   \_ \_ \_ \_ 如果没有 D3DDEVCAPS HWTRANSFORMANDLIGHT 功能，则软件顶点处理支持 ia 顶点缓冲区和/或 ia 索引缓冲区格式 \_ 。
-   还可以通过将 TEXTURE2D 格式推断为深度模具格式。
-   对于着色器 \_ 示例格式，驱动程序必须支持 FORMATOP \_ 纹理、FORMATOP \_ VOLUMETEXTURE 或 FORMATOP \_ CUBETEXTURE，并且它不能报告 FORMATOP \_ NOFILTER。
-   对于 MIP \_ AUTOGEN 格式，Direct3D 10Level 9 会生成自己的 mip 映射，因此它需要 mip、RENDER \_ TARGET 和 TEXTURE2D 位。

 

 

