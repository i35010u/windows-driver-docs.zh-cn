---
title: KSPROPERTY \_ 音频 \_ 质量
description: "\"KSPROPERTY \\_ 音频 \\_ 质量\" 属性指定节点输出流的质量级别。 这是 SRC 节点 (KSNODETYPE src) 的属性 \\_ 。"
ms.assetid: ef57de3b-f7ac-4ecd-915e-27f34fcc2028
keywords:
- KSPROPERTY_AUDIO_QUALITY 音频设备
topic_type:
- apiref
api_name:
- KSPROPERTY_AUDIO_QUALITY
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 57901a4025eacfa0bb9700f0cec23cc4c7fe6873
ms.sourcegitcommit: 7500a03d1d57e95377b0b182a06f6c7dcdd4748e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "90102052"
---
# <a name="ksproperty_audio_quality"></a>KSPROPERTY \_ 音频 \_ 质量


"KSPROPERTY \_ 音频 \_ 质量" 属性指定节点输出流的质量级别。 这是 SRC 节点 ([**KSNODETYPE \_ src**](ksnodetype-src.md)) 的属性。

## <span id="ddk_ksproperty_audio_quality_ks"></span><span id="DDK_KSPROPERTY_AUDIO_QUALITY_KS"></span>


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
<td align="left"><p>是</p></td>
<td align="left"><p>Pin</p></td>
<td align="left"><a href="/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksnodeproperty" data-raw-source="[&lt;strong&gt;KSNODEPROPERTY&lt;/strong&gt;](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksnodeproperty)"><strong>KSNODEPROPERTY</strong></a></td>
<td align="left"><p>ULONG</p></td>
</tr>
</tbody>
</table>

 

 (操作数据) 的属性值为 ULONG 类型，指示输出流的质量级别。 应将此值设置为标头文件 Ksmedia 中的以下常量之一：

<span id="KSAUDIO_QUALITY_WORST"></span><span id="ksaudio_quality_worst"></span>KSAUDIO \_ 质量 \_ 最差  
最差质量

<span id="KSAUDIO_QUALITY_PC"></span><span id="ksaudio_quality_pc"></span>KSAUDIO \_ 优质 \_ PC  
标准计算机质量 (无限制) 

<span id="KSAUDIO_QUALITY_BASIC"></span><span id="ksaudio_quality_basic"></span>KSAUDIO \_ 质量 \_ 基本  
基本 (低端) 使用者音频质量 (默认值) 

<span id="KSAUDIO_QUALITY_ADVANCED"></span><span id="ksaudio_quality_advanced"></span>KSAUDIO \_ 优质 \_ 高级  
高级 (高端) 消费者音频质量

### <a name="span-idreturn_valuespanspan-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

KSPROPERTY \_ 音频 \_ 质量属性请求返回状态 " \_ 成功" 以指示它已成功完成。 否则，请求将返回相应的错误状态代码。

<a name="remarks"></a>注解
-------

有关 [KMixer 系统驱动程序](./kernel-mode-wdm-audio-components.md#kmixer-system-driver) 执行的采样速率转换的类型的信息，请参阅 [KMixer 驱动程序采样速率转换和混合策略](./index.md)。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>标头</p></td>
<td align="left">Ksmedia (包含 Ksmedia) </td>
</tr>
</tbody>
</table>

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[**KSNODETYPE \_ SRC**](ksnodetype-src.md)

[**KSNODEPROPERTY**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksnodeproperty)

