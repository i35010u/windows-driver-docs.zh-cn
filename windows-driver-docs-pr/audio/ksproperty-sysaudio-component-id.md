---
title: KSPROPERTY\_SYSAUDIO\_COMPONENT\_ID
description: KSPROPERTY\_SYSAUDIO\_组件\_ID 属性从指定的虚拟音频设备使用的波次呈现设备中检索组件 ID。
ms.assetid: ef4a940f-dfef-43ed-8895-d318fb603e5c
keywords:
- KSPROPERTY_SYSAUDIO_COMPONENT_ID Audio Devices
topic_type:
- apiref
api_name:
- KSPROPERTY_SYSAUDIO_COMPONENT_ID
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: fc30eb87306be2f5e9b40ceb8aea16072f6ede15
ms.sourcegitcommit: f663c383886d87ea762e419963ff427500cc5042
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67391625"
---
# <a name="kspropertysysaudiocomponentid"></a>KSPROPERTY\_SYSAUDIO\_COMPONENT\_ID


KSPROPERTY\_SYSAUDIO\_组件\_ID 属性从指定的虚拟音频设备使用的波次呈现设备中检索组件 ID。

## <span id="ddk_ksproperty_sysaudio_component_id_ks"></span><span id="DDK_KSPROPERTY_SYSAUDIO_COMPONENT_ID_KS"></span>


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
<td align="left"><p>Filter</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/ff564262(v=vs.85)" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/ff564262(v=vs.85))"><strong>KSPROPERTY</strong></a>+ ULONG</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-kscomponentid" data-raw-source="[&lt;strong&gt;KSCOMPONENTID&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-kscomponentid)"><strong>KSCOMPONENTID</strong></a></p></td>
</tr>
</tbody>
</table>

 

属性描述符 （实例数据） 是类型 KSPROPERTY 跟包含标识虚拟的音频设备的设备 ID 的 ULONG 变量的结构。 如果枚举 SysAudio *n*音频的虚拟设备 (请参阅[ **KSPROPERTY\_SYSAUDIO\_设备\_计数**](ksproperty-sysaudio-device-count.md))，然后有效设备 Id 的范围是从 0 到*n*-1。

属性值 （操作数据） 为类型指定制造商、 产品和其他特定于硬件的信息批呈现设备，由指定的虚拟音频设备的 KSCOMPONENTID 的结构。

### <a name="span-idreturnvaluespanspan-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

KSPROPERTY\_SYSAUDIO\_组件\_ID 属性请求将返回状态\_成功以指示已成功完成。 否则，请求将返回相应的错误状态代码。

<a name="remarks"></a>备注
-------

DirectSound 不直接与提供的每个 SysAudio 的虚拟音频设备支持的音频硬件的微型端口驱动程序通信。 因此，DirectSound 是无法查询批呈现设备直接为其组件 ID 信息。 KSPROPERTY\_SYSAUDIO\_组件\_ID 属性提供了有关 DirectSound 获取此信息通过 SysAudio 间接方法。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>Header</p></td>
<td align="left">Ksmedia.h （包括 Ksmedia.h）</td>
</tr>
</tbody>
</table>

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>另请参阅


[**KSPROPERTY**](https://docs.microsoft.com/previous-versions/ff564262(v=vs.85))

[**KSCOMPONENTID**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-kscomponentid)

[**KSPROPERTY\_SYSAUDIO\_DEVICE\_COUNT**](ksproperty-sysaudio-device-count.md)

 

 






