---
title: KSPROPERTY\_AUDIO\_DEV\_SPECIFIC
description: KSPROPERTY\_音频\_开发人员\_特定的属性用于访问特定于设备的节点中的特定于设备的属性 (KSNODETYPE\_开发人员\_特定)。
ms.assetid: f3f2e340-7403-4c86-841f-7008afda28a5
keywords:
- KSPROPERTY_AUDIO_DEV_SPECIFIC 音频设备
topic_type:
- apiref
api_name:
- KSPROPERTY_AUDIO_DEV_SPECIFIC
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: dd1b56d5f89cf793677082e9197c3da2718d73e7
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56520379"
---
# <a name="kspropertyaudiodevspecific"></a>KSPROPERTY\_AUDIO\_DEV\_SPECIFIC


`KSPROPERTY_AUDIO_DEV_SPECIFIC`属性用于访问特定于设备的节点中的特定于设备的属性 ([**KSNODETYPE\_开发人员\_特定**](ksnodetype-dev-specific.md))。

## <span id="ddk_ksproperty_audio_dev_specific_ks"></span><span id="DDK_KSPROPERTY_AUDIO_DEV_SPECIFIC_KS"></span>


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
<td align="left"><p>&lt;device-specific&gt;</p></td>
<td align="left"><p>&lt;device-specific&gt;</p></td>
<td align="left"><p>&lt;device-specific&gt;</p></td>
<td align="left"><p>&lt;device-specific&gt;</p></td>
<td align="left"><p>&lt;device-specific&gt;</p></td>
</tr>
</tbody>
</table>

 

以特定于设备的格式表示的属性值 （操作数据）。

该属性是否支持 get 或 set 属性请求也是特定于设备。

### <a name="span-idreturnvaluespanspan-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

此属性返回任一状态\_成功或第三方提供商的音频驱动程序确定的设备特定值。

<a name="remarks"></a>备注
-------

在 Windows Vista 和更高版本的 Windows，一个附加选项卡中 (标记为**自定义**) 中提供**声音**小程序中的**控制面板**。 **自定义**选项卡显示用于自动增益控制 (AGC) 和特定于设备的属性的控件。 下表显示了在中公开的控件**声音**各种小程序`KSPROPERTY_AUDIO_DEV_SPECIFIC`属性和数据类型的组合。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">KSPROPERTY</th>
<th align="left">数据类型</th>
<th align="left">控件</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="ksproperty-audio-agc.md" data-raw-source="[&lt;strong&gt;KSPROPERTY_AUDIO_AGC&lt;/strong&gt;](ksproperty-audio-agc.md)"><strong>KSPROPERTY_AUDIO_AGC</strong></a></p></td>
<td align="left"><p>BOOL</p></td>
<td align="left"><p>复选框</p></td>
</tr>
<tr class="even">
<td align="left"><p>KSPROPERTY_AUDIO_DEV_SPECIFIC</p></td>
<td align="left"><p>BOOL</p></td>
<td align="left"><p>复选框</p></td>
</tr>
<tr class="odd">
<td align="left"><p>KSPROPERTY_AUDIO_DEV_SPECIFIC</p></td>
<td align="left"><p>长</p></td>
<td align="left"><p>滑块</p></td>
</tr>
<tr class="even">
<td align="left"><p>KSPROPERTY_AUDIO_DEV_SPECIFIC</p></td>
<td align="left"><p>ULONG</p></td>
<td align="left"><p>滑块</p></td>
</tr>
</tbody>
</table>

 

**KSPROPERTY\_音频\_AGC**必须用于公开实际 AGC 功能的设备中。 其他特定于设备的功能必须通过使用公开`KSPROPERTY_AUDIO_DEV_SPECIFIC`。

若要查看**自定义**选项卡上，选择音频呈现或中的捕获设备**声音**小程序，然后单击*属性*。

有关如何实现的属性处理程序的示例`KSPROPERTY_AUDIO_DEV_SPECIFIC`属性，请参阅**CMiniportTopologyMSVAD::PropertyHandlerDevSpecific** Basetopo.cpp 文件中的方法。

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
<td align="left"><p>在 Windows Vista 和更高版本的 Windows 操作系统中可用。</p></td>
</tr>
<tr class="even">
<td align="left"><p>标头</p></td>
<td align="left">Ksmedia.h （包括 Ksmedia.h）</td>
</tr>
</tbody>
</table>

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>另请参阅


[**KSNODETYPE\_开发人员\_特定**](ksnodetype-dev-specific.md)

[**KSPROPERTY\_AUDIO\_AGC**](ksproperty-audio-agc.md)

 

 






