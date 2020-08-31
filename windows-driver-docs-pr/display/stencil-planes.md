---
title: 模具平面
description: 模具平面
ms.assetid: a2abe78b-7755-45fc-ba02-f2809db5da3e
keywords:
- Direct3D WDK Windows 2000 显示，模具平面
- 模具平面 WDK Direct3D
- 每像素绘制 WDK Direct3D
- 特殊效果 WDK Direct3D
- 几何图形渲染 WDK Direct3D
- 概述 WDK Direct3D
- 隐藏 WDK Direct3D
- decals WDK Direct3D
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e77dfa292ae53b2aa0ae521a8dc68aca27835528
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89063801"
---
# <a name="stencil-planes"></a>模具平面


## <span id="ddk_stencil_planes_gg"></span><span id="DDK_STENCIL_PLANES_GG"></span>


模具平面启用和禁用每个像素的绘图。 它们通常用于 multipass 算法，以实现特殊效果，如 decals、大纲显示、阴影和建设性的实体几何呈现。

旨在加速 Direct3D 实现模具平面的某些硬件。 模具平面启用的特殊效果对于娱乐应用程序很有用。

模具平面假设嵌入在 z 缓冲区数据中。

在 DirectX 5.0 中，应用程序使用 \_ [**D3DDEVICEDESC \_ V1**](/windows-hardware/drivers/ddi/d3dhal/ns-d3dhal-_d3ddevicedesc_v1)结构的**DWDEVICEZBUFFERBITDEPTH**成员中设置的 DDBD*Xx*标志找到可用的 z 缓冲区位深度。 若要支持不能使用现有的 DDBD Xx 标志表示的具有模具和 z 缓冲比特率的 z 缓冲区 \_ *Xx* ，DirectX 6.0 和更高版本具有新的 API 入口点， **IDirect3D7：： ENUMZBUFFERFORMATS** (在 Direct3D SDK 文档) 中介绍，后者返回描述可能的 z 缓冲/模具像素格式的 DDPIXELFORMAT 结构的数组。 [**DDPIXELFORMAT**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_ddpixelformat)结构包含以下与 z 缓冲区相关的新成员：

<span id="dwStencilBitDepth"></span><span id="dwstencilbitdepth"></span><span id="DWSTENCILBITDEPTH"></span>**dwStencilBitDepth**  
指定 (为整数的模具位数，而不是) 的 DDBD \_ *Xx*标志值。

<span id="dwZBitMask"></span><span id="dwzbitmask"></span><span id="DWZBITMASK"></span>**dwZBitMask**  
指定 z 值占用的位数。 如果为非零值，则此掩码意味着 z 缓冲区是标准的无符号整数 z 缓冲区格式。

<span id="dwStencilBitMask"></span><span id="dwstencilbitmask"></span><span id="DWSTENCILBITMASK"></span>**dwStencilBitMask**  
指定模具值占用的位数。

新标志 DDPF \_ STENCILBUFFER 指示 z 缓冲区内是否存在模具位。 之前存在的 **dwZBufferBitDepth** 成员提供包括模具位在内的 z 缓冲区的总数。

DirectX 6.0 和更高版本驱动程序仍应 \_ 在**dwDeviceZBufferBitDepth**中为其支持的仅 z z 缓冲区格式设置适当的 DDBD*Xx*标志。 如果不支持模具平面并且 DDBD \_ *Xx*标志可以表示所有可用的 z 缓冲区格式，则设置这些标志就足够了，因为这些标志通过**IDirect3D7：： EnumZBufferFormats**转换为 DDPIXELFORMAT。 否则，Direct3D 驱动程序必须响应使用 GUID ZPixelFormats GUID 的 [**DdGetDriverInfo**](/windows/desktop/api/ddrawint/nc-ddrawint-pdd_getdriverinfo) 查询，该查询 \_ 返回一个缓冲区，其中第一个 DWORD 指示有效 z 缓冲区 DDPIXELFORMAT 结构的数目，后跟 DDPIXELFORMAT 结构本身。

下表显示了与模具平面关联的新渲染状态，其中列出了渲染状态、与渲染状态的值相关联的类型，以及描述。 有关这些呈现状态的更多详细信息，请参阅 DirectX SDK 文档。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">呈现状态</th>
<th align="left">类型</th>
<th align="left">说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>D3DRENDERSTATE_STENCILFUNC</p></td>
<td align="left"><p>D3DCMPFUNC</p></td>
<td align="left"><p>比较函数。 如果以下表达式为 true，则测试通过：</p>
<p> (引用 & 掩码) 操作 (模具 & 掩码) 其中 <em>ref</em> 是引用值， <em>模具</em> 是模具缓冲区中的值， <em>掩码</em> 是 D3DRENDERSTATE_STENCILMASK 的值。</p></td>
</tr>
<tr class="even">
<td align="left"><p>D3DRENDERSTATE_STENCILREF</p></td>
<td align="left"><p>DWORD</p></td>
<td align="left"><p>模具测试中使用的引用值。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>D3DRENDERSTATE_STENCILMASK</p></td>
<td align="left"><p>DWORD</p></td>
<td align="left"><p>模具测试中使用的掩码值。</p></td>
</tr>
<tr class="even">
<td align="left"><p>D3DRENDERSTATE_STENCILWRITEMASK</p></td>
<td align="left"><p>DWORD</p></td>
<td align="left"><p>写入掩码，适用于写入到模具缓冲区的任何值。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>D3DRENDERSTATE_STENCILFAIL</p>
<p>D3DRENDERSTATE_STENCILZFAIL</p>
<p>D3DRENDERSTATE_STENCILPASS</p></td>
<td align="left"><p>D3DSTENCILOP</p></td>
<td align="left"><p>这些新的呈现状态分别定义为：在模具测试失败时，当模具测试通过但 z 测试失败时，以及当模具和 z 测试都通过时，通知硬件应执行的操作。 这些新呈现状态的值可以设置为 D3DSTENCILOP 枚举类型的枚举器，该枚举类型指定要执行的所需模具操作。 有关 D3DSTENCILOP 的详细信息，请参阅 DirectX SDK 文档。</p></td>
</tr>
</tbody>
</table>

 

 

