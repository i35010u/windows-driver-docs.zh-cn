---
title: CODECAPI\_包括
description: CODECAPI\_包括
ms.assetid: c1b65350-32b9-4c94-a6d4-74cb9959d737
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: be21fad3cd401a0cab02b8745f48905c15d72437
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386650"
---
# <a name="codecapichangelists"></a>CODECAPI\_包括


## <span id="ddk_codecapi_changelists_ks"></span><span id="DDK_CODECAPI_CHANGELISTS_KS"></span>


CODECAPI\_包括事件用于返回已因属性而更改的 Guid 列表"设置"调用，如[CODECAPI\_ALLSETTINGS](codecapi-allsettings.md)并[CODECAPI\_SETALLDEFAULTS](codecapi-setalldefaults.md)，或编码器设置属性。

<table>
<colgroup>
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
</colgroup>
<thead>
<tr class="header">
<th>Get</th>
<th>设置</th>
<th>目标</th>
<th>事件描述符类型</th>
<th>事件值类型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>是 （支持的查询）</p></td>
<td><p>是</p></td>
<td><p>Filter</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-kse_node" data-raw-source="[&lt;strong&gt;KSE_NODE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-kse_node)"><strong>KSE_NODE</strong></a></p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-kseventdata" data-raw-source="[&lt;strong&gt;KSEVENTDATA&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-kseventdata)"><strong>KSEVENTDATA</strong></a></p></td>
</tr>
</tbody>
</table>

 

有关 DirectShow 筛选器和 KsProxy 详细信息请参阅[内核流式处理代理](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_stream/index)。

驱动程序使用 AVStream [ **KsGenerateEvents** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nf-ks-ksgenerateevents)发布更改的 Guid 的列表。

### <a name="see-also"></a>请参阅

[**KsGenerateEvents**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nf-ks-ksgenerateevents)， [CODECAPI\_ALLSETTINGS](codecapi-allsettings.md)， [CODECAPI\_SETALLDEFAULTS](codecapi-setalldefaults.md)

 

 





