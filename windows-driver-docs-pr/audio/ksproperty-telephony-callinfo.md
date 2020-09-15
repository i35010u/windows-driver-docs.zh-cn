---
title: KSPROPERTY \_ 电话服务 \_ CALLINFO
description: KSPROPERTY \_ 电话服务 \_ CALLINFO 属性用于检索当前调用信息，如调用状态和调用类型。
ms.assetid: EEBA38F6-86EC-4C2C-930C-A848153AD918
keywords:
- KSPROPERTY_TELEPHONY_CALLINFO 音频设备
topic_type:
- apiref
api_name:
- KSPROPERTY_TELEPHONY_CALLINFO
api_location:
- ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9b6cc03fd385b9476cb963a90960e864b246220c
ms.sourcegitcommit: 7500a03d1d57e95377b0b182a06f6c7dcdd4748e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "90101852"
---
# <a name="ksproperty_telephony_callinfo"></a>KSPROPERTY \_ 电话服务 \_ CALLINFO


**KSPROPERTY \_ 电话服务 \_ CALLINFO**属性用于检索当前调用信息，如调用状态和调用类型。

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
<td align="left"><p>筛选器</p></td>
<td align="left"><p><a href="/previous-versions/ff564262(v=vs.85)" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](/previous-versions/ff564262(v=vs.85))"><strong>KSPROPERTY</strong></a></p></td>
<td align="left"><p><a href="/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_tagkstelephony_callinfo" data-raw-source="[&lt;strong&gt;KSTELEPHONY_CALLINFO&lt;/strong&gt;](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_tagkstelephony_callinfo)"><strong>KSTELEPHONY_CALLINFO</strong></a></p></td>
</tr>
</tbody>
</table>

 

属性值的类型为 [**KSTELEPHONY \_ CALLINFO**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_tagkstelephony_callinfo)，它指定电话呼叫的状态和类型。

### <a name="span-idreturn_valuespanspan-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

**KSPROPERTY \_ 电话服务 \_ CALLINFO**属性请求返回[**KSTELEPHONY \_ CALLINFO**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_tagkstelephony_callinfo)结构，该结构包含用于启用、禁用、保留或在提供程序转换)  (启用、禁用、保留或在提供程序转换中的呼叫类型)  (。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>最低受支持的客户端</p></td>
<td align="left"><p>Windows 10</p></td>
</tr>
<tr class="even">
<td align="left"><p>最低受支持的服务器</p></td>
<td align="left"><p>无受支持的版本</p></td>
</tr>
<tr class="odd">
<td align="left"><p>客户端</p></td>
<td align="left"><p>Windows 10 移动版</p></td>
</tr>
<tr class="even">
<td align="left"><p>标头</p></td>
<td align="left">Ksmedia.h</td>
</tr>
</tbody>
</table>

