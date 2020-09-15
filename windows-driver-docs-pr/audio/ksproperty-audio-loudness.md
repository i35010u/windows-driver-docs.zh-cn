---
title: KSPROPERTY \_ 音频 \_ 响度
description: KSPROPERTY \_ AUDIO \_ 响度属性指定是否为响度节点 (KSNODETYPE 响度) 中的通道启用或禁用响度 (总体动态范围和低音提升) \_ 。
ms.assetid: bc567e98-8a04-44f0-9ddf-7b71abf659a5
keywords:
- KSPROPERTY_AUDIO_LOUDNESS 音频设备
topic_type:
- apiref
api_name:
- KSPROPERTY_AUDIO_LOUDNESS
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1918ee3b79b4accd9a8d6b8b79371fff7c3d9242
ms.sourcegitcommit: 7500a03d1d57e95377b0b182a06f6c7dcdd4748e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "90102640"
---
# <a name="ksproperty_audio_loudness"></a>KSPROPERTY \_ 音频 \_ 响度


KSPROPERTY \_ AUDIO \_ 响度属性指定是否为响度节点 ([**KSNODETYPE \_ 响度**](ksnodetype-loudness.md)) 中的通道启用或禁用响度 (总体动态范围和低音提升) 。

## <span id="ddk_ksproperty_audio_loudness_ks"></span><span id="DDK_KSPROPERTY_AUDIO_LOUDNESS_KS"></span>


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
<td align="left"><p><a href="/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksnodeproperty_audio_channel" data-raw-source="[&lt;strong&gt;KSNODEPROPERTY_AUDIO_CHANNEL&lt;/strong&gt;](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksnodeproperty_audio_channel)"><strong>KSNODEPROPERTY_AUDIO_CHANNEL</strong></a></p></td>
<td align="left"><p>BOOL</p></td>
</tr>
</tbody>
</table>

 

 (操作数据) 的属性值为 BOOL 类型，指定是否打开或关闭响度。 如果值 **为 TRUE** ，则表示响度为 on。 **FALSE** 指示它已关闭。

### <a name="span-idreturn_valuespanspan-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

KSPROPERTY \_ 音频 \_ 响度属性请求返回状态 " \_ 成功" 以指示它已成功完成。 否则，请求将返回相应的错误状态代码。

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

[**KSNODETYPE \_ 响度**](ksnodetype-loudness.md)

