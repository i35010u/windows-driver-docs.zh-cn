---
title: KSPROPERTY\_音频\_复制\_保护
description: KSPROPERTY\_音频\_复制\_保护属性指定的音频流的复制保护状态。
ms.assetid: 68896bd4-9ffe-4632-a3b2-441b5d04208a
keywords:
- KSPROPERTY_AUDIO_COPY_PROTECTION 音频设备
topic_type:
- apiref
api_name:
- KSPROPERTY_AUDIO_COPY_PROTECTION
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 601da5beb0e302729882b6c7e9e0977d2fecae47
ms.sourcegitcommit: f663c383886d87ea762e419963ff427500cc5042
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67391485"
---
# <a name="kspropertyaudiocopyprotection"></a>KSPROPERTY\_音频\_复制\_保护


KSPROPERTY\_音频\_复制\_保护属性指定的音频流的复制保护状态。

## <span id="ddk_ksproperty_audio_copy_protection_ks"></span><span id="DDK_KSPROPERTY_AUDIO_COPY_PROTECTION_KS"></span>


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
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/ff564262(v=vs.85)" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/ff564262(v=vs.85))"><strong>KSPROPERTY</strong></a></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksaudio_copy_protection" data-raw-source="[&lt;strong&gt;KSAUDIO_COPY_PROTECTION&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksaudio_copy_protection)"><strong>KSAUDIO_COPY_PROTECTION</strong></a></p></td>
</tr>
</tbody>
</table>

 

属性值 （操作数据） 是一种结构的类型 KSAUDIO\_复制\_保护。 该结构指定是否具有版权流;它还指定流是否原始流或原始流的副本。

### <a name="span-idreturnvaluespanspan-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

KSPROPERTY\_音频\_副本\_保护属性请求将返回状态\_成功以指示已成功完成。 否则，请求将返回相应的错误状态代码。

<a name="remarks"></a>备注
-------

KSPROPERTY\_音频\_复制\_保护属性是支持到串行复制管理系统 (SCMS) 类似的保护方案的音频设备的属性。 属性指示数字流是否受版权以及它是否原始流或副本。

SCMS 可以提供三个级别的音频内容的保护：

**级别 0:** 不受限制复制缺少版权或不会断言版权的流。

**级别 1:** 复制第一代的流的限制。 用户可以创建多份原始受版权保护的流，但它们不能进行将流的副本的副本。

**级别 2:** 在所有流的任何复制。

KSPROPERTY\_音频\_副本\_保护属性的实现的是独立于和不相关[数字版权管理 (DRM)](https://docs.microsoft.com/windows-hardware/drivers/audio/digital-rights-management)和保护音频路径 (SAP) 的 Windows介质。 有关 SAP 的信息，请参阅 Microsoft Windows SDK 文档。

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


[**KSPROPERTY**](https://docs.microsoft.com/previous-versions/ff564262(v=vs.85))

[**KSAUDIO\_COPY\_PROTECTION**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksaudio_copy_protection)

 

 






