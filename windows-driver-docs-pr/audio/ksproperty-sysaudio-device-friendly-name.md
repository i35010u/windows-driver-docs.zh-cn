---
title: KSPROPERTY \_ SYSAUDIO \_ 设备 \_ 友好 \_ 名称
description: KSPROPERTY \_ SYSAUDIO \_ 设备 \_ 友好 \_ 名称属性检索包含虚拟音频设备友好名称的 Unicode 字符串。
ms.assetid: 14e23bb3-f0af-486f-8e34-fe27b2db2849
keywords:
- KSPROPERTY_SYSAUDIO_DEVICE_FRIENDLY_NAME 音频设备
topic_type:
- apiref
api_name:
- KSPROPERTY_SYSAUDIO_DEVICE_FRIENDLY_NAME
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4f49bcbb693e8d9e7f520e575fb8162800b4c109
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89211485"
---
# <a name="ksproperty_sysaudio_device_friendly_name"></a>KSPROPERTY \_ SYSAUDIO \_ 设备 \_ 友好 \_ 名称


KSPROPERTY \_ SYSAUDIO \_ 设备 \_ 友好 \_ 名称属性检索包含虚拟音频设备友好名称的 Unicode 字符串。

## <span id="ddk_ksproperty_sysaudio_device_friendly_name_ks"></span><span id="DDK_KSPROPERTY_SYSAUDIO_DEVICE_FRIENDLY_NAME_KS"></span>


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
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/ff564262(v=vs.85)" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](/previous-versions/ff564262(v=vs.85))"><strong>KSPROPERTY</strong></a>+ ULONG</p></td>
<td align="left"><p>LPWSTR</p></td>
</tr>
</tbody>
</table>

 

属性描述符 (实例数据) 包含一个 KSPROPERTY 结构，后跟一个 ULONG 变量，其中包含用于标识虚拟音频设备的设备 ID。 如果 SysAudio 枚举 *n* 个虚拟音频设备 (参阅 [**KSPROPERTY \_ SysAudio \_ 设备 \_ 计数**](ksproperty-sysaudio-device-count.md)) ，则有效的设备 id 范围介于0到 *n*-1 之间。 此外，设备 ID 值-1 可用于指示当前设备，这是由 [**KSPROPERTY \_ SYSAUDIO \_ 设备 \_ 实例**](ksproperty-sysaudio-device-instance.md) 或 [**KSPROPERTY \_ SYSAUDIO \_ 实例 \_ 信息**](ksproperty-sysaudio-instance-info.md)集请求打开的最后一个虚拟音频设备。

) 操作数据 (的属性值是一个指针，指向以 null 结尾的 Unicode 字符字符串，其中包含设备的友好名称。

### <a name="span-idreturn_valuespanspan-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

KSPROPERTY \_ SYSAUDIO \_ 设备 \_ 友好 \_ 名称属性请求返回状态 " \_ 成功" 以指示它已成功完成。 否则，请求将返回相应的错误状态代码。

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


[**KSPROPERTY**](/previous-versions/ff564262(v=vs.85))

[**KSPROPERTY \_ SYSAUDIO \_ 设备 \_ 计数**](ksproperty-sysaudio-device-count.md)

[**KSPROPERTY \_ SYSAUDIO \_ 设备 \_ 实例**](ksproperty-sysaudio-device-instance.md)

[**KSPROPERTY \_ SYSAUDIO \_ 实例 \_ 信息**](ksproperty-sysaudio-instance-info.md)

 

