---
title: KSPROPERTY\_JACK\_说明
description: KSPROPERTY\_JACK\_DESCRIPTION 属性作为筛选器句柄可通过访问的多项、 pin-wise 属性。
ms.assetid: 005c7edc-8eb2-4387-b818-edef9b9dd4ee
keywords:
- KSPROPERTY_JACK_DESCRIPTION 音频设备
topic_type:
- apiref
api_name:
- KSPROPERTY_JACK_DESCRIPTION
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: c09565b3821b6b6850f9f2643645e5f822d0b153
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67360521"
---
# <a name="kspropertyjackdescription"></a>KSPROPERTY\_JACK\_说明


KSPROPERTY\_JACK\_DESCRIPTION 属性作为筛选器句柄可通过访问的多项、 pin-wise 属性。

在 Windows Vista 及更高版本，可以在任何一个或多个物理插孔与相关联的桥插针上支持此属性。 它用于获取物理特性的说明和使用情况的特定输入插孔。

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
<td align="left"><p>（通过筛选器句柄） 的 pin 工厂</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksp_pin" data-raw-source="[&lt;strong&gt;KSP_PIN&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksp_pin)"><strong>KSP_PIN</strong></a></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksmultiple_item" data-raw-source="[&lt;strong&gt;KSMULTIPLE_ITEM&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksmultiple_item)"><strong>KSMULTIPLE_ITEM</strong> </a>跟的数组<a href="ksjack-description.md" data-raw-source="[&lt;strong&gt;KSJACK_DESCRIPTION&lt;/strong&gt;](ksjack-description.md)"> <strong>KSJACK_DESCRIPTION</strong> </a>结构</p></td>
</tr>
</tbody>
</table>

 

属性值 （实例数据） 是 KSMULTIPLE\_项后, 跟数组 KSJACK\_描述结构。

### <a name="span-idreturnvaluespanspan-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

KSPROPERTY\_JACK\_说明属性请求返回 KSMULTIPLE\_项后跟一个数组*N* KSJACK\_描述结构，其中*N* = 插孔与指定的桥 pin 的数量。 属性请求返回的成员会因此可使用：

KSMULTIPLE\_项。大小 = sizeof (KSMULTIPLE\_项) + N \* sizeof (KSJACK\_说明)

KSMULTIPLE\_项。计数 = N

KSJACK\_说明\[0\]

...

KSJACK\_说明\[N-1\]

<a name="remarks"></a>备注
-------

每个 KSJACK\_描述结构必须具有一个 jack 有关的信息。 例如，支持 5.1 音频在三个立体声插孔，输出桥 pin 将要求数据缓冲区的大小

sizeof (KSMULTIPLE\_项) + 3 \* sizeof (KSJACK\_说明)

和每个 KSJACK\_描述结构有 two-bit ChannelMapping 值。

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
<td align="left"><p>Windows Vista</p></td>
</tr>
<tr class="even">
<td align="left"><p>最低受支持的服务器</p></td>
<td align="left"><p>Windows Server 2003</p></td>
</tr>
<tr class="odd">
<td align="left"><p>Header</p></td>
<td align="left">Ksmedia.h</td>
</tr>
</tbody>
</table>

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>另请参阅


[**KSJACK\_说明**](ksjack-description.md)

[KSMULTIPLE\_项](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksmultiple_item)

[KSPROPERTY](https://docs.microsoft.com/previous-versions/ff564262(v=vs.85))

 

 






