---
title: 操作代码处理
description: 操作代码处理
ms.assetid: 97de8370-316e-41df-bf27-1985af47a4e0
keywords:
- Direct3D WDK Windows 2000 显示，操作代码
- 操作代码 WDK Direct3D
- D3dDrawPrimitives2
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bd7ed5c7aaae8d0021529099d4749ca908c4ae26
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840500"
---
# <a name="operation-code-handling"></a>操作代码处理


## <span id="ddk_opcode_handling_gg"></span><span id="DDK_OPCODE_HANDLING_GG"></span>


显示驱动程序处理请求以呈现图形基元，并处理其[**D3dDrawPrimitives2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dhal/nc-d3dhal-lpd3dhal_drawprimitives2cb)函数中的状态更改。 驱动程序将这些请求作为[**D3DHAL\_DP2OPERATION**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dhal/ne-d3dhal-_d3dhal_dp2operation)操作代码接收。 以下主题介绍了驱动程序如何处理操作代码，以及在此类处理过程中如何提高其性能：

[命令流](command-stream.md)

[提高操作处理的性能](improving-performance-of-operation-handling.md)

为了支持 Microsoft DirectX 7.0 和更高版本的 Direct3D 驱动程序模型，驱动程序编写器需要使其驱动程序在其[**D3dDrawPrimitives2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dhal/nc-d3dhal-lpd3dhal_drawprimitives2cb)实现中响应多个新的操作代码。 其中一些操作代码替换回调函数，其他一些则提供新功能。 下表总结了最重要的新操作代码，从替换回叫的代码开始。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">操作代码</th>
<th align="left">条件/描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>D3DDP2OP_SETRENDERTARGET</p></td>
<td align="left"><p><strong>始终是必需的。</strong> 映射当前上下文中的新呈现目标图面和深度缓冲区。 替换<em>D3dSetRenderTarget</em>。</p></td>
</tr>
<tr class="even">
<td align="left"><p>D3DDP2OP_CLEAR</p></td>
<td align="left"><p><strong>始终是必需的。</strong> 用于清除上下文的呈现目标 Z 缓冲区。 替换<em>D3dClear2</em>。 还用于清除硬件模具缓冲区和深度填充位块传输无法正确清除的深度缓冲区。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>D3DDP2OP_SETPALETTE</p></td>
<td align="left"><p>用于映射调色板控点和图面控点之间的关联，并指定调色板的特征。 仅支持支持调色板纹理的驱动程序需要;否则，此操作不应为（NOP）。</p></td>
</tr>
<tr class="even">
<td align="left"><p>D3DDP2OP_UPDATEPALETTE</p></td>
<td align="left"><p>用于对支持调色板纹理的驱动程序进行更改纹理调色板。 否则，这应该是一个 NOP。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>D3DDP2OP_TEXBLT</p></td>
<td align="left"><p>指定从源纹理到目标纹理的 blt 操作。</p></td>
</tr>
</tbody>
</table>

 

 

 





