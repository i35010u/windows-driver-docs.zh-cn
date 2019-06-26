---
title: KSPROPERTY\_JACK\_SINK\_INFO
description: KSPROPERTY\_JACK\_接收器\_信息属性实现为可通过使用筛选器句柄的 pin-wise 属性。
ms.assetid: a51c03fa-91e4-49f2-ad76-35133c3b09ba
keywords:
- KSPROPERTY_JACK_SINK_INFO 音频设备
topic_type:
- apiref
api_name:
- KSPROPERTY_JACK_SINK_INFO
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: f2953da5c40634cca031f08691c337a44de140b6
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67354400"
---
# <a name="kspropertyjacksinkinfo"></a>KSPROPERTY\_JACK\_SINK\_INFO


KSPROPERTY\_JACK\_接收器\_信息属性实现为可通过使用筛选器句柄的 pin-wise 属性。

在 Windows 7 和更高版本操作系统中，可以在任何一个或多个物理插孔与相关联的桥插针上支持此属性。 KSPROPERTY\_JACK\_接收器\_信息用于获取描述和显示相关数字音频设备，例如 HDMI 设备或显示端口的插孔功能接收器。

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
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-_tagksjack_sink_information" data-raw-source="[&lt;strong&gt;KSJACK_SINK_INFORMATION&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-_tagksjack_sink_information)"><strong>KSJACK_SINK_INFORMATION</strong></a></p></td>
</tr>
</tbody>
</table>

 

属性值 （实例数据） 是 KSJACK\_接收器\_信息结构。

### <a name="span-idreturnvaluespanspan-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

KSPROPERTY\_JACK\_接收器\_信息属性请求返回中的信息**KSJACK\_接收器\_信息**结构。

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
<td align="left"><p>Windows 7</p></td>
</tr>
<tr class="even">
<td align="left"><p>最低受支持的服务器</p></td>
<td align="left"><p>Windows Server 2008</p></td>
</tr>
<tr class="odd">
<td align="left"><p>Header</p></td>
<td align="left">Ksmedia.h</td>
</tr>
</tbody>
</table>

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>另请参阅


[**KSJACK\_接收器\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-_tagksjack_sink_information)

 

 






