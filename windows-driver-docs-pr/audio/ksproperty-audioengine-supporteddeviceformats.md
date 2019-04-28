---
title: KSPROPERTY\_AUDIOENGINE\_SUPPORTEDDEVICEFORMATS
description: KSPROPERTY\_AUDIOENGINE\_SUPPORTEDDEVICEFORMATS 属性请求检索硬件音频引擎所支持的设备格式。
ms.assetid: BF602B17-09E2-4003-95F8-CB45605EFA09
keywords:
- KSPROPERTY_AUDIOENGINE_SUPPORTEDDEVICEFORMATS 音频设备
topic_type:
- apiref
api_name:
- KSPROPERTY_AUDIOENGINE_SUPPORTEDDEVICEFORMATS
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 14f3ca98d9fc476975b35e30f57b3d40113ec2de
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63332805"
---
# <a name="kspropertyaudioenginesupporteddeviceformats"></a>KSPROPERTY\_AUDIOENGINE\_SUPPORTEDDEVICEFORMATS


**KSPROPERTY\_AUDIOENGINE\_SUPPORTEDDEVICEFORMATS**属性请求检索硬件音频引擎所支持的设备格式。

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
<td align="left"><p>一个<a href="https://msdn.microsoft.com/library/windows/hardware/ff563441" data-raw-source="[&lt;strong&gt;KSMULTIPLE_ITEM&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff563441)"> <strong>KSMULTIPLE_ITEM</strong> </a>结构后, 跟一系列<a href="https://msdn.microsoft.com/library/windows/hardware/ff537095" data-raw-source="[&lt;strong&gt;KSDATAFORMAT_WAVEFORMATEX&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff537095)"> <strong>KSDATAFORMAT_WAVEFORMATEX</strong> </a>结构</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idreturnvaluespanspan-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

**KSPROPERTY\_AUDIOENGINE\_SUPPORTEDDEVICEFORMATS**属性请求将返回**状态\_成功**以指示已成功完成. 否则，请求将返回相应的错误状态代码。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>Version</p></td>
<td align="left"><p>Windows 8</p></td>
</tr>
<tr class="even">
<td align="left"><p>Header</p></td>
<td align="left">Ksmedia.h</td>
</tr>
</tbody>
</table>

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>另请参阅


[**KSDATAFORMAT\_WAVEFORMATEX**](https://msdn.microsoft.com/library/windows/hardware/ff537095)

[**KSMULTIPLE\_项**](https://msdn.microsoft.com/library/windows/hardware/ff563441)

[**KSPROPERTY\_AUDIOENGINE**](ksproperty-audioengine.md)

[**KSPROPERTY\_AUDIOENGINE\_VOLUMELEVEL**](ksproperty-audioengine-volumelevel.md)

 

 






