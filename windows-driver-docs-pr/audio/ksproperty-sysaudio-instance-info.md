---
title: KSPROPERTY\_SYSAUDIO\_实例\_信息
description: KSPROPERTY\_SYSAUDIO\_实例\_属性打开虚拟的音频设备，以及指定该设备的配置标志的信息。
ms.assetid: ef60c188-704f-4dbb-bf6d-cdf3152c209b
keywords:
- KSPROPERTY_SYSAUDIO_INSTANCE_INFO 音频设备
topic_type:
- apiref
api_name:
- KSPROPERTY_SYSAUDIO_INSTANCE_INFO
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 14b94a5e0b8fd18fc689a7a18b0de9f1920b7d48
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63332608"
---
# <a name="kspropertysysaudioinstanceinfo"></a>KSPROPERTY\_SYSAUDIO\_实例\_信息


KSPROPERTY\_SYSAUDIO\_实例\_属性打开虚拟的音频设备，以及指定该设备的配置标志的信息。

## <span id="ddk_ksproperty_sysaudio_instance_info_ks"></span><span id="DDK_KSPROPERTY_SYSAUDIO_INSTANCE_INFO_KS"></span>


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
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff538490" data-raw-source="[&lt;strong&gt;SYSAUDIO_INSTANCE_INFO&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff538490)"><strong>SYSAUDIO_INSTANCE_INFO</strong></a></p></td>
<td align="left"><p>无</p></td>
</tr>
</tbody>
</table>

 

属性描述符 （实例数据） 是一种结构的类型 SYSAUDIO\_实例\_指定哪些虚拟的音频设备，若要打开，并还指定该设备的配置标志的信息。

为此属性定义没有属性值 （操作数据）。 指定属性值指针视为**NULL**，和属性值的大小为零。

### <a name="span-idreturnvaluespanspan-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

KSPROPERTY\_SYSAUDIO\_实例\_信息属性请求将返回状态\_成功以指示已成功完成。 否则，请求将返回相应的错误状态代码。

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


[**SYSAUDIO\_INSTANCE\_INFO**](https://msdn.microsoft.com/library/windows/hardware/ff538490)

 

 






