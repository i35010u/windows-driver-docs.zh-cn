---
title: KSPROPERTY \_ RTAUDIO \_ 查询 \_ 通知 \_ 支持
description: 客户端应用程序使用 KSPROPERTY \_ RTAUDIO \_ 查询 \_ 通知 \_ 支持属性来确定音频驱动程序是否可以在提交的缓冲区上执行的进程完成时通知客户端应用程序。
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
ms.openlocfilehash: 38547c412c05f14139d9af4077ea070d3c4097e6
ms.sourcegitcommit: 7500a03d1d57e95377b0b182a06f6c7dcdd4748e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "90101936"
---
# <a name="ksproperty_rtaudio_query_notification_support"></a>KSPROPERTY \_ RTAUDIO \_ 查询 \_ 通知 \_ 支持


客户端应用程序使用 `KSPROPERTY_RTAUDIO_QUERY_NOTIFICATION_SUPPORT` 属性来确定音频驱动程序是否可以在提交的缓冲区上执行的进程完成时通知客户端应用程序。

### <a name="span-idusage_summary_tablespanspan-idusage_summary_tablespanspan-idusage_summary_tablespanusage-summary-table"></a><span id="Usage_Summary_Table"></span><span id="usage_summary_table"></span><span id="USAGE_SUMMARY_TABLE"></span>使用情况摘要表

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
<th align="left">获取</th>
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
<td align="left"><p><a href="/previous-versions/ff564262(v=vs.85)" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](/previous-versions/ff564262(v=vs.85))"><strong>KSPROPERTY</strong></a></p></td>
<td align="left"><p>BOOL</p></td>
</tr>
</tbody>
</table>

 

属性值为 BOOL 类型的变量。

### <a name="span-idreturn_valuespanspan-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

为响应 `KSPROPERTY_RTAUDIO_QUERY_NOTIFICATION_SUPPORT` 属性请求，驱动程序将返回 **TRUE** 或 **FALSE** 值。 此值取决于驱动程序是否支持属性。

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
<td align="left"><p>版本</p></td>
<td align="left"><p>在 windows 7 和更高版本的 Windows 操作系统中可用。</p></td>
</tr>
<tr class="even">
<td align="left"><p>标头</p></td>
<td align="left">Ksmedia (包含 Ksmedia) </td>
</tr>
</tbody>
</table>

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[**KSPROPERTY**](/previous-versions/ff564262(v=vs.85))

