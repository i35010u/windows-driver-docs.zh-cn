---
title: KSEVENT\_VIDCAP\_SEARCH
description: KSEVENT\_VIDCAP\_自动\_搜索完成后触发更新事件。
ms.assetid: 07c7ef26-4f88-40cf-84f2-14cc702f37d5
keywords:
- KSEVENT_VIDCAP_SEARCH 流式处理媒体设备
topic_type:
- apiref
api_name:
- KSEVENT_VIDCAP_SEARCH
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: ddb32ad312405eddbcb4a65e3f9e8871200ef608
ms.sourcegitcommit: f663c383886d87ea762e419963ff427500cc5042
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67393388"
---
# <a name="kseventvidcapsearch"></a>KSEVENT\_VIDCAP\_SEARCH


KSEVENT\_VIDCAP\_自动\_搜索完成后触发更新事件。

## <span id="ddk_ksevent_vidcap_search_ks"></span><span id="DDK_KSEVENT_VIDCAP_SEARCH_KS"></span>


### <a name="span-idusagesummarytablespanspan-idusagesummarytablespanusage-summary-table"></a><span id="usage_summary_table"></span><span id="USAGE_SUMMARY_TABLE"></span>使用率摘要表

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
<td><p>否</p></td>
<td><p>是</p></td>
<td><p>Filter</p></td>
<td><p><a href="https://docs.microsoft.com/previous-versions/ff561744(v=vs.85)" data-raw-source="[&lt;strong&gt;KSEVENT&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/ff561744(v=vs.85))"><strong>KSEVENT</strong></a></p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-kseventdata" data-raw-source="[&lt;strong&gt;KSEVENTDATA&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-kseventdata)"><strong>KSEVENTDATA</strong></a></p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

客户端可能会注册为搜索特定跟踪，例如，若要搜索完成后收到通知时此事件。

有关 DirectShow 筛选器和 KsProxy 详细信息请参阅[内核流式处理代理](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_stream/index)。

 

 





