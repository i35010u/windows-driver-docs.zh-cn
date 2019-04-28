---
title: KSPROPERTY\_音频\_CPU\_资源
description: KSPROPERTY\_音频\_CPU\_资源属性指定是否在硬件中实现节点的功能，或在主机 CPU 运行的软件中模拟。
ms.assetid: 4379aa05-9661-44cd-8f10-0fb37009a4f3
keywords:
- KSPROPERTY_AUDIO_CPU_RESOURCES 音频设备
topic_type:
- apiref
api_name:
- KSPROPERTY_AUDIO_CPU_RESOURCES
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: b549a6bc2e32ab23fd3b999450b09e948c22fe39
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63333097"
---
# <a name="kspropertyaudiocpuresources"></a>KSPROPERTY\_音频\_CPU\_资源


KSPROPERTY\_音频\_CPU\_资源属性指定是否在硬件中实现节点的功能，或在主机 CPU 运行的软件中模拟。

## <span id="ddk_ksproperty_audio_cpu_resources_ks"></span><span id="DDK_KSPROPERTY_AUDIO_CPU_RESOURCES_KS"></span>


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
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff537143" data-raw-source="[&lt;strong&gt;KSNODEPROPERTY&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff537143)"><strong>KSNODEPROPERTY</strong></a></p></td>
<td align="left"><p>ULONG</p></td>
</tr>
</tbody>
</table>

 

（操作数据） 的属性值的类型为 ULONG，指示是否在硬件或软件中实现该节点的功能。 微型端口驱动程序从标头文件 Ksmedia.h 将此值设置为以下两个常量之一：

<span id="KSAUDIO_CPU_RESOURCES_HOST_CPU"></span><span id="ksaudio_cpu_resources_host_cpu"></span>KSAUDIO\_CPU\_RESOURCES\_HOST\_CPU  
此节点在主机 CPU 运行的软件中实现其功能。

<span id="KSAUDIO_CPU_RESOURCES_NOT_HOST_CPU"></span><span id="ksaudio_cpu_resources_not_host_cpu"></span>KSAUDIO\_CPU\_RESOURCES\_NOT\_HOST\_CPU  
此节点在硬件中实现其功能。

### <a name="span-idreturnvaluespanspan-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

KSPROPERTY\_音频\_CPU\_资源属性请求将返回状态\_成功以指示已成功完成。 否则，请求将返回相应的错误状态代码。

<a name="remarks"></a>备注
-------

此属性用于确定是否在硬件或软件中实现以下节点类型：

-   AEC 节点 ([**KSNODETYPE\_声学\_ECHO\_取消**](ksnodetype-acoustic-echo-cancel.md))

-   干扰禁止显示节点 ([**KSNODETYPE\_干扰\_禁止**](ksnodetype-noise-suppress.md))

-   Peakmeter 节点 ([**KSNODETYPE\_PEAKMETER**](ksnodetype-peakmeter.md))

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


[**KSNODEPROPERTY**](https://msdn.microsoft.com/library/windows/hardware/ff537143)

[**KSNODETYPE\_ACOUSTIC\_ECHO\_CANCEL**](ksnodetype-acoustic-echo-cancel.md)

[**KSNODETYPE\_干扰\_禁止**](ksnodetype-noise-suppress.md)

[**KSNODETYPE\_PEAKMETER**](ksnodetype-peakmeter.md)

 

 






