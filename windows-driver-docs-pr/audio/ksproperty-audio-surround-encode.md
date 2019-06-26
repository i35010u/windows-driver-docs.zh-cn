---
title: KSPROPERTY\_音频\_环绕\_编码
description: KSPROPERTY\_音频\_环绕\_编码属性指定是启用还是禁用筛选器的外侧代码编码器。 外侧代码编码器节点 (KSNODETYPE\_PROLOGIC\_编码器) 执行 Dolby 环绕 Pro 逻辑的编码。
ms.assetid: 249ee13f-a986-4cb1-906f-55062274df45
keywords:
- KSPROPERTY_AUDIO_SURROUND_ENCODE 音频设备
topic_type:
- apiref
api_name:
- KSPROPERTY_AUDIO_SURROUND_ENCODE
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 96b307caf85fbd1ec758c65615b547f49b99cf5b
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67358871"
---
# <a name="kspropertyaudiosurroundencode"></a>KSPROPERTY\_音频\_环绕\_编码


KSPROPERTY\_音频\_环绕\_编码属性指定是启用还是禁用筛选器的外侧代码编码器。 外侧代码编码器节点 ([**KSNODETYPE\_PROLOGIC\_编码器**](ksnodetype-prologic-encoder.md)) 执行 Dolby 环绕 Pro 逻辑的编码。

## <span id="ddk_ksproperty_audio_surround_encode_ks"></span><span id="DDK_KSPROPERTY_AUDIO_SURROUND_ENCODE_KS"></span>


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
<td align="left"><p>是</p></td>
<td align="left"><p>Filter</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksnodeproperty" data-raw-source="[&lt;strong&gt;KSNODEPROPERTY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksnodeproperty)"><strong>KSNODEPROPERTY</strong></a></p></td>
<td align="left"><p>BOOL</p></td>
</tr>
</tbody>
</table>

 

（操作数据） 的属性值属于类型布尔值，指示是否启用外侧代码编码器节点。 值为 **，则返回 TRUE**指示是否启用了编码器环绕节点。 **FALSE**指示已禁用。

### <a name="span-idreturnvaluespanspan-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

KSPROPERTY\_音频\_环绕\_编码属性请求将返回状态\_成功以指示已成功完成。 否则，请求将返回相应的错误状态代码。

<a name="remarks"></a>备注
-------

在 Microsoft Windows XP 及更高版本， [KMixer 系统驱动程序](https://docs.microsoft.com/windows-hardware/drivers/audio/kernel-mode-wdm-audio-components#kmixer-system-driver)支持 KSPROPERTY\_音频\_环绕\_编码属性。

如果启用，环绕编码器节点进行编码的 4 个通道输入的流中 （与通道左侧、 右侧、 中心和后置扬声器） 到环绕声编码的立体声输出流。 此输出流可以解码[ **KSNODETYPE\_PROLOGIC\_解码器**](ksnodetype-prologic-decoder.md)节点，例如。 它还可以通过音频设备模拟立体声输出，它们可以连接到外部环绕解码器，直接引导左、 右对齐、 居中，并返回扬声器播放。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>Header</p></td>
<td align="left">Ksmedia.h （包括 Ksmedia.h）</td>
</tr>
</tbody>
</table>

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>另请参阅


[**KSNODEPROPERTY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksnodeproperty)

[**KSNODETYPE\_PROLOGIC\_编码器**](ksnodetype-prologic-encoder.md)

[**KSNODETYPE\_PROLOGIC\_解码器**](ksnodetype-prologic-decoder.md)

 

 






