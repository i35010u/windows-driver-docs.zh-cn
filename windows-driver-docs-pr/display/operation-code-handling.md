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
ms.openlocfilehash: 42a7aaadd3f2dbeaf196e000e08d88538a9f9409
ms.sourcegitcommit: b3859d56cb393e698c698d3fb13519ff1522c7f3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57350068"
---
# <a name="operation-code-handling"></a>操作代码处理


## <span id="ddk_opcode_handling_gg"></span><span id="DDK_OPCODE_HANDLING_GG"></span>


显示驱动程序处理请求来呈现图形基元和流程中的状态更改其[ **D3dDrawPrimitives2** ](https://msdn.microsoft.com/library/windows/hardware/ff544704)函数。 该驱动程序将接收为这些请求[ **D3DHAL\_DP2OPERATION** ](https://msdn.microsoft.com/library/windows/hardware/ff545678)操作代码。 下面的主题介绍如何驱动程序处理操作代码以及如何在此类处理过程改进其性能：

[命令 Stream](command-stream.md)

[提高了操作处理的性能](improving-performance-of-operation-handling.md)

若要支持的 Microsoft DirectX 7.0 和更高版本的 Direct3D 驱动程序模型，驱动程序编写人员需要使响应在其实现中的新操作代码的许多其驱动程序[ **D3dDrawPrimitives2** ](https://msdn.microsoft.com/library/windows/hardware/ff544704). 这些操作代码的一些替换回调函数和其他人提供了新功能。 下表中，将为回调的总结了最重要的新操作代码。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">操作代码</th>
<th align="left">条件/说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>D3DDP2OP_SETRENDERTARGET</p></td>
<td align="left"><p><strong>始终要求。</strong> 映射的新呈现目标面和深度缓冲区当前上下文中。 将替换<em>D3dSetRenderTarget</em>。</p></td>
</tr>
<tr class="even">
<td align="left"><p>D3DDP2OP_CLEAR</p></td>
<td align="left"><p><strong>始终要求。</strong> 用于清除上下文的呈现器目标，Z 缓冲区。 将替换<em>D3dClear2</em>。 此外用于清除硬件模具缓冲区和深度填充位块传输不能正确清除的深度缓冲区。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>D3DDP2OP_SETPALETTE</p></td>
<td align="left"><p>用于映射调色板的句柄和图面上的句柄之间的关联和指定的调色板的特征。 仅需用于支持调色板纹理; 的驱动程序否则，这应该是 (NOP) 的任何操作。</p></td>
</tr>
<tr class="even">
<td align="left"><p>D3DDP2OP_UPDATEPALETTE</p></td>
<td align="left"><p>用于对进行的修改纹理调色板，支持调色板纹理的驱动程序。 否则，这应该是 NOP。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>D3DDP2OP_TEXBLT</p></td>
<td align="left"><p>指定从源纹理到目标纹理的 blt 操作。</p></td>
</tr>
</tbody>
</table>

 

 

 





