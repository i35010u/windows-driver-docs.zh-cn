---
title: KSPROPERTY\_SYSAUDIO\_组件\_ID
description: KSPROPERTY\_SYSAUDIO\_组件\_ID 属性从指定的虚拟音频设备使用的声波渲染设备检索组件 ID。
ms.assetid: ef4a940f-dfef-43ed-8895-d318fb603e5c
keywords:
- KSPROPERTY_SYSAUDIO_COMPONENT_ID 音频设备
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
ms.openlocfilehash: da6fc58e40e98855adb888b9be714de6140ab3a9
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72830488"
---
# <a name="ksproperty_sysaudio_component_id"></a>KSPROPERTY\_SYSAUDIO\_组件\_ID


KSPROPERTY\_SYSAUDIO\_组件\_ID 属性从指定的虚拟音频设备使用的声波渲染设备检索组件 ID。

## <span id="ddk_ksproperty_sysaudio_component_id_ks"></span><span id="DDK_KSPROPERTY_SYSAUDIO_COMPONENT_ID_KS"></span>


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
<th align="left">“获取”</th>
<th align="left">设置</th>
<th align="left">目标</th>
<th align="left">属性描述符类型</th>
<th align="left">属性值类型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>“是”</p></td>
<td align="left"><p>无</p></td>
<td align="left"><p>Filter</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/ff564262(v=vs.85)" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/ff564262(v=vs.85))"><strong>KSPROPERTY</strong></a>+ ULONG</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-kscomponentid" data-raw-source="[&lt;strong&gt;KSCOMPONENTID&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-kscomponentid)"><strong>KSCOMPONENTID</strong></a></p></td>
</tr>
</tbody>
</table>

 

属性说明符（实例数据）是类型为 KSPROPERTY 的结构，后跟一个 ULONG 变量，其中包含用于标识虚拟音频设备的设备 ID。 如果 SysAudio 枚举*n*个虚拟音频设备（请参阅[**KSPROPERTY\_SysAudio\_设备\_计数**](ksproperty-sysaudio-device-count.md)），则有效的设备 id 范围介于0到*n*-1 之间。

属性值（操作数据）是 KSCOMPONENTID 类型的结构，它指定制造商、产品和其他特定于硬件的信息，这些信息与指定的虚拟音频设备使用的声波渲染设备有关。

### <a name="span-idreturn_valuespanspan-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

KSPROPERTY\_SYSAUDIO\_组件\_ID 属性请求返回状态\_"成功" 以指示已成功完成。 否则，请求将返回相应的错误状态代码。

<a name="remarks"></a>备注
-------

DirectSound 不会直接与每个 SysAudio 的虚拟音频设备基础的音频硬件的微型端口驱动程序通信。 因此，DirectSound 无法直接在其组件 ID 信息中查询波形渲染设备。 KSPROPERTY\_SYSAUDIO\_组件\_ID 属性为 DirectSound 提供了一种通过 SysAudio 间接获取此信息的方法。

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
<td align="left">Ksmedia （包括 Ksmedia）</td>
</tr>
</tbody>
</table>

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[**KSPROPERTY**](https://docs.microsoft.com/previous-versions/ff564262(v=vs.85))

[**KSCOMPONENTID**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-kscomponentid)

[**KSPROPERTY\_SYSAUDIO\_设备\_计数**](ksproperty-sysaudio-device-count.md)

 

 






