---
title: KSPROPERTY \_ SYSAUDIO \_ 组件 \_ ID
description: KSPROPERTY \_ SYSAUDIO \_ component \_ id 属性从指定的虚拟音频设备使用的声波渲染设备检索组件 id。
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
ms.openlocfilehash: ec9951690fcc4cd12293f15c56cb7a71cbffd531
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96801161"
---
# <a name="ksproperty_sysaudio_component_id"></a>KSPROPERTY \_ SYSAUDIO \_ 组件 \_ ID


KSPROPERTY \_ SYSAUDIO \_ component \_ id 属性从指定的虚拟音频设备使用的声波渲染设备检索组件 id。

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
<td align="left"><p><a href="/previous-versions/ff564262(v=vs.85)" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](/previous-versions/ff564262(v=vs.85))"><strong>KSPROPERTY</strong></a>+ ULONG</p></td>
<td align="left"><p><a href="/windows-hardware/drivers/ddi/ks/ns-ks-kscomponentid" data-raw-source="[&lt;strong&gt;KSCOMPONENTID&lt;/strong&gt;](/windows-hardware/drivers/ddi/ks/ns-ks-kscomponentid)"><strong>KSCOMPONENTID</strong></a></p></td>
</tr>
</tbody>
</table>

 

属性描述符 (实例数据) 是 KSPROPERTY 类型的结构，后跟一个 ULONG 变量，其中包含用于标识虚拟音频设备的设备 ID。 如果 SysAudio 枚举 *n* 个虚拟音频设备 (参阅 [**KSPROPERTY \_ SysAudio \_ 设备 \_ 计数**](ksproperty-sysaudio-device-count.md)) ，则有效的设备 id 范围介于0到 *n*-1 之间。

 (操作数据) 的属性值是 KSCOMPONENTID 类型的结构，该结构指定制造商、产品和其他特定于硬件的信息，这些信息与指定的虚拟音频设备使用的波形渲染设备有关。

### <a name="span-idreturn_valuespanspan-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

KSPROPERTY \_ SYSAUDIO \_ COMPONENT \_ ID 属性请求返回状态 \_ SUCCESS 以指示已成功完成。 否则，请求将返回相应的错误状态代码。

<a name="remarks"></a>备注
-------

DirectSound 不会直接与每个 SysAudio 的虚拟音频设备基础的音频硬件的微型端口驱动程序通信。 因此，DirectSound 无法直接在其组件 ID 信息中查询波形渲染设备。 KSPROPERTY \_ SYSAUDIO \_ COMPONENT \_ ID 属性提供一种方法，用于 DirectSound 通过 SYSAUDIO 间接获取此信息。

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

[**KSCOMPONENTID**](/windows-hardware/drivers/ddi/ks/ns-ks-kscomponentid)

[**KSPROPERTY \_ SYSAUDIO \_ 设备 \_ 计数**](ksproperty-sysaudio-device-count.md)

