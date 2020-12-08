---
title: KSPROPERTY \_ AUDIOENGINE \_ 环回 \_ 保护
description: KSPROPERTY \_ AUDIOENGINE \_ 环回 \_ protection 属性请求允许音频驱动程序设置音频引擎节点的环回保护状态。
keywords:
- KSPROPERTY_AUDIOENGINE_LOOPBACK_PROTECTION 音频设备
topic_type:
- apiref
api_name:
- KSPROPERTY_AUDIOENGINE_LOOPBACK_PROTECTION
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 232e7acd13e3ec37b50099332c830af602a121cc
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96798951"
---
# <a name="ksproperty_audioengine_loopback_protection"></a>KSPROPERTY \_ AUDIOENGINE \_ 环回 \_ 保护


**KSPROPERTY \_ AUDIOENGINE \_ 环回 \_ protection** 属性请求允许音频驱动程序设置音频引擎节点的环回保护状态。

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
<td align="left"><p>节点 via 引脚实例</p></td>
<td align="left"><p>KSP_NODE</p></td>
<td align="left"><p>ULONG</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idreturn_valuespanspan-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

KSPROPERTY \_ AUDIOENGINE \_ 环回 \_ PROTECTION 属性请求返回状态 SUCCESS，指示该请求已 \_ 成功完成。 否则，请求将返回相应的错误状态代码。

<a name="remarks"></a>备注
-------

与此属性调用关联的输入缓冲区使用类型 CONSTRICTOR 选项的枚举值进行填充 \_ 。 因此，输入缓冲区设置为 CONSTRICTOR 选项 " \_ \_ 禁用" 或 "CONSTRICTOR \_ 选项静音" \_ 。

如果有任何活动流的 CONSTRICTOR \_ 选项 \_ 静音有效，则此音频输出的 KS 环回将发出无声。 如果所有活动流都 \_ \_ (默认状态为 "禁用"，则此状态为 "") ，然后仅通过环回点击才能包含有意义的数据。

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
<td align="left"><p>Windows 8</p></td>
</tr>
<tr class="even">
<td align="left"><p>标头</p></td>
<td align="left">Ksmedia.h</td>
</tr>
</tbody>
</table>

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[**KSPROPERTY \_ AUDIOENGINE**](ksproperty-audioengine.md)

 

 






