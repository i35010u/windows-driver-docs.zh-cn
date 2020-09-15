---
title: KSPROPERTY \_ ONESHOT \_ 重新连接
description: KSPROPERTY \_ ONESHOT \_ RECONNECT 属性用于提示音频驱动程序尝试连接到蓝牙音频设备。
ms.assetid: 54122a02-87e9-4953-aa78-4b9b31447a26
keywords:
- KSPROPERTY_ONESHOT_RECONNECT 音频设备
topic_type:
- apiref
api_name:
- KSPROPERTY_ONESHOT_RECONNECT
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2aaa21e3b2042c7879d3de89312290e7ec29cc22
ms.sourcegitcommit: 7500a03d1d57e95377b0b182a06f6c7dcdd4748e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "90101968"
---
# <a name="ksproperty_oneshot_reconnect"></a>KSPROPERTY \_ ONESHOT \_ 重新连接


**KSPROPERTY \_ ONESHOT \_ RECONNECT**属性用于提示音频驱动程序尝试连接到蓝牙音频设备。

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

如果请求成功，则 **KSPROPERTY \_ ONESHOT \_ 重新连接** 属性返回状态 " \_ 成功"。

> [!NOTE]
> 成功的请求意味着驱动程序尝试连接到 Bluetooth 音频设备，但并不一定表示尝试成功。

 

<a name="remarks"></a>备注
-------

您可以在您的驱动程序中实现 [**KSPROPERTY \_ 插孔 \_ 说明**](ksproperty-jack-description.md) pin 属性。 此实现允许在进行 **KSPROPERTY \_ ONESHOT \_ 重新连接** 属性请求后检查终结点的连接状态。

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

