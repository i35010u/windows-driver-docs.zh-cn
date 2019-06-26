---
title: KSPROPERTY\_RTAUDIO\_查询\_通知\_支持
description: 客户端应用程序使用 KSPROPERTY\_RTAUDIO\_查询\_通知\_支持属性来确定是否音频驱动程序可以通知客户端应用程序时执行的进程完成提交的缓冲区。
ms.assetid: 7e0910df-4b76-4e61-9f88-8953860f3abe
keywords:
- KSPROPERTY_RTAUDIO_QUERY_NOTIFICATION_SUPPORT 音频设备
topic_type:
- apiref
api_name:
- KSPROPERTY_RTAUDIO_QUERY_NOTIFICATION_SUPPORT
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: c0bec65c2f7eb92fe4c8b1533828eba302cdbe1d
ms.sourcegitcommit: f663c383886d87ea762e419963ff427500cc5042
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67391653"
---
# <a name="kspropertyrtaudioquerynotificationsupport"></a>KSPROPERTY\_RTAUDIO\_查询\_通知\_支持


客户端应用程序使用`KSPROPERTY_RTAUDIO_QUERY_NOTIFICATION_SUPPORT`属性来确定是否音频驱动程序可以通知客户端应用程序时提交的缓冲区执行的进程完成。

### <a name="span-idusagesummarytablespanspan-idusagesummarytablespanspan-idusagesummarytablespanusage-summary-table"></a><span id="Usage_Summary_Table"></span><span id="usage_summary_table"></span><span id="USAGE_SUMMARY_TABLE"></span>使用率摘要表

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
<th align="left">Get</th>
<th align="left">设置</th>
<th align="left">目标</th>
<th align="left">属性描述符类型</th>
<th align="left">属性值类型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>是</p></td>
<td align="left"><p>否</p></td>
<td align="left"><p>Pin</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/ff564262(v=vs.85)" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/ff564262(v=vs.85))"><strong>KSPROPERTY</strong></a></p></td>
<td align="left"><p>BOOL</p></td>
</tr>
</tbody>
</table>

 

属性值为类型 BOOL 的变量。

### <a name="span-idreturnvaluespanspan-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

以响应`KSPROPERTY_RTAUDIO_QUERY_NOTIFICATION_SUPPORT`属性请求驱动程序将返回**TRUE**或**FALSE**值。 此值取决于驱动程序是否支持该属性。

<a name="remarks"></a>备注
-------

无

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>Version</p></td>
<td align="left"><p>在 Windows 7 和更高版本的 Windows 操作系统中可用。</p></td>
</tr>
<tr class="even">
<td align="left"><p>Header</p></td>
<td align="left">Ksmedia.h （包括 Ksmedia.h）</td>
</tr>
</tbody>
</table>

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>另请参阅


[**KSPROPERTY**](https://docs.microsoft.com/previous-versions/ff564262(v=vs.85))

 

 






