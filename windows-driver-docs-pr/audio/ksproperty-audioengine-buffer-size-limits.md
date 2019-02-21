---
title: KSPROPERTY\_AUDIOENGINE\_缓冲区\_大小\_范围
description: KSPROPERTY\_AUDIOENGINE\_缓冲区\_大小\_范围属性指示对于给定的数据格式，在实例时它可以支持硬件音频引擎的缓冲区的最小值和最大大小调用。 以字节为单位指定缓冲区大小。
ms.assetid: 6A5DF24C-A328-4814-A410-2B1E13402A2B
keywords:
- KSPROPERTY_AUDIOENGINE_BUFFER_SIZE_RANGE 音频设备
topic_type:
- apiref
api_name:
- KSPROPERTY_AUDIOENGINE_BUFFER_SIZE_RANGE
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: c44a0b88eff0918068bbb961d729eadf37ed0cf5
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56541450"
---
# <a name="kspropertyaudioenginebuffersizerange"></a>KSPROPERTY\_AUDIOENGINE\_缓冲区\_大小\_范围


**KSPROPERTY\_AUDIOENGINE\_缓冲区\_大小\_范围**属性指示给定的数据可以支持硬件音频引擎的缓冲区的最小值和最大大小在实例时调用它的格式。 以字节为单位指定缓冲区大小。

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
<td align="left"><p>通过筛选器节点</p></td>
<td align="left"><p>KSP_NODE</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/hh450864" data-raw-source="[&lt;strong&gt;KSAUDIOENGINE_BUFFER_SIZE_RANGE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/hh450864)"><strong>KSAUDIOENGINE_BUFFER_SIZE_RANGE</strong></a></p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idreturnvaluespanspan-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

一个**KSPROPERTY\_AUDIOENGINE\_缓冲区\_大小\_范围**属性请求返回**状态\_成功**指示它已成功完成。 否则，请求将返回相应的错误状态代码。

<a name="remarks"></a>备注
-------

务必请注意，然后在调用方调用**KSPROPERTY\_AUDIOENGINE\_缓冲区\_大小\_范围**属性，调用方的字段中填充[**KSDATAFORMAT\_WAVEFORMATEX** ](https://msdn.microsoft.com/library/windows/hardware/ff537095)结构。 因此，在**KSPROPERTY\_AUDIOENGINE\_缓冲区\_大小\_范围**调用时，音频驱动程序将收到 KSP\_节点和填充的**KSDATAFORMAT\_WAVEFORMATEX**从调用方的结构。 驱动程序使用此结构中的数据格式信息来确定最小值和最大缓冲区大小，以适应指定的数据格式。 在成功调用此属性，然后流式处理 (KS) 筛选器内核填写**MinBufferBytes**并**MaxBufferBytes**的字段[ **KSAUDIOENGINE\_缓冲区\_大小\_范围**](https://msdn.microsoft.com/library/windows/hardware/hh450864)结构。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>版本</p></td>
<td align="left"><p>Windows 8</p></td>
</tr>
<tr class="even">
<td align="left"><p>标头</p></td>
<td align="left">Ksmedia.h</td>
</tr>
</tbody>
</table>

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>另请参阅


[**KSAUDIOENGINE\_缓冲区\_大小\_范围**](https://msdn.microsoft.com/library/windows/hardware/hh450864)

[**KSDATAFORMAT\_WAVEFORMATEX**](https://msdn.microsoft.com/library/windows/hardware/ff537095)

[**KSPROPERTY\_AUDIOENGINE**](ksproperty-audioengine.md)

 

 






