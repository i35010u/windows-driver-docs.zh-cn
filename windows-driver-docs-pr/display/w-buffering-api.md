---
title: W 缓冲 API
description: W 缓冲 API
keywords:
- Direct3D WDK Windows 2000 显示，w-缓冲
- w-缓冲 WDK Direct3D
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5a4fd117ce7d0d0d72db6850d5e20610c7946cec
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96806325"
---
# <a name="w-buffering-api"></a>W 缓冲 API


## <span id="ddk_w_buffering_api_gg"></span><span id="DDK_W_BUFFERING_API_GG"></span>


D3DRENDERSTATE \_ ZENABLE render 状态支持 D3DZBUFFERTYPE 枚举类型中的三个设置。

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
<td align="left"><p>D3DZB_FALSE</p></td>
<td align="left"><p>禁用所有深度缓冲。</p></td>
</tr>
<tr class="even">
<td align="left"><p>D3DZB_TRUE</p></td>
<td align="left"><p>使用透视正确 <em>z</em>启用 z 缓冲区。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>D3DZB_USEW</p></td>
<td align="left"><p>禁用 z 缓冲，但启用 w-缓冲，即 "眼睛相对 <em>z</em>"。</p></td>
</tr>
</tbody>
</table>

 

因为用于存储 *w* 的准确格式差别很大，所以应将其视为不透明。

使用 w 缓冲时，表面分配和深度填充操作的工作方式相同。 所有 z 缓冲区比较模式在任何一种情况下都有效。

有关详细信息，请参阅 DirectX SDK 文档。

 

 





