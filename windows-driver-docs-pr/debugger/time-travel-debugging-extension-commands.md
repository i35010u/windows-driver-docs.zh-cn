---
title: 调试扩展按时间顺序查看
description: 本部分介绍如何使用时间旅行调试器扩展命令。
ms.date: 09/22/2017
ms.localizationpriority: medium
ms.openlocfilehash: e46b66c7beb256c32a62c49617d65d5a0fe09c5c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56564345"
---
#  <a name="time-travel-debugging-extension-commands"></a>调试扩展命令按时间顺序查看

![显示时钟的较短时间的行程徽标](images/ttd-time-travel-debugging-logo.png)

本部分介绍时间旅行调试器扩展命令。


## <a name="span-idinthissectionspanin-this-section"></a><span id="in_this_section"></span>本部分中的内容


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
<td align="left"><p><a href="time-travel-debugging-extension-tt.md" data-raw-source="[&lt;strong&gt;!tt (time travel)&lt;/strong&gt;](time-travel-debugging-extension-tt.md)"><strong>！ tt （时程）</strong></a></p></td>
<td align="left"><p><a href="time-travel-debugging-extension-tt.md" data-raw-source="[&lt;strong&gt;!tt (time travel)&lt;/strong&gt;](time-travel-debugging-extension-tt.md)"> <strong>！ Tt （时程）</strong> </a>调试器扩展，可用于在时间中向前和向后导航。</p></td>

</tr>
<tr class="even">
<td align="left"><p><a href="time-travel-debugging-extension-positions.md" data-raw-source="[&lt;strong&gt;!positions&lt;/strong&gt;](time-travel-debugging-extension-positions.md)"><strong>!positions</strong></a></p></td>
<td align="left"><p><a href="time-travel-debugging-extension-positions.md" data-raw-source="[&lt;strong&gt;!positions&lt;/strong&gt;](time-travel-debugging-extension-positions.md)"> <strong>！ 位置</strong></a>扩展插件都会显示所有活动的线程，包括其时间旅行跟踪中的当前位置。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="time-travel-debugging-extension-index.md" data-raw-source="[&lt;strong&gt;!index&lt;/strong&gt;](time-travel-debugging-extension-index.md)"><strong>!index</strong></a></p></td>
<td align="left"><p><a href="time-travel-debugging-extension-index.md" data-raw-source="[&lt;strong&gt;!index&lt;/strong&gt;](time-travel-debugging-extension-index.md)"> <strong>！ 索引</strong></a>扩展索引按时间顺序查看跟踪或显示索引的状态信息。</p></td>
</tr>
</tbody>
</table>

### <a name="spanspan-idadditionalinformationspanadditional-information"></a></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

此扩展只适用于时间传输跟踪。 有关按时间顺序查看详细信息，请参阅[时间旅行调试-概述](time-travel-debugging-overview.md)。

### <a name="dll"></a>DLL

时间旅行命令实现 ttdext.dll 中的调试器扩展。 在 WinDbg 预览版中自动加载时间旅行命令 dll。 不需要使用负载命令手动加载 ttdext.dll。
 
## <a name="see-also"></a>请参阅

[按照时间顺序逐个调试-概述](time-travel-debugging-overview.md)

---






