---
title: KSPROPERTY \_ SYSAUDIO \_ 设备 \_ 计数
description: KSPROPERTY \_ SYSAUDIO \_ 设备 \_ 计数属性检索指定 DirectSound 应用程序必须从中选择的虚拟音频设备数的计数。
keywords:
- KSPROPERTY_SYSAUDIO_DEVICE_COUNT 音频设备
topic_type:
- apiref
api_name:
- KSPROPERTY_SYSAUDIO_DEVICE_COUNT
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 791282d8ab11afb544783d7619073c524f75b30d
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96801157"
---
# <a name="ksproperty_sysaudio_device_count"></a>KSPROPERTY \_ SYSAUDIO \_ 设备 \_ 计数


KSPROPERTY \_ SYSAUDIO \_ 设备 \_ 计数属性检索指定 DirectSound 应用程序必须从中选择的虚拟音频设备数的计数。

## <span id="ddk_ksproperty_sysaudio_device_count_ks"></span><span id="DDK_KSPROPERTY_SYSAUDIO_DEVICE_COUNT_KS"></span>


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
<td align="left"><p><a href="/previous-versions/ff564262(v=vs.85)" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](/previous-versions/ff564262(v=vs.85))"><strong>KSPROPERTY</strong></a></p></td>
<td align="left"><p>ULONG</p></td>
</tr>
</tbody>
</table>

 

 (操作数据) 的属性值是一个 ULONG 变量，SysAudio 将指定要从中选择的虚拟音频设备数的计数。 如果 SysAudio 枚举 *n* 个虚拟音频设备，则这些设备由设备 id 0 到 *n*-1 标识。

### <a name="span-idreturn_valuespanspan-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

KSPROPERTY \_ SYSAUDIO \_ 设备 \_ 计数属性请求返回状态 " \_ 成功" 以指示它已成功完成。 否则，请求将返回相应的错误状态代码。

<a name="remarks"></a>备注
-------

SysAudio 为系统中每个启用了波形渲染功能的已启用硬件设备枚举唯一的虚拟音频设备。 在每个实例中，虚拟音频设备由硬件设备、 [KMixer 系统驱动程序](./kernel-mode-wdm-audio-components.md#kmixer-system-driver)和其他音频组件组成。 DirectSound 应用程序通过选择包含硬件设备的虚拟音频设备来选择特定硬件设备。

例如，如果将三个声卡插入系统总线，其中每个声卡都包含具有 WaveCyclic 或 WavePci 微型端口驱动程序的 wave 渲染设备，则 SysAudio 将使用设备 Id 为0、1和2的三个虚拟音频设备枚举。

SysAudio 在 KSCATEGORY 音频设备类别下的系统注册表中维护虚拟音频设备的 \_ 列表 \_ 。 此类别是专门为 SysAudio 使用而保留的。 DirectSound 不直接从系统注册表中访问有关虚拟音频设备的信息。 相反，它会在 SysAudio 中查询虚拟音频设备的属性。

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

