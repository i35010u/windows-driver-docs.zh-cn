---
title: KSEVENT\_VIDCAP\_自动\_更新
description: 属性值更改时，将触发 KSEVENT\_VIDCAP\_自动\_UPDATE 事件。
ms.assetid: dd7e665f-104d-4276-94aa-62d64faba69d
keywords:
- KSEVENT_VIDCAP_AUTO_UPDATE 流媒体设备
topic_type:
- apiref
api_name:
- KSEVENT_VIDCAP_AUTO_UPDATE
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 22ee65eb06fa34f7995517ed3cfb0605157a6d19
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843675"
---
# <a name="ksevent_vidcap_auto_update"></a>KSEVENT\_VIDCAP\_自动\_更新


属性值更改时，将触发 KSEVENT\_VIDCAP\_自动\_UPDATE 事件。

## <span id="ddk_ksevent_vidcap_auto_update_ks"></span><span id="DDK_KSEVENT_VIDCAP_AUTO_UPDATE_KS"></span>


### <a name="span-idusage_summary_tablespanspan-idusage_summary_tablespanusage-summary-table"></a><span id="usage_summary_table"></span><span id="USAGE_SUMMARY_TABLE"></span>使用情况摘要表

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
<td><p>无</p></td>
<td><p>“是”</p></td>
<td><p>Filter</p></td>
<td><p><a href="https://docs.microsoft.com/previous-versions/ff561744(v=vs.85)" data-raw-source="[&lt;strong&gt;KSEVENT&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/ff561744(v=vs.85))"><strong>KSEVENT</strong></a></p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-kseventdata" data-raw-source="[&lt;strong&gt;KSEVENTDATA&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-kseventdata)"><strong>KSEVENTDATA</strong></a></p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

如果用户在设备上翻转交换机，并更改属性值，则客户端可能会注册此事件以获得通知。 要使此事件可用，硬件实现必须提供对此功能的支持。

有关 DirectShow 筛选器和 KsProxy 的详细信息，请参阅[内核流式处理代理](https://docs.microsoft.com/windows-hardware/drivers/ddi/_stream/index)。

 

 





