---
title: KSPROPERTY\_AUDIOSIGNALPROCESSING\_模式
description: KSPROPERTY\_AUDIOSIGNALPROCESSING\_模式属性返回 pin 工厂支持的音频信号处理模式的列表。
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
ms.openlocfilehash: 06957e2014e3cb50f0d3a44b5d816cbaeea1c66e
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72830846"
---
# <a name="ksproperty_audiosignalprocessing_modes"></a>KSPROPERTY\_AUDIOSIGNALPROCESSING\_模式


**KSPROPERTY\_AUDIOSIGNALPROCESSING\_模式**属性返回 pin 工厂支持的音频信号处理模式的列表。

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
<th align="left">“获取”</th>
<th align="left">设置</th>
<th align="left">目标</th>
<th align="left">属性描述符类型</th>
<th align="left">属性值类型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>“是”</p></td>
<td align="left"><p>无</p></td>
<td align="left"><p>固定工厂（通过筛选器实例）</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksp_pin" data-raw-source="[KSP_PIN](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksp_pin)">KSP_PIN</a></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksmultiple_item" data-raw-source="[KSMULTIPLE_ITEM](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksmultiple_item)">KSMULTIPLE_ITEM</a></p></td>
</tr>
</tbody>
</table>

 

属性值为结构，后跟零（0）或更多 Guid。

### <a name="span-idreturn_valuespanspan-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

**KSPROPERTY\_AUDIOSIGNALPROCESSING\_模式**返回**KSMULTIPLE\_项**，后跟零（0）或更多 guid。 KSMULTIPLE\_项。Count 成员包含 Guid 的数目。 KSMULTIPLE\_项。Size 成员包含属性值的总大小。 每个 GUID 都为**KSP\_固定**结构的 KSP 成员的*PinId*成员中指定的 Pin ID 识别音频驱动程序所支持的信号处理模式。

在 Windows 8.1 有两种已定义的音频信号处理模式，音频\_SIGNALPROCESSINGMODE\_默认和音频\_SIGNALPROCESSINGMODE\_RAW。

在 Windows 10 中，定义了五种附加模式。

音频\_SIGNALPROCESSINGMODE\_通信音频\_SIGNALPROCESSINGMODE\_语音音频\_SIGNALPROCESSINGMODE\_MEDIA AUDIO\_SIGNALPROCESSINGMODE\_电影音频\_SIGNALPROCESSINGMODE\_通知有关详细信息，请参阅[音频信号处理模式](https://docs.microsoft.com/windows-hardware/drivers/audio/audio-signal-processing-modes)。

<a name="remarks"></a>备注
-------

适用于**KSPROPERTY\_AUDIOSIGNALPROCESSING\_模式**的基本支持处理程序应将**KSP 传递到 KSP\_PIN**结构，并且应仅在非环回流式处理 pin 上公布支持。 音频驱动程序应仅支持主机和卸载 pin 上的信号处理模式。 对于环回或桥接，音频驱动程序仍应支持属性，但会返回**KSMULTIPLE\_项**结构，并将其*Count*参数设置为零（0）。

开发的任何适用于 Microsoft 音频端口类驱动程序（Portcls）的音频微型端口驱动程序都可以实现[**IMiniportAudioSignalProcessing：： GetModes**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iminiportaudiosignalprocessing-getmodes)方法。

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
<td align="left"><p>Windows 8.1</p></td>
</tr>
<tr class="even">
<td align="left"><p>标头</p></td>
<td align="left">Ksmedia.h</td>
</tr>
</tbody>
</table>

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[**IMiniportAudioSignalProcessing::GetModes**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iminiportaudiosignalprocessing-getmodes)

[KSMULTIPLE\_项](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksmultiple_item)

[KSP\_PIN](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksp_pin)

 

 






