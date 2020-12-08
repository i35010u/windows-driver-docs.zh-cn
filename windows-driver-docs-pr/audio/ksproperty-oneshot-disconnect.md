---
title: KSPROPERTY \_ ONESHOT \_ 断开连接
description: KSPROPERTY \_ ONESHOT \_ disconnect 属性用于提示音频驱动程序与蓝牙音频设备断开连接。
keywords:
- KSPROPERTY_ONESHOT_DISCONNECT 音频设备
topic_type:
- apiref
api_name:
- KSPROPERTY_ONESHOT_DISCONNECT
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: e30e7c2217a73e0c0503f1572ec2fd12c93ad9c7
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96801205"
---
# <a name="ksproperty_oneshot_disconnect"></a>KSPROPERTY \_ ONESHOT \_ 断开连接


**KSPROPERTY \_ ONESHOT \_ disconnect** 属性用于提示音频驱动程序与蓝牙音频设备断开连接。

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
<td align="left"><p>Null</p></td>
</tr>
</tbody>
</table>

 

没有与此属性请求一起发送的属性值。

### <a name="span-idreturn_valuespanspan-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

如果请求成功，则 **KSPROPERTY \_ ONESHOT \_ DISCONNECT** 属性返回状态 \_ 成功。

> [!NOTE]
> 成功的请求表示驱动程序尝试从蓝牙音频设备断开连接，但并不一定表示尝试成功。

 

<a name="remarks"></a>备注
-------

您可以在您的驱动程序中实现 [**KSPROPERTY \_ 插孔 \_ 说明**](ksproperty-jack-description.md) pin 属性。 此实现允许在进行 **KSPROPERTY \_ ONESHOT \_ 断开连接** 属性请求后检查终结点的连接状态。

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

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[**KSPROPERTY**](/previous-versions/ff564262(v=vs.85))

[**KSPROPERTY \_ 插孔 \_ 说明**](ksproperty-jack-description.md)

