---
title: 帧速率转换模式
description: 帧速率转换模式
ms.assetid: cbb609b5-6021-4f47-855d-24882533a7a0
keywords:
- 帧速率转换 WDK DirectX VA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e76a69528af4e9c8cfd84e27134db2a0185ad2da
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56540974"
---
# <a name="frame-rate-conversion-modes"></a>帧速率转换模式


## <span id="ddk_frame_rate_conversion_modes_gg"></span><span id="DDK_FRAME_RATE_CONVERSION_MODES_GG"></span>


以下是可以支持 DDI 的帧速率转换模式的示例。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">模式</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>帧重复/Drop</p></td>
<td align="left"><p>这不是一种建议的模式，因为它通过将所选的源示例复制到目标面使用额外的内存。</p></td>
</tr>
<tr class="even">
<td align="left"><p>临时的线性内插</p></td>
<td align="left"><p>Future 和上一个引用字段是 alpha 混合在一起以产生新帧。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>动作矢量 Steered</p></td>
<td align="left"><p>场景中的不同对象的动作矢量用于内插发生之前对齐单个移动到时间轴。</p></td>
</tr>
</tbody>
</table>

 

 

 





