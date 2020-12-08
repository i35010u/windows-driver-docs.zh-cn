---
title: KSPROPERTY \_ AUDIO \_ 多路分解器 \_ DEST
description: KSPROPERTY \_ AUDIO \_ 多路分解器 \_ DEST 属性指定信号分离器定向到其输入流的目标流。 这是多路分解器节点 (KSNODETYPE 多路分解器) 的属性 \_ 。
keywords:
- KSPROPERTY_AUDIO_DEMUX_DEST 音频设备
topic_type:
- apiref
api_name:
- KSPROPERTY_AUDIO_DEMUX_DEST
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9ad7bc84cfbf429417d274e896facdb52a28d62d
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96799045"
---
# <a name="ksproperty_audio_demux_dest"></a>KSPROPERTY \_ AUDIO \_ 多路分解器 \_ DEST


KSPROPERTY \_ AUDIO \_ 多路分解器 \_ DEST 属性指定信号分离器定向到其输入流的目标流。 这是多路分解器节点 ([**KSNODETYPE \_ 多路分解器**](ksnodetype-demux.md)) 的属性。

## <span id="ddk_ksproperty_audio_demux_dest_ks"></span><span id="DDK_KSPROPERTY_AUDIO_DEMUX_DEST_KS"></span>


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
<td align="left"><p>是</p></td>
<td align="left"><p>筛选器</p></td>
<td align="left"><p><a href="/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksnodeproperty" data-raw-source="[&lt;strong&gt;KSNODEPROPERTY&lt;/strong&gt;](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksnodeproperty)"><strong>KSNODEPROPERTY</strong></a></p></td>
<td align="left"><p>ULONG</p></td>
</tr>
</tbody>
</table>

 

 (操作数据) 的属性值为 ULONG 类型。 此值是多路分解器节点上所选输出插针的 pin ID。

### <a name="span-idreturn_valuespanspan-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

KSPROPERTY \_ 音频 \_ 多路分解器 \_ DEST 属性请求返回状态 " \_ 成功" 以指示该请求已成功完成。 否则，请求将返回相应的错误状态代码。

<a name="remarks"></a>备注
-------

Pin ID 标识多路分解器节点上的逻辑 pin。 有关筛选器内某个节点上的逻辑插针 Id 的讨论，请参阅 [**PCCONNECTION \_ 描述符**](/previous-versions/windows/hardware/drivers/ff537688(v=vs.85))。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>标头</p></td>
<td align="left">Ksmedia (包含 Ksmedia) </td>
</tr>
</tbody>
</table>

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[**KSNODETYPE \_ 多路分解器**](ksnodetype-demux.md)

[**KSNODEPROPERTY**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksnodeproperty)

[**PCCONNECTION \_ 描述符**](/previous-versions/windows/hardware/drivers/ff537688(v=vs.85))

