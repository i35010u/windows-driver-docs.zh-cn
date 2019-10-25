---
title: KSPROPERTY\_音频\_采样\_速率
description: KSPROPERTY\_音频\_采样\_速率属性指定节点采样其输入流以生成其输出流的速率。
ms.assetid: c5e48678-3b9a-4e5b-ae7b-16f9dcae7492
keywords:
- KSPROPERTY_AUDIO_SAMPLING_RATE 音频设备
topic_type:
- apiref
api_name:
- KSPROPERTY_AUDIO_SAMPLING_RATE
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 22524173db6de9e944a8e44239920b74ef3182ab
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72830940"
---
# <a name="ksproperty_audio_sampling_rate"></a>KSPROPERTY\_音频\_采样\_速率


KSPROPERTY\_音频\_采样\_速率属性指定节点采样其输入流以生成其输出流的速率。

## <span id="ddk_ksproperty_audio_sampling_rate_ks"></span><span id="DDK_KSPROPERTY_AUDIO_SAMPLING_RATE_KS"></span>


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
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksnodeproperty" data-raw-source="[&lt;strong&gt;KSNODEPROPERTY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksnodeproperty)"><strong>KSNODEPROPERTY</strong></a></p></td>
<td align="left"><p>ULONG</p></td>
</tr>
</tbody>
</table>

 

属性值（操作数据）的类型为 ULONG，并指定采样率。 此速率表示为每秒的样本数（以 Hz 为单位的采样频率）。

### <a name="span-idreturn_valuespanspan-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

KSPROPERTY\_音频\_采样\_RATE 属性请求返回状态\_"成功" 以指示已成功完成。 否则，请求将返回相应的错误状态代码。

<a name="remarks"></a>备注
-------

如果节点不支持指定的采样速率，则微型端口驱动程序应在设置属性请求上返回错误。

此属性用于控制以下节点类型的采样率：

-   ADC 节点（[**KSNODETYPE\_ADC**](ksnodetype-adc.md)）

-   DAC 节点（[**KSNODETYPE\_DAC**](ksnodetype-dac.md)）

-   SRC 节点（[**KSNODETYPE\_src**](ksnodetype-src.md)）

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


[**KSNODEPROPERTY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksnodeproperty)

[**KSNODETYPE\_ADC**](ksnodetype-adc.md)

[**KSNODETYPE\_DAC**](ksnodetype-dac.md)

[**KSNODETYPE\_SRC**](ksnodetype-src.md)

 

 






