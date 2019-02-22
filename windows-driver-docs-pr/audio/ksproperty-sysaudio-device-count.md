---
title: KSPROPERTY\_SYSAUDIO\_设备\_计数
description: KSPROPERTY\_SYSAUDIO\_设备\_COUNT 属性，检索指定的虚拟 DirectSound 应用程序具有可供选择的音频设备的数量计数。
ms.assetid: c70b6b5e-78fc-4f03-99cf-892297e592be
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
ms.openlocfilehash: 236fc2fe7e9d81780665dbcc0683c6b60adbb6f4
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56534302"
---
# <a name="kspropertysysaudiodevicecount"></a>KSPROPERTY\_SYSAUDIO\_设备\_计数


KSPROPERTY\_SYSAUDIO\_设备\_COUNT 属性，检索指定的虚拟 DirectSound 应用程序具有可供选择的音频设备的数量计数。

## <span id="ddk_ksproperty_sysaudio_device_count_ks"></span><span id="DDK_KSPROPERTY_SYSAUDIO_DEVICE_COUNT_KS"></span>


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
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff564262" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564262)"><strong>KSPROPERTY</strong></a></p></td>
<td align="left"><p>ULONG</p></td>
</tr>
</tbody>
</table>

 

属性值 （操作数据） 为 ULONG 变量 SysAudio 向其中写入指定的虚拟音频设备可供选择的数量计数。 如果枚举 SysAudio *n*虚拟音频设备，这些设备通过设备 Id 0 用来标识*n*-1。

### <a name="span-idreturnvaluespanspan-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

KSPROPERTY\_SYSAUDIO\_设备\_计数属性请求将返回状态\_成功以指示已成功完成。 否则，请求将返回相应的错误状态代码。

<a name="remarks"></a>备注
-------

SysAudio 枚举执行批呈现在系统中的每个已启用的硬件设备的唯一虚拟音频设备。 在每个实例中，虚拟音频设备组成的硬件设备， [KMixer 系统驱动程序](https://msdn.microsoft.com/library/windows/hardware/ff537039#kmixer-system-driver)，和其他音频组件。 DirectSound 应用程序选择特定的硬件设备通过选择虚拟的音频设备，其中包含硬件设备。

例如，如果三个音频卡插入到系统总线，每个都包含具有 WaveCyclic 或 WavePci 微型端口驱动程序的批呈现设备 SysAudio 枚举具有设备 Id 0、 1 和 2 的三个虚拟音频设备。

SysAudio 维护其类别 KSCATEGORY 下在系统注册表中的虚拟音频设备的列表\_音频\_设备。 此类别的 SysAudio 保留以独占方式供使用。 DirectSound 不直接访问虚拟音频设备的信息从系统注册表。 相反，它将查询 SysAudio 虚拟音频设备的属性。

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
<td align="left">Ksmedia.h （包括 Ksmedia.h）</td>
</tr>
</tbody>
</table>

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>另请参阅


[**KSPROPERTY**](https://msdn.microsoft.com/library/windows/hardware/ff564262)

 

 






