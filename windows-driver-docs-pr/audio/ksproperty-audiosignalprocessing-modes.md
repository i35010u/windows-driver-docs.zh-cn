---
title: KSPROPERTY \_ AUDIOSIGNALPROCESSING \_ 模式
description: KSPROPERTY \_ AUDIOSIGNALPROCESSING \_ 模式属性返回 pin 工厂支持的音频信号处理模式的列表。
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
ms.openlocfilehash: c0d4bbe5d94ffc4b5c93034fde563fe88c1b2567
ms.sourcegitcommit: 7500a03d1d57e95377b0b182a06f6c7dcdd4748e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "90102596"
---
# <a name="ksproperty_audiosignalprocessing_modes"></a>KSPROPERTY \_ AUDIOSIGNALPROCESSING \_ 模式


**KSPROPERTY \_ AUDIOSIGNALPROCESSING \_ 模式**属性返回 pin 工厂支持的音频信号处理模式的列表。

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
<th align="left">获取</th>
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
<td align="left"><p>通过筛选器实例 (固定工厂) </p></td>
<td align="left"><p><a href="/windows-hardware/drivers/ddi/ks/ns-ks-ksp_pin" data-raw-source="[KSP_PIN](/windows-hardware/drivers/ddi/ks/ns-ks-ksp_pin)">KSP_PIN</a></p></td>
<td align="left"><p><a href="/windows-hardware/drivers/ddi/ks/ns-ks-ksmultiple_item" data-raw-source="[KSMULTIPLE_ITEM](/windows-hardware/drivers/ddi/ks/ns-ks-ksmultiple_item)">KSMULTIPLE_ITEM</a></p></td>
</tr>
</tbody>
</table>

 

属性值为结构，后跟零 (0) 或多个 Guid。

### <a name="span-idreturn_valuespanspan-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

**KSPROPERTY \_AUDIOSIGNALPROCESSING \_ 模式** 返回 **KSMULTIPLE \_ 项** ，后跟零 (0) 或多个 guid。 KSMULTIPLE \_ 项。Count 成员包含 Guid 的数目。 KSMULTIPLE \_ 项。Size 成员包含属性值的总大小。 每个 GUID 标识在**KSP \_ pin**结构的*PinId*成员中指定的 Pin ID 的音频驱动程序所支持的信号处理模式。

在 Windows 8.1 有两个已定义的音频信号处理模式：音频 \_ SIGNALPROCESSINGMODE \_ 默认值和音频 \_ SIGNALPROCESSINGMODE \_ RAW。

在 Windows 10 中，定义了五种附加模式。

音频 \_ SIGNALPROCESSINGMODE \_ 通信音频 \_ SIGNALPROCESSINGMODE \_ 语音音频 \_ SIGNALPROCESSINGMODE \_ 媒体音频 \_ SIGNALPROCESSINGMODE \_ 电影音频 \_ SIGNALPROCESSINGMODE \_ 通知有关详细信息，请参阅 [音频信号处理模式](./audio-signal-processing-modes.md)。

<a name="remarks"></a>备注
-------

**KSPROPERTY \_ AUDIOSIGNALPROCESSING \_ 模式**的基本支持处理程序应获得**KSP \_ PIN**结构，且仅在非环回流式处理 pin 上公布支持。 音频驱动程序应仅支持主机和卸载 pin 上的信号处理模式。 对于环回或桥接，音频驱动程序仍应支持属性，但会返回一个 **KSMULTIPLE \_ 项目** 结构，其 *Count* 参数设置为零 (0) 。

开发的任何音频微型端口驱动程序都 (Portcls) ，可实现 [**IMiniportAudioSignalProcessing：： GetModes**](/windows-hardware/drivers/ddi/portcls/nf-portcls-iminiportaudiosignalprocessing-getmodes) 方法。

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


[**IMiniportAudioSignalProcessing::GetModes**](/windows-hardware/drivers/ddi/portcls/nf-portcls-iminiportaudiosignalprocessing-getmodes)

[KSMULTIPLE \_ 项](/windows-hardware/drivers/ddi/ks/ns-ks-ksmultiple_item)

[KSP \_ PIN](/windows-hardware/drivers/ddi/ks/ns-ks-ksp_pin)

