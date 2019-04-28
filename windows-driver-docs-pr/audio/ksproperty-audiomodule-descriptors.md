---
title: KSPROPERTY\_AUDIOMODULE\_描述符
description: KSPROPERTY\_AUDIOMODULE\_使用描述符到检索终结点批筛选器上的每个音频模块的静态数据描述符。
ms.assetid: EAD613AA-005B-4751-B60E-212853CA40B4
keywords:
- KSPROPERTY_AUDIOMODULE_DESCRIPTORS 音频设备
topic_type:
- apiref
api_name:
- KSPROPERTY_AUDIOMODULE_DESCRIPTORS
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 42fb8facd76b5bda28a8b8099ff9b5d2ec3c84d2
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63332787"
---
# <a name="kspropertyaudiomoduledescriptors"></a>KSPROPERTY\_AUDIOMODULE\_描述符


**KSPROPERTY\_AUDIOMODULE\_描述符**使用到检索终结点批筛选器上的每个音频模块的静态数据描述符。

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
<td align="left"><p>筛选器或 Pin</p></td>
<td align="left"><p><strong>KSPROPERTY</strong></p></td>
<td align="left"><p>对于筛选器目标后, 跟数组描述模板模块 KSAUDIOMODULE_DESCRIPTOR KSMULTIPLE_ITEM。</p>
<p>对于固定目标后, 跟数组 KSAUDIOMODULE_DESCRIPTOR 该流路径中的实例化模块 KSMULTIPLE_ITEM。</p></td>
</tr>
</tbody>
</table>

 

属性值是一种结构后, 跟零 (0) 或更多[ **KSAUDIOMODULE\_描述符**](https://msdn.microsoft.com/library/windows/hardware/mt808137)结构。

### <a name="span-idreturnvaluespanspan-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

**KSPROPERTY\_AUDIOMODULE\_描述符**返回到此请求的响应中返回这些描述符的数组。

如果该驱动程序支持此属性，但它不具有任何音频模块，它将返回 ksmultiple\_具有零个元素计数项。

有关音频模块的详细信息，请参阅[实现音频模块发现](https://msdn.microsoft.com/windows/hardware/drivers/audio/implementing-audio-module-communication)。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>最低受支持的客户端</p></td>
<td align="left"><p>Windows 10</p></td>
</tr>
<tr class="even">
<td align="left"><p>最低受支持的服务器</p></td>
<td align="left"><p>无受支持的版本</p></td>
</tr>
<tr class="odd">
<td align="left"><p>Version</p></td>
<td align="left"><p>Windows 10，版本 1703</p></td>
</tr>
</tbody>
</table>

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>另请参阅


[**KSAUDIOMODULE\_DESCRIPTOR**](https://msdn.microsoft.com/library/windows/hardware/mt808137)

[KSPROPSETID\_AudioModule](kspropsetid-audiomodule.md)

 

 






