---
title: KSPROPERTY\_SOUNDDETECTOR\_模式
description: KSPROPERTY\_SOUNDDETECTOR\_模式属性设置由操作系统来配置要检测到的关键字。
ms.assetid: 7A6AF4F6-5F5F-4A3D-AF61-B3E4374B33AD
keywords:
- KSPROPERTY_SOUNDDETECTOR_PATTERNS 音频设备
topic_type:
- apiref
api_name:
- KSPROPERTY_SOUNDDETECTOR_PATTERNS
api_location:
- ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 284a82ef6c11bc0faba44057de5c10735638fb03
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56577145"
---
# <a name="kspropertysounddetectorpatterns"></a>KSPROPERTY\_SOUNDDETECTOR\_模式


**KSPROPERTY\_SOUNDDETECTOR\_模式**操作系统设置属性来配置要检测到的关键字。

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
<td align="left"><p>否</p></td>
<td align="left"><p>是</p></td>
<td align="left"><p>Filter</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff564262" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564262)"><strong>KSPROPERTY</strong></a></p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff563441" data-raw-source="[&lt;strong&gt;KSMULTIPLE_ITEM&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff563441)"><strong>KSMULTIPLE_ITEM</strong></a></p></td>
</tr>
</tbody>
</table>

 

OS 设置关键字模式，或可能将此设置为空值。

OS 设置此属性，该驱动程序将自动 disarms 检测程序，如果以前了解。

如果该驱动程序不能满足"set"由于资源不足而请求，该驱动程序将会失败**状态\_不足\_资源**。

### <a name="span-idreturnvaluespanspan-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

属性值是[ **KSMULTIPLE\_项**](https://msdn.microsoft.com/library/windows/hardware/ff563441)结构后跟一系列 64 位对齐的检测模式。 每个模式开头[ **SOUNDDETECTOR\_PATTERNHEADER** ](https://msdn.microsoft.com/library/windows/hardware/dn957513)跟模式有效负载。

<a name="remarks"></a>备注
-------

驱动程序不应完成"设置"请求一直到：

-   检测程序位于已卸下和后续的"get"请求[ **KSPROPERTY\_SOUNDDETECTOR\_ARMED** ](ksproperty-sounddetector-armed.md)返回 false。
-   后续"get"请求[ **KSPROPERTY\_SOUNDDETECTOR\_MATCHRESULT** ](ksproperty-sounddetector-matchresult.md)不返回任何数据。
-   建立新的关键字模式和关键字检测程序操作上的新模式。

该驱动程序可能将挂起的请求，直至满足上述条件。 此外，如果设备需要可测量初始化时，驱动程序可能会保持挂起此请求之前设备已准备就绪，可以处理该请求。

OS 需要此行为，以避免争用条件之间检测到一个关键字和更新关键字模式 (例如如果检测到一个关键字和 KSEVENT\_SOUNDDETECTOR 生成即时 OS 更新关键字之前)。

OS 等待至少 2 秒才能完成此请求。

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
<td align="left"><p>Windows Server 2016</p></td>
</tr>
<tr class="odd">
<td align="left"><p>Header</p></td>
<td align="left">Ksmedia.h</td>
</tr>
</tbody>
</table>

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>另请参阅


[**SOUNDDETECTOR\_PATTERNHEADER**](https://msdn.microsoft.com/library/windows/hardware/dn957513)

[**SOUNDDETECTOR\_模式**](https://msdn.microsoft.com/library/windows/hardware/dn932155)

[**KSPROPERTY\_SOUNDDETECTOR\_ARMED**](ksproperty-sounddetector-armed.md)

[**KSPROPERTY\_SOUNDDETECTOR\_MATCHRESULT**](ksproperty-sounddetector-matchresult.md)

[**KSPROPERTY**](https://msdn.microsoft.com/library/windows/hardware/ff564262)

[**KSMULTIPLE\_项**](https://msdn.microsoft.com/library/windows/hardware/ff563441)

 

 






