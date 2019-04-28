---
title: KSPROPERTY\_SYSAUDIO\_DEVICE\_INTERFACE\_NAME
description: KSPROPERTY\_SYSAUDIO\_设备\_接口\_名称属性检索包含指定的虚拟音频设备的即插设备接口名称的 Unicode 字符串。
ms.assetid: 0541ebb3-ad9a-42c6-9cd6-ea7b056821df
keywords:
- KSPROPERTY_SYSAUDIO_DEVICE_INTERFACE_NAME 音频设备
topic_type:
- apiref
api_name:
- KSPROPERTY_SYSAUDIO_DEVICE_INTERFACE_NAME
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6fba1c1651c31e6d8153122052343d96754b3499
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63332602"
---
# <a name="kspropertysysaudiodeviceinterfacename"></a>KSPROPERTY\_SYSAUDIO\_DEVICE\_INTERFACE\_NAME


KSPROPERTY\_SYSAUDIO\_设备\_接口\_名称属性检索包含指定的虚拟音频设备的即插设备接口名称的 Unicode 字符串。

## <span id="ddk_ksproperty_sysaudio_device_interface_name_ks"></span><span id="DDK_KSPROPERTY_SYSAUDIO_DEVICE_INTERFACE_NAME_KS"></span>


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
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff564262" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564262)"><strong>KSPROPERTY</strong></a>+ ULONG</p></td>
<td align="left"><p>LPWSTR</p></td>
</tr>
</tbody>
</table>

 

属性描述符 （实例数据） 包含后, 跟一个包含标识虚拟的音频设备的设备 ID 的 ULONG 变量的 KSPROPERTY 结构。 如果枚举 SysAudio *n*音频的虚拟设备 (请参阅[ **KSPROPERTY\_SYSAUDIO\_设备\_计数**](ksproperty-sysaudio-device-count.md))，然后有效设备 Id 的范围是从 0 到*n*-1。 此外，设备 ID 值为-1 可以是用来指示当前的设备，这最后一个虚拟的音频设备打开[ **KSPROPERTY\_SYSAUDIO\_设备\_实例**](ksproperty-sysaudio-device-instance.md)或[ **KSPROPERTY\_SYSAUDIO\_实例\_信息**](ksproperty-sysaudio-instance-info.md)集属性请求。

（操作数据） 的属性值是指向以 null 结尾的 Unicode 字符的字符串，它包含设备的接口名称。

### <a name="span-idreturnvaluespanspan-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

KSPROPERTY\_SYSAUDIO\_设备\_界面\_名称属性请求将返回状态\_成功以指示已成功完成。 否则，请求将返回相应的错误状态代码。

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


[**KSPROPERTY**](https://msdn.microsoft.com/library/windows/hardware/ff564262)

[**KSPROPERTY\_SYSAUDIO\_DEVICE\_COUNT**](ksproperty-sysaudio-device-count.md)

[**KSPROPERTY\_SYSAUDIO\_设备\_实例**](ksproperty-sysaudio-device-instance.md)

[**KSPROPERTY\_SYSAUDIO\_实例\_信息**](ksproperty-sysaudio-instance-info.md)

 

 






