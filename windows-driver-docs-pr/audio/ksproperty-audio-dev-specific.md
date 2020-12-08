---
title: KSPROPERTY \_ \_ \_ 特定于音频的开发
description: KSPROPERTY \_ AUDIO \_ DEV \_ 特定属性用于访问特定于设备的节点中特定于设备的属性， (KSNODETYPE \_ DEV \_ 特定) 。
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
ms.openlocfilehash: 7f07324df2ad0930427d41b91c8c1874970a9034
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96784527"
---
# <a name="ksproperty_audio_dev_specific"></a>KSPROPERTY \_ \_ \_ 特定于音频的开发


属性用于访问特定于设备的节点中特定于设备的 `KSPROPERTY_AUDIO_DEV_SPECIFIC` 属性 ([**KSNODETYPE \_ DEV \_ 特定**](ksnodetype-dev-specific.md)) 。

## <span id="ddk_ksproperty_audio_dev_specific_ks"></span><span id="DDK_KSPROPERTY_AUDIO_DEV_SPECIFIC_KS"></span>


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
<td align="left"><p>&lt;设备特定&gt;</p></td>
<td align="left"><p>&lt;设备特定&gt;</p></td>
<td align="left"><p>&lt;设备特定&gt;</p></td>
<td align="left"><p>&lt;设备特定&gt;</p></td>
<td align="left"><p>&lt;设备特定&gt;</p></td>
</tr>
</tbody>
</table>

 

) 操作数据 (的属性值以特定于设备的格式表示。

属性是否支持获取或设置属性请求也是特定于设备的。

### <a name="span-idreturn_valuespanspan-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

此属性返回状态 \_ 成功或由音频驱动程序的第三方提供程序确定的设备特定值。

<a name="remarks"></a>备注
-------

在 Windows Vista 和更高版本的 Windows 中，"**控制面板**" 的 "**声音**" 小程序中提供了一个附加选项卡 (标签为 "**自定义**) "。 " **自定义** " 选项卡显示 (AGC) 和特定于设备的属性的自动获取控件的控件。 下表显示了在 **声音** 小程序中为各种 `KSPROPERTY_AUDIO_DEV_SPECIFIC` 属性和数据类型组合公开的控件。

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
<th align="left">控制</th>
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
<td align="left"><p>LONG</p></td>
<td align="left"><p>Slider</p></td>
</tr>
<tr class="even">
<td align="left"><p>KSPROPERTY_AUDIO_DEV_SPECIFIC</p></td>
<td align="left"><p>ULONG</p></td>
<td align="left"><p>Slider</p></td>
</tr>
</tbody>
</table>

 

**KSPROPERTY \_必须使用音频 \_ AGC** 公开设备中的实际 AGC 功能。 其他特定于设备的功能必须使用公开 `KSPROPERTY_AUDIO_DEV_SPECIFIC` 。

若要查看 " **自定义** " 选项卡，请在 **声音** 小程序中选择音频呈现器或捕获设备，然后单击 " *属性*"。

有关如何为属性实现属性处理程序的示例 `KSPROPERTY_AUDIO_DEV_SPECIFIC` ，请参阅 Basetopo 文件中的 **CMiniportTopologyMSVAD：:P ropertyhandlerdevspecific** 方法。

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
<td align="left">Ksmedia (包含 Ksmedia) </td>
</tr>
</tbody>
</table>

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[**KSNODETYPE \_ 开发人员 \_ 特定**](ksnodetype-dev-specific.md)

[**KSPROPERTY \_ 音频 \_ AGC**](ksproperty-audio-agc.md)

 

 






