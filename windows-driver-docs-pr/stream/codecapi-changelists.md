---
title: CODECAPI\_CHANGELISTS
description: CODECAPI\_CHANGELISTS
ms.assetid: c1b65350-32b9-4c94-a6d4-74cb9959d737
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 02d770e17b22135ab72a5f285c4d42e4d7c2a6b1
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844728"
---
# <a name="codecapi_changelists"></a>CODECAPI\_CHANGELISTS


## <span id="ddk_codecapi_changelists_ks"></span><span id="DDK_CODECAPI_CHANGELISTS_KS"></span>


CODECAPI\_CHANGELISTS 事件用于返回因属性 "set" 调用而发生更改的 Guid 的列表，例如[CODECAPI\_ALLSETTINGS](codecapi-allsettings.md)和[CODECAPI\_SETALLDEFAULTS](codecapi-setalldefaults.md)，或编码器设置属性。

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
<th>“获取”</th>
<th>设置</th>
<th>目标</th>
<th>事件描述符类型</th>
<th>事件值类型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>是（支持查询）</p></td>
<td><p>“是”</p></td>
<td><p>Filter</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-kse_node" data-raw-source="[&lt;strong&gt;KSE_NODE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-kse_node)"><strong>KSE_NODE</strong></a></p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-kseventdata" data-raw-source="[&lt;strong&gt;KSEVENTDATA&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-kseventdata)"><strong>KSEVENTDATA</strong></a></p></td>
</tr>
</tbody>
</table>

 

有关 DirectShow 筛选器和 KsProxy 的详细信息，请参阅[内核流式处理代理](https://docs.microsoft.com/windows-hardware/drivers/ddi/_stream/index)。

驱动程序使用 AVStream [**KsGenerateEvents**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-ksgenerateevents)发布更改的 guid 的列表。

### <a name="see-also"></a>另请参阅

[**KsGenerateEvents**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-ksgenerateevents)、 [CODECAPI\_ALLSETTINGS](codecapi-allsettings.md)、 [CODECAPI\_SETALLDEFAULTS](codecapi-setalldefaults.md)

 

 





