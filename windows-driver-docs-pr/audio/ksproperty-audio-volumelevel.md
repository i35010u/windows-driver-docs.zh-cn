---
title: KSPROPERTY \_ 音频 \_ VOLUMELEVEL
description: KSPROPERTY \_ AUDIO \_ VOLUMELEVEL 属性指定 (KSNODETYPE volume) 的卷节点中通道的音量级别 \_ 。
keywords:
- KSPROPERTY_AUDIO_VOLUMELEVEL 音频设备
topic_type:
- apiref
api_name:
- KSPROPERTY_AUDIO_VOLUMELEVEL
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8217d7619e134a45232c234454c0be69c64b4f7c
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96798977"
---
# <a name="ksproperty_audio_volumelevel"></a>KSPROPERTY \_ 音频 \_ VOLUMELEVEL


KSPROPERTY \_ AUDIO \_ VOLUMELEVEL 属性指定 ([**KSNODETYPE \_ volume**](ksnodetype-volume.md)) 的卷节点中通道的音量级别。

## <span id="ddk_ksproperty_audio_volumelevel_ks"></span><span id="DDK_KSPROPERTY_AUDIO_VOLUMELEVEL_KS"></span>


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
<td align="left"><p>节点 via 筛选器或固定实例</p></td>
<td align="left"><p><a href="/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksnodeproperty_audio_channel" data-raw-source="[&lt;strong&gt;KSNODEPROPERTY_AUDIO_CHANNEL&lt;/strong&gt;](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksnodeproperty_audio_channel)"><strong>KSNODEPROPERTY_AUDIO_CHANNEL</strong></a></p></td>
<td align="left"><p>LONG</p></td>
</tr>
</tbody>
</table>

 

属性值的类型为 LONG，指定给定流中通道的卷级别。 卷级值使用以下比例：

-2147483648 是-无限大 (衰减) ，

-2147483647 是-32767.99998474 分贝 (衰减) ，

+ 2147483647 为 + 32767.99998474 分贝 (获取) 。

> [!NOTE]
> 分贝范围由从-2147483648 到 + 2147483647 的整数值表示，其中此刻度的分辨率为1/65536 分贝。

 

如果在筛选器范围之外指定了某个值，则设置此属性的请求仍将成功。 但应用于筛选器的实际值只能由对此属性的后续调用来确定。

### <a name="span-idreturn_valuespanspan-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

KSPROPERTY \_ 音频 \_ VOLUMELEVEL 属性请求返回状态 " \_ 成功" 以指示它已成功完成。 否则，请求将返回相应的错误状态代码。

<a name="remarks"></a>备注
-------

此属性的属性描述符指定频道号。 如果通过卷节点传递的流包含 *n* 个通道，通道将从0到 *n*-1 进行编号。 有关详细信息，请参阅 [公开多通道节点](./exposing-multichannel-nodes.md)。

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


[自定义默认音频音量设置](./customizing-default-audio-volume-settings.md)

[默认的音频音量设置](./default-audio-volume-settings.md)

[**KSNODEPROPERTY \_ 音频 \_ 通道**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksnodeproperty_audio_channel)

[**KSNODETYPE \_ 卷**](ksnodetype-volume.md)

