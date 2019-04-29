---
title: 模具平面
description: 模具平面
ms.assetid: a2abe78b-7755-45fc-ba02-f2809db5da3e
keywords:
- Direct3D WDK Windows 2000 显示，模具平面
- 模具平面 WDK Direct3D
- 每个像素绘制 WDK Direct3D
- 特殊效果 WDK Direct3D
- WDK Direct3D 呈现的几何图形
- WDK Direct3D 的大纲显示
- 隐藏 WDK Direct3D
- 贴花纸 WDK Direct3D
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f9bd7aa7c8eecb2bd3e102e5524694d62a8233c4
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63376008"
---
# <a name="stencil-planes"></a>模具平面


## <span id="ddk_stencil_planes_gg"></span><span id="DDK_STENCIL_PLANES_GG"></span>


模具平面启用和禁用绘制每个像素。 它们通常用于在多通道算法中实现特殊效果，如贴花纸、 大纲显示、 阴影和建设性实体几何呈现。

旨在加快 Direct3D 实现模具平面某些硬件。 启用由模具平面特殊效果非常有用的娱乐应用程序。

假定模具平面嵌入在 z 缓冲区数据。

应用程序在 DirectX 5.0 中，找到可用的 z 缓冲区位深度使用 DDBD\_*Xx*设置标志**dwDeviceZBufferBitDepth**隶属[ **D3DDEVICEDESC\_V1** ](https://msdn.microsoft.com/library/windows/hardware/ff544689)结构。 若要支持 z 缓冲区模具和 z 缓冲区位深度不能使用现有 DDBD 表示\_*Xx*标志、 DirectX 6.0 和更高版本中有新的 API 入口点， **IDirect3D7::EnumZBufferFormats** （Direct3D SDK 文档中介绍），这会返回 DDPIXELFORMAT 结构描述可能 z 缓冲区/模具像素格式的数组。 [ **DDPIXELFORMAT** ](https://msdn.microsoft.com/library/windows/hardware/ff550274)结构包括以下新 z 缓冲区相关的成员：

<span id="dwStencilBitDepth"></span><span id="dwstencilbitdepth"></span><span id="DWSTENCILBITDEPTH"></span>**dwStencilBitDepth**  
指定模具比特数 (为整数，而不是作为 DDBD\_*Xx*标志值)。

<span id="dwZBitMask"></span><span id="dwzbitmask"></span><span id="DWZBITMASK"></span>**dwZBitMask**  
指定 z 值所占的位。 如果非零值，此掩码表示 z 缓冲区是一种标准化的无符号的整数 z 缓冲区格式。

<span id="dwStencilBitMask"></span><span id="dwstencilbitmask"></span><span id="DWSTENCILBITMASK"></span>**dwStencilBitMask**  
指定模具值所占的位。

新的标志，DDPF\_STENCILBUFFER，指示模具位 z 缓冲区中是否存在。 **DwZBufferBitDepth**成员，之前已存在，提供了 z 缓冲区位包括模具位的总数。

DirectX 6.0 和更高版本驱动程序仍应设置相应 DDBD\_*Xx*标记中**dwDeviceZBufferBitDepth**它们支持仅限 z z 缓冲区格式。 如果不支持模具平面和 DDBD\_*Xx*标志可以表示所有可用的 z 缓冲区格式，然后设置这些标志已足够，因为它们将转换为通过 DDPIXELFORMAT **IDirect3D7::EnumZBufferFormats**。 否则，Direct3D 驱动程序必须响应[ **DdGetDriverInfo** ](https://msdn.microsoft.com/library/windows/hardware/ff549404)查询使用 GUID\_ZPixelFormats GUID 通过返回的缓冲区中的第一个 dword 值指示的数目有效的 z 缓冲区 DDPIXELFORMAT 结构，跟 DDPIXELFORMAT 结构自身。

模具平面与相关联的新呈现状态将显示在下表列出了呈现状态，使用的呈现状态的值和说明关联的类型。 更多详细信息请参阅呈现状态，请参阅 DirectX SDK 文档。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">呈现器状态</th>
<th align="left">在任务栏的搜索框中键入</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>D3DRENDERSTATE_STENCILFUNC</p></td>
<td align="left"><p>D3DCMPFUNC</p></td>
<td align="left"><p>比较函数。 如果下面的表达式为 true，则测试通过：</p>
<p>(ref&amp;掩码) 操作 (模具&amp;掩码) 其中<em>ref</em>是引用值<em>模具</em>模具缓冲区中的值并<em>掩码</em>是D3DRENDERSTATE_STENCILMASK 的值。</p></td>
</tr>
<tr class="even">
<td align="left"><p>D3DRENDERSTATE_STENCILREF</p></td>
<td align="left"><p>DWORD</p></td>
<td align="left"><p>引用模具测试中使用的值。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>D3DRENDERSTATE_STENCILMASK</p></td>
<td align="left"><p>DWORD</p></td>
<td align="left"><p>模具测试中使用的掩码值。</p></td>
</tr>
<tr class="even">
<td align="left"><p>D3DRENDERSTATE_STENCILWRITEMASK</p></td>
<td align="left"><p>DWORD</p></td>
<td align="left"><p>写掩码应用于向模具缓冲区写入任何值。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>D3DRENDERSTATE_STENCILFAIL</p>
<p>D3DRENDERSTATE_STENCILZFAIL</p>
<p>D3DRENDERSTATE_STENCILPASS</p></td>
<td align="left"><p>D3DSTENCILOP</p></td>
<td align="left"><p>这些新的呈现状态，分别以通知有关要执行的操作时模具测试失败，硬件时模具测试通过，但 z 测试失败，和定义的模具和 z 测试时传递。 一种新的呈现状态的值可以设置为 D3DSTENCILOP 枚举类型的枚举器指定要执行的所需的模具操作。 有关 D3DSTENCILOP 详细信息，请参阅 DirectX SDK 文档。</p></td>
</tr>
</tbody>
</table>

 

 

 





