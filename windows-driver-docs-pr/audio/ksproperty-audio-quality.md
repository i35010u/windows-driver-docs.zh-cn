---
title: KSPROPERTY\_音频\_质量
description: KSPROPERTY\_音频\_QUALITY 属性指定节点输出流的质量级别。 这是 SRC 节点（KSNODETYPE\_SRC）的属性。
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
ms.openlocfilehash: b6edce229aee481217e4f443e74ce3be129d1cd9
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72832937"
---
# <a name="ksproperty_audio_quality"></a>KSPROPERTY\_音频\_质量


KSPROPERTY\_音频\_QUALITY 属性指定节点输出流的质量级别。 这是 SRC 节点（[**KSNODETYPE\_src**](ksnodetype-src.md)）的属性。

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
<td align="left"><p>“是”</p></td>
<td align="left"><p>大头针</p></td>
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksnodeproperty" data-raw-source="[&lt;strong&gt;KSNODEPROPERTY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksnodeproperty)"><strong>KSNODEPROPERTY</strong></a></td>
<td align="left"><p>ULONG</p></td>
</tr>
</tbody>
</table>

 

属性值（操作数据）的类型为 ULONG，指示输出流的质量级别。 应将此值设置为标头文件 Ksmedia 中的以下常量之一：

<span id="KSAUDIO_QUALITY_WORST"></span><span id="ksaudio_quality_worst"></span>KSAUDIO\_质量\_最差  
最差质量

<span id="KSAUDIO_QUALITY_PC"></span><span id="ksaudio_quality_pc"></span>KSAUDIO\_PC 的\_质量  
标准计算机质量（无限制）

<span id="KSAUDIO_QUALITY_BASIC"></span><span id="ksaudio_quality_basic"></span>KSAUDIO\_质量\_基本  
基本（低端）消费者音频质量（默认值）

<span id="KSAUDIO_QUALITY_ADVANCED"></span><span id="ksaudio_quality_advanced"></span>KSAUDIO\_优质\_高级  
高级（高端）消费者音频质量

### <a name="span-idreturn_valuespanspan-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

KSPROPERTY\_音频\_质量属性请求返回状态\_SUCCESS，以指示已成功完成。 否则，请求将返回相应的错误状态代码。

<a name="remarks"></a>备注
-------

有关[KMixer 系统驱动程序](https://docs.microsoft.com/windows-hardware/drivers/audio/kernel-mode-wdm-audio-components#kmixer-system-driver)执行的采样速率转换的类型的信息，请参阅[KMixer 驱动程序采样速率转换和混合策略](https://docs.microsoft.com/windows-hardware/drivers/audio/kmixer-driver-sample-rate-conversion-and-mixing-policy)。

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
<td align="left">Ksmedia （包括 Ksmedia）</td>
</tr>
</tbody>
</table>

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[**KSNODETYPE\_SRC**](ksnodetype-src.md)

[**KSNODEPROPERTY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksnodeproperty)

 

 






