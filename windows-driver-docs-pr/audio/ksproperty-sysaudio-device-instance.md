---
title: KSPROPERTY \_ SYSAUDIO \_ 设备 \_ 实例
description: KSPROPERTY \_ SYSAUDIO \_ 设备 \_ 实例属性指定虚拟音频设备的当前实例。
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
ms.openlocfilehash: 6c5860e2f8c9e596c53f3e1062233dfbb8df241c
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89208913"
---
# <a name="ksproperty_sysaudio_device_instance"></a>KSPROPERTY \_ SYSAUDIO \_ 设备 \_ 实例


KSPROPERTY \_ SYSAUDIO \_ 设备 \_ 实例属性指定虚拟音频设备的当前实例。

## <span id="ddk_ksproperty_sysaudio_device_instance_ks"></span><span id="DDK_KSPROPERTY_SYSAUDIO_DEVICE_INSTANCE_KS"></span>


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
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/ff564262(v=vs.85)" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](/previous-versions/ff564262(v=vs.85))"><strong>KSPROPERTY</strong></a></p></td>
<td align="left"><p>ULONG</p></td>
</tr>
</tbody>
</table>

 

 (操作数据) 的属性值为 ULONG 类型，并指定虚拟音频设备的设备 ID。 如果 SysAudio 枚举 *n* 个虚拟音频设备 (参阅 [**KSPROPERTY \_ SysAudio \_ 设备 \_ 计数**](ksproperty-sysaudio-device-count.md)) ，则有效的设备 id 范围介于0到 *n*-1 之间。

### <a name="span-idreturn_valuespanspan-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

KSPROPERTY \_ SYSAUDIO \_ 设备 \_ 实例属性请求返回状态 " \_ 成功" 以指示已成功完成。 否则，请求将返回相应的错误状态代码。

<a name="remarks"></a>备注
-------

KSPROPERTY \_ SYSAUDIO \_ 设备 \_ 实例集-属性请求打开由属性值中包含的设备 ID 指定的虚拟音频设备。 最后一个要打开的设备称为 "当前设备"。

某些 SysAudio 属性允许使用空设备 ID-1 （而不是0到 *n*-1 范围内的有效设备 id）来标识当前设备，其中 *n* 是可用虚拟音频设备的数目。 这些属性包括 [**KSPROPERTY \_ SYSAUDIO \_ 设备 \_ 接口 \_ 名称**](ksproperty-sysaudio-device-interface-name.md) 和 [**KSPROPERTY \_ SYSAUDIO \_ 设备 \_ 友好 \_ 名称**](ksproperty-sysaudio-device-friendly-name.md)。

Get 属性请求检索当前 (的设备 ID，) 虚拟音频设备上一次打开。

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

[**KSPROPERTY \_ SYSAUDIO \_ 设备 \_ 接口 \_ 名称**](ksproperty-sysaudio-device-interface-name.md)

[**KSPROPERTY \_ SYSAUDIO \_ 设备 \_ 友好 \_ 名称**](ksproperty-sysaudio-device-friendly-name.md)

 

