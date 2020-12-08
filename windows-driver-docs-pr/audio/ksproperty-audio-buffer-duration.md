---
title: KSPROPERTY \_ 音频 \_ 缓冲区 \_ 持续时间
description: KSPROPERTY \_ AUDIO \_ BUFFER \_ DURATION 属性允许将客户端应用程序缓冲区的大小报告为时间长度。
keywords:
- KSPROPERTY_AUDIO_BUFFER_DURATION 音频设备
topic_type:
- apiref
api_name:
- KSPROPERTY_AUDIO_BUFFER_DURATION
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 830c0e7165a375cf6b3edd2b9e67738cbb59f437
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96799073"
---
# <a name="ksproperty_audio_buffer_duration"></a>KSPROPERTY \_ 音频 \_ 缓冲区 \_ 持续时间


KSPROPERTY \_ AUDIO \_ BUFFER \_ DURATION 属性允许将客户端应用程序缓冲区的大小报告为时间长度。

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
<td align="left"><p>否</p></td>
<td align="left"><p>是</p></td>
<td align="left"><p>Pin</p></td>
<td align="left"><p>KSPROPERTY</p></td>
<td align="left"><p>ULONG</p></td>
</tr>
</tbody>
</table>

 

属性值的类型为 ULONG，表示以毫秒为单位的客户端缓冲持续时间（以毫秒为单位）。

### <a name="span-idreturn_valuespanspan-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

KSPROPERTY \_ 音频 \_ 缓冲区 \_ 持续时间属性请求返回状态 \_ SUCCESS 以指示属性请求已成功完成。 否则，请求将返回相应的错误状态代码。

<a name="remarks"></a>备注
-------

可以调整对同步音频数据捕获请求的持续时间，以帮助提高 USB 音频设备的性能。 缩短的持续时间可减少延迟，但也意味着 USB 音频堆栈必须 (DPC) 进行更频繁的延迟过程调用，这可能会导致性能下降。

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
<td align="left"><p>在 windows 7 和更高版本的 Windows 中可用。</p></td>
</tr>
<tr class="even">
<td align="left"><p>标头</p></td>
<td align="left">Ksmedia (包含 Ksmedia) </td>
</tr>
</tbody>
</table>

 

 





