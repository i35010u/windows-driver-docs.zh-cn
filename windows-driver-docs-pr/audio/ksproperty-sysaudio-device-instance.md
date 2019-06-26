---
title: KSPROPERTY\_SYSAUDIO\_DEVICE\_INSTANCE
description: KSPROPERTY\_SYSAUDIO\_设备\_实例属性指定虚拟的音频设备的当前实例。
ms.assetid: 67cdc1ec-c696-454f-a3cc-1b50418c4056
keywords:
- KSPROPERTY_SYSAUDIO_DEVICE_INSTANCE 音频设备
topic_type:
- apiref
api_name:
- KSPROPERTY_SYSAUDIO_DEVICE_INSTANCE
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: d61c1abc32e6755d15df484c4ecc41e14ce30d0a
ms.sourcegitcommit: f663c383886d87ea762e419963ff427500cc5042
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67391609"
---
# <a name="kspropertysysaudiodeviceinstance"></a>KSPROPERTY\_SYSAUDIO\_DEVICE\_INSTANCE


KSPROPERTY\_SYSAUDIO\_设备\_实例属性指定虚拟的音频设备的当前实例。

## <span id="ddk_ksproperty_sysaudio_device_instance_ks"></span><span id="DDK_KSPROPERTY_SYSAUDIO_DEVICE_INSTANCE_KS"></span>


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
<td align="left"><p>是</p></td>
<td align="left"><p>Filter</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/ff564262(v=vs.85)" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/ff564262(v=vs.85))"><strong>KSPROPERTY</strong></a></p></td>
<td align="left"><p>ULONG</p></td>
</tr>
</tbody>
</table>

 

属性值 （操作数据） 是类型为 ULONG，指定虚拟的音频设备的设备 ID。 如果枚举 SysAudio *n*音频的虚拟设备 (请参阅[ **KSPROPERTY\_SYSAUDIO\_设备\_计数**](ksproperty-sysaudio-device-count.md))，然后有效设备 Id 的范围是从 0 到*n*-1。

### <a name="span-idreturnvaluespanspan-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

KSPROPERTY\_SYSAUDIO\_设备\_实例属性请求将返回状态\_成功以指示已成功完成。 否则，请求将返回相应的错误状态代码。

<a name="remarks"></a>备注
-------

KSPROPERTY\_SYSAUDIO\_设备\_实例设置属性请求打开指定的属性值中包含的设备 ID 的虚拟音频设备。 若要打开的最后一个设备称为当前设备。

对于某些 SysAudio 属性，可以标识由空设备 ID 为-1 而不是有效的设备 ID 在范围 0 到当前设备*n*-1，其中*n*是可用的虚拟音频设备的数目。 这些属性包括[ **KSPROPERTY\_SYSAUDIO\_设备\_接口\_名称**](ksproperty-sysaudio-device-interface-name.md)并[ **KSPROPERTY\_SYSAUDIO\_设备\_友好\_名称**](ksproperty-sysaudio-device-friendly-name.md)。

获取属性的请求检索的设备 ID （上一次打开） 的当前虚拟音频设备。

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

[**KSPROPERTY\_SYSAUDIO\_DEVICE\_COUNT**](ksproperty-sysaudio-device-count.md)

[**KSPROPERTY\_SYSAUDIO\_DEVICE\_INTERFACE\_NAME**](ksproperty-sysaudio-device-interface-name.md)

[**KSPROPERTY\_SYSAUDIO\_DEVICE\_FRIENDLY\_NAME**](ksproperty-sysaudio-device-friendly-name.md)

 

 






