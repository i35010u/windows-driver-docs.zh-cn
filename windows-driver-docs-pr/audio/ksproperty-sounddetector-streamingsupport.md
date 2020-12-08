---
title: KSPROPERTY \_ SOUNDDETECTOR \_ STREAMINGSUPPORT
description: KSPROPERTY \_ SOUNDDETECTOR \_ STREAMINGSUPPORT 属性指示流是否受支持。
keywords:
- KSPROPERTY_SOUNDDETECTOR_STREAMINGSUPPORT 音频设备
topic_type:
- apiref
api_name:
- KSPROPERTY_SOUNDDETECTOR_STREAMINGSUPPORT
api_location:
- ksmedia.h
api_type:
- HeaderDef
ms.date: 09/24/2019
ms.localizationpriority: medium
ms.openlocfilehash: 029de1a03094df0a6038d45d0d3b91a153c9197b
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96801169"
---
# <a name="ksproperty_sounddetector_streamingsupport"></a>KSPROPERTY \_ SOUNDDETECTOR \_ STREAMINGSUPPORT

**KSPROPERTY \_ SOUNDDETECTOR \_ STREAMINGSUPPORT** 属性指示流是否受支持。

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
<td align="left"><p><a href="/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-kssounddetectorproperty" data-raw-source="[&lt;strong&gt;KSSOUNDDETECTORPROPERTY&lt;/strong&gt;](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-kssounddetectorproperty)"><strong>KSSOUNDDETECTORPROPERTY</strong></a></p></td>
<td align="left"><p>BOOL</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idreturn_valuespanspan-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

属性值为布尔值，指示是否支持流式处理。

支持此读取属性并返回 false 的驱动程序，指示在没有相关突发音频流的情况下仅支持语音开始。

不支持此属性的驱动程序，或支持此属性并返回 true，这表示它支持对触发关键字检测的音频数据进行突发。

所有检测程序都必须支持缓冲和脉冲流式处理触发硬件关键字检测的音频数据，并使此请求失败，或将此值设置为 true。

<a name="remarks"></a>备注
-------
此属性供将来使用。 目前没有对检测程序的操作系统支持，这只是语音开始。

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
<td align="left"><p>Windows 10 版本1903</p></td>
</tr>
<tr class="odd">
<td align="left"><p>标头</p></td>
<td align="left">Ksmedia.h</td>
</tr>
</tbody>
</table>

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅

[**KSPROPERTY \_ SOUNDDETECTOR \_ 模式**](ksproperty-sounddetector-patterns.md)

[**KSSOUNDDETECTORPROPERTY**](/windows-hardware/drivers/ddi/ksmedia/)
