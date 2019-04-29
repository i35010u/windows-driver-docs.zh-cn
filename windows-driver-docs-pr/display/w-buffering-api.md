---
title: W 缓冲 API
description: W 缓冲 API
ms.assetid: 7244d697-5200-4d37-9a75-270788c1c7f7
keywords:
- Direct3D WDK Windows 2000 显示、 w 缓冲
- w 缓冲 WDK Direct3D
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 529757973552366f1b4b08bde1e18748bd296daf
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63391207"
---
# <a name="w-buffering-api"></a>W 缓冲 API


## <span id="ddk_w_buffering_api_gg"></span><span id="DDK_W_BUFFERING_API_GG"></span>


D3DRENDERSTATE\_ZENABLE 呈现状态支持从 D3DZBUFFERTYPE 枚举类型的三个设置。

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
<td align="left"><p>D3DZB_FALSE</p></td>
<td align="left"><p>禁用所有深度缓冲。</p></td>
</tr>
<tr class="even">
<td align="left"><p>D3DZB_TRUE</p></td>
<td align="left"><p>启用 z 缓冲区使用正确的角度来看<em>z</em>。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>D3DZB_USEW</p></td>
<td align="left"><p>禁用 z 缓冲，但可让 w 缓冲，这是关注相对<em>z</em>。</p></td>
</tr>
</tbody>
</table>

 

因为的确切格式用于存储*w*变化很大，那么应该假定是不透明。

图面上分配和深度填充操作的工作方式与使用 w 缓冲时。 所有的 z 缓冲区比较在任一情况下完全相同的模式工作。

有关详细信息，请参阅 DirectX SDK 文档。

 

 





