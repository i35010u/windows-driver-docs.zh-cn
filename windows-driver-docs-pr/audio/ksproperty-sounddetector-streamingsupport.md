---
title: KSPROPERTY\_SOUNDDETECTOR\_STREAMINGSUPPORT
description: KSPROPERTY\_SOUNDDETECTOR\_STREAMINGSUPPORT 属性指示流是否受支持。
ms.assetid: 3B9B43C0-31EE-4490-AD29-98DA81D1664E
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
ms.openlocfilehash: 7792fd58d77e3d481dba0b27520be4cf835c66a2
ms.sourcegitcommit: 8295a2b59212972b0f7457a748cc904b5417ad67
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/27/2019
ms.locfileid: "71329455"
---
# <a name="ksproperty_sounddetector_streamingsupport"></a>KSPROPERTY\_SOUNDDETECTOR\_STREAMINGSUPPORT

**KSPROPERTY\_SOUNDDETECTOR\_STREAMINGSUPPORT**属性指示流是否受支持。

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
<td align="left"><p>Filter</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-kssounddetectorproperty" data-raw-source="[&lt;strong&gt;KSSOUNDDETECTORPROPERTY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-kssounddetectorproperty"><strong>KSSOUNDDETECTORPROPERTY</strong></a></p></td>
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
<td align="left"><p>Header</p></td>
<td align="left">Ksmedia.h</td>
</tr>
</tbody>
</table>

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅

[**KSPROPERTY\_SOUNDDETECTOR\_模式**](ksproperty-sounddetector-patterns.md)

[**KSSOUNDDETECTORPROPERTY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/)
