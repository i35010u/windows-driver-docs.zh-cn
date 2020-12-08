---
title: 帧速率转换模式
description: 帧速率转换模式
keywords:
- 帧速率转换 WDK DirectX VA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8a7c40423cdee64136bb347f803bdbb99fd99c7a
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96799703"
---
# <a name="frame-rate-conversion-modes"></a>帧速率转换模式


## <span id="ddk_frame_rate_conversion_modes_gg"></span><span id="DDK_FRAME_RATE_CONVERSION_MODES_GG"></span>


下面是 DDI 可支持的帧速率转换模式的示例。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">“模式”</th>
<th align="left">说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>帧重复/删除</p></td>
<td align="left"><p>这不是建议的模式，因为它通过将所选的源样本复制到目标图面来使用额外的内存。</p></td>
</tr>
<tr class="even">
<td align="left"><p>线性时态内插</p></td>
<td align="left"><p>将来的和以前的引用字段都混合在一起，以生成一个新帧。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>运动向量 Steered</p></td>
<td align="left"><p>场景中不同对象的运动向量用于在插值发生之前将各个运动与时间轴对齐。</p></td>
</tr>
</tbody>
</table>

 

 

 





