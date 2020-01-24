---
title: 行程调试扩展
description: 本部分介绍如何使用行程调试器扩展命令。
ms.date: 09/22/2017
ms.localizationpriority: medium
ms.openlocfilehash: 838337a0fc9db255097d190ee383f6e0cc252c20
ms.sourcegitcommit: ee70846334ab6710ec0f9143e9f3a3754bc69f98
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/23/2020
ms.locfileid: "76706980"
---
# <a name="time-travel-debugging-extension-commands"></a>行程调试扩展命令

![显示时钟的小时间旅行徽标](images/ttd-time-travel-debugging-logo.png)

本部分介绍了旅行调试器扩展命令。

## <a name="span-idin_this_sectionspanin-this-section"></a><span id="in_this_section"></span>本部分内容

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">主题</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="time-travel-debugging-extension-tt.md" data-raw-source="[&lt;strong&gt;!tt (time travel)&lt;/strong&gt;](time-travel-debugging-extension-tt.md)"><strong>！ tt （行程）</strong></a></p></td>
<td align="left"><p>允许您在时间中向前和向后导航的<a href="time-travel-debugging-extension-tt.md" data-raw-source="[&lt;strong&gt;!tt (time travel)&lt;/strong&gt;](time-travel-debugging-extension-tt.md)"><strong>！ tt （时间段）</strong></a>调试器扩展。</p></td>

</tr>
<tr class="even">
<td align="left"><p><a href="time-travel-debugging-extension-positions.md" data-raw-source="[&lt;strong&gt;!positions&lt;/strong&gt;](time-travel-debugging-extension-positions.md)"><strong>！位置</strong></a></p></td>
<td align="left"><p><a href="time-travel-debugging-extension-positions.md" data-raw-source="[&lt;strong&gt;!positions&lt;/strong&gt;](time-travel-debugging-extension-positions.md)"><strong>！位置</strong></a>扩展显示所有活动线程，包括其在时间行程跟踪中的当前位置。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="time-travel-debugging-extension-index.md" data-raw-source="[&lt;strong&gt;!index&lt;/strong&gt;](time-travel-debugging-extension-index.md)"><strong>！索引</strong></a></p></td>
<td align="left"><p><a href="time-travel-debugging-extension-index.md" data-raw-source="[&lt;strong&gt;!index&lt;/strong&gt;](time-travel-debugging-extension-index.md)"><strong>！索引</strong></a>扩展索引时间段跟踪或显示索引状态信息。</p></td>
</tr>
</tbody>
</table>

### <a name="spanspan-idadditional_informationspanadditional-information"></a></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

此扩展仅适用于时间行程跟踪。 有关时间段的详细信息，请参阅[行程调试-概述](time-travel-debugging-overview.md)。

### <a name="dll"></a>DLL

在 ttdext 中实现了旅行调试器扩展命令。 时间段预览中自动加载了旅行命令 dll。 无需使用 load 命令手动加载 ttdext。
 
## <a name="see-also"></a>另请参阅

[行程调试-概述](time-travel-debugging-overview.md)
