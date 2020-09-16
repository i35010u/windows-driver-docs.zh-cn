---
title: KSPROPERTY \_ 插座 \_ \_ 信息
description: KSPROPERTY \_ 插座 \_ \_ 信息属性实现为使用筛选器句柄访问的按位数属性。
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
ms.openlocfilehash: c1f20b9b78811335b47c1b499b3b2ecd37c8b12a
ms.sourcegitcommit: 9b4760aae390b36dbdf9e0dd729a4a643c3f7831
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "90565247"
---
# <a name="ksproperty_jack_sink_info"></a>KSPROPERTY \_ 插座 \_ \_ 信息


KSPROPERTY \_ 插座 \_ \_ 信息属性实现为使用筛选器句柄访问的按位数属性。

在 Windows 7 及更高版本的操作系统中，与一个或多个物理插孔关联的任何桥接 pin 都可以支持此属性。 KSPROPERTY \_ 插孔 \_ 接收器 \_ 信息用于获取显示相关数字音频设备（如 HDMI 设备或显示器端口）的插孔接收器的说明和功能。

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
<td align="left"><p>通过筛选器句柄 (固定工厂) </p></td>
<td align="left"><p><a href="/windows-hardware/drivers/ddi/ks/ns-ks-ksp_pin" data-raw-source="[&lt;strong&gt;KSP_PIN&lt;/strong&gt;](/windows-hardware/drivers/ddi/ks/ns-ks-ksp_pin)"><strong>KSP_PIN</strong></a></p></td>
<td align="left"><p><a href="/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_tagksjack_sink_information" data-raw-source="[&lt;strong&gt;KSJACK_SINK_INFORMATION&lt;/strong&gt;](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_tagksjack_sink_information)"><strong>KSJACK_SINK_INFORMATION</strong></a></p></td>
</tr>
</tbody>
</table>

 

实例数据)  (属性值是 KSJACK \_ 接收器 \_ 信息结构。

### <a name="span-idreturn_valuespanspan-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

KSPROPERTY \_ 插座信息 \_ \_ 属性请求返回 **KSJACK \_ 接收器 \_ 信息** 结构中的信息。

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
<td align="left"><p>Windows 7</p></td>
</tr>
<tr class="even">
<td align="left"><p>最低受支持的服务器</p></td>
<td align="left"><p>Windows Server 2008</p></td>
</tr>
<tr class="odd">
<td align="left"><p>标头</p></td>
<td align="left">Ksmedia.h</td>
</tr>
</tbody>
</table>

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[**KSJACK \_ 接收器 \_ 信息**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_tagksjack_sink_information)

