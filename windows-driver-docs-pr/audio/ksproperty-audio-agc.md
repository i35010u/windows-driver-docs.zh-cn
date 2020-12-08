---
title: KSPROPERTY \_ 音频 \_ AGC
description: KSPROPERTY \_ AUDIO \_ AGC 属性指定 AGC 节点中通道的 AGC (自动增益控制)  (KSNODETYPE \_ AGC) 的状态。
keywords:
- KSPROPERTY_AUDIO_AGC 音频设备
topic_type:
- apiref
api_name:
- KSPROPERTY_AUDIO_AGC
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5adfee395102a56ebf79ace8d3ee176071993151
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96799077"
---
# <a name="ksproperty_audio_agc"></a>KSPROPERTY \_ 音频 \_ AGC


KSPROPERTY \_ AUDIO \_ AGC 属性指定 AGC 节点中通道的 AGC (自动增益控制)  ([**KSNODETYPE \_ AGC**](ksnodetype-agc.md)) 的状态。

## <span id="ddk_ksproperty_audio_agc_ks"></span><span id="DDK_KSPROPERTY_AUDIO_AGC_KS"></span>


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
<td align="left"><a href="/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksnodeproperty_audio_channel" data-raw-source="[&lt;strong&gt;KSNODEPROPERTY_AUDIO_CHANNEL&lt;/strong&gt;](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksnodeproperty_audio_channel)"><strong>KSNODEPROPERTY_AUDIO_CHANNEL</strong></a></td>
<td align="left"><p>BOOL</p></td>
</tr>
</tbody>
</table>

 

 (操作数据) 的属性值为 BOOL 类型，指示 AGC 是打开还是关闭。 如果值为 **TRUE** ，则表示 AGC 为 on。 **FALSE** 指示它已关闭。

### <a name="span-idreturn_valuespanspan-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

KSPROPERTY \_ 音频 \_ AGC 属性请求返回状态 " \_ 成功" 以指示它已成功完成。 否则，请求将返回相应的错误状态代码。

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


[**KSNODEPROPERTY \_ 音频 \_ 通道**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksnodeproperty_audio_channel)

[**KSNODETYPE \_ AGC**](ksnodetype-agc.md)

