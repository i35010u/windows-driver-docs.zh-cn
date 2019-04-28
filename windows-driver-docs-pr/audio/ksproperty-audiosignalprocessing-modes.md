---
title: KSPROPERTY\_AUDIOSIGNALPROCESSING\_模式
description: KSPROPERTY\_AUDIOSIGNALPROCESSING\_模式属性返回 pin 工厂所支持的音频信号处理模式的列表。
ms.assetid: 95536F80-D4E0-48CB-8DB2-603C4CEF0053
keywords:
- KSPROPERTY_AUDIOSIGNALPROCESSING_MODES 音频设备
topic_type:
- apiref
api_name:
- KSPROPERTY_AUDIOSIGNALPROCESSING_MODES
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 378c8d57eca8631826af6edb56be9af0797c3105
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63332793"
---
# <a name="kspropertyaudiosignalprocessingmodes"></a>KSPROPERTY\_AUDIOSIGNALPROCESSING\_模式


**KSPROPERTY\_AUDIOSIGNALPROCESSING\_模式**属性返回 pin 工厂所支持的音频信号处理模式的列表。

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
<td align="left"><p>（通过筛选器实例） 的 pin 工厂</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff566722.aspx" data-raw-source="[KSP_PIN](https://msdn.microsoft.com/library/windows/hardware/ff566722.aspx)">KSP_PIN</a></p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff563441.aspx" data-raw-source="[KSMULTIPLE_ITEM](https://msdn.microsoft.com/library/windows/hardware/ff563441.aspx)">KSMULTIPLE_ITEM</a></p></td>
</tr>
</tbody>
</table>

 

属性值是一个结构后, 跟零 (0) 或更多的 Guid。

### <a name="span-idreturnvaluespanspan-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

**KSPROPERTY\_AUDIOSIGNALPROCESSING\_模式**返回**KSMULTIPLE\_项**后跟零 (0) 或更多的 GUID。 KSMULTIPLE\_项。Count 成员包含的 Guid 数目。 KSMULTIPLE\_项。Size 成员包含的属性值的总大小。 每个 GUID 标识中指定的 Pin ID 的音频驱动程序所支持的信号处理模式*PinId*的成员**KSP\_PIN**结构。

在 Windows 8.1 中没有两个定义的音频信号处理模式，音频\_SIGNALPROCESSINGMODE\_默认值和音频\_SIGNALPROCESSINGMODE\_RAW。

在 Windows 10 中，定义五个其他模式。

音频\_SIGNALPROCESSINGMODE\_通信音频\_SIGNALPROCESSINGMODE\_语音音频\_SIGNALPROCESSINGMODE\_MEDIA 音频\_SIGNALPROCESSINGMODE\_电影音频\_SIGNALPROCESSINGMODE\_通知的详细信息，请参阅[音频信号处理模式](https://msdn.microsoft.com/windows/hardware/drivers/audio/audio-signal-processing-modes)。

<a name="remarks"></a>备注
-------

基本支持处理程序**KSPROPERTY\_AUDIOSIGNALPROCESSING\_模式**应传递给**KSP\_PIN**结构，以及是否应将播发仅支持在非环回流式处理的 pin。 音频驱动程序应仅在主机上支持信号处理模式和卸载的 pin。 环回或桥 pin 音频驱动程序应仍支持该属性，但返回**KSMULTIPLE\_项**结构，其*计数*参数设置为零 (0)。

开发使用 Microsoft 音频端口类驱动程序 (Portcls) 可以实现任何音频的微型端口驱动程序[ **IMiniportAudioSignalProcessing::GetModes** ](https://msdn.microsoft.com/library/windows/hardware/dn457660)方法。

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
<td align="left"><p>Windows 8.1</p></td>
</tr>
<tr class="even">
<td align="left"><p>Header</p></td>
<td align="left">Ksmedia.h</td>
</tr>
</tbody>
</table>

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>另请参阅


[**IMiniportAudioSignalProcessing::GetModes**](https://msdn.microsoft.com/library/windows/hardware/dn457660)

[KSMULTIPLE\_项](https://msdn.microsoft.com/library/windows/hardware/ff563441.aspx)

[KSP\_PIN](https://msdn.microsoft.com/library/windows/hardware/ff566722.aspx)

 

 






