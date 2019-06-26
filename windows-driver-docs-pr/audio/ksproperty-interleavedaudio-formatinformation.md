---
title: KSPROPERTY\_INTERLEAVEDAUDIO_FORMATINFORMATION
description: KSPROPERTY\_INTERLEAVEDAUDIO_FORMATINFORMATION 属性提供有关环回音频和捕获音频的交错执行的其他信息。
keywords:
- KSPROPERTY_INTERLEAVEDAUDIO_FORMATINFORMATION 音频设备
topic_type:
- apiref
api_name:
- KSPROPERTY_INTERLEAVEDAUDIO_FORMATINFORMATION
api_location:
- ksmedia.h
api_type:
- HeaderDef
ms.date: 02/15/2019
ms.localizationpriority: medium
ms.openlocfilehash: 37618d62b8ffb1ec8a26dee90b75b8ede4239b9f
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67361005"
---
# <a name="kspropertyinterleavedaudioformatinformation"></a>KSPROPERTY\_INTERLEAVEDAUDIO_FORMATINFORMATION 

**KSPROPERTY\_INTERLEAVEDAUDIO_FORMATINFORMATION**属性提供有关环回音频和捕获音频的交错执行的其他信息。

### <a name="span-idusagesummarytablespanspan-idusagesummarytablespanspan-idusagesummarytablespanusage-summary-table"></a><span id="Usage_Summary_Table"></span><span id="usage_summary_table"></span><span id="USAGE_SUMMARY_TABLE"></span>使用率摘要表

 |Get|设置|目标|属性描述符类型|属性值类型|
|--- |--- |--- |--- |--- |
|是|否|Pin|[KS_PIN](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksp_pin)|[INTERLEAVED_AUDIO_FORMAT_INFORMATION](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-interleaved-audio-format-information)|

### <a name="span-idreturnvaluespanspan-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

 Get **KSPROPERTY\_INTERLEAVEDAUDIO_FORMATINFORMATION**返回[INTERLEAVED_AUDIO_FORMAT_INFORMATION](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-interleaved-audio-format-information)结构，其中包含有关其他信息交错的环回音频和音频流中的捕获音频。 

Windows 10 中启动 19 H 1，设置 KSPROPERTY\_INTERLEAVEDAUDIO_FORMATINFORMATION 属性键是成一个流，支持的硬件关键字 Spotter (HW KWS) 该组合麦克风和环回音频的系统的要求若要使用 AEC APO 关键字迸发输出。 有关详细信息，请参阅[语音激活](voice-activation.md)。


<a name="remarks"></a>备注
-------

此属性仅用于硬件关键字 Spotter pin，并提供一种方法，以包括交织在一起的麦克风音频环回音频。 这是通过隔行扫描硬件关键字 Spotter pin 音频和环回音频一起成一个 PCM 音频流，然后通信时，通过此属性包含与麦克风音频环回的通道。

可使用此属性示例 APO。 它是 GitHub 上作为 sysvad 示例驱动程序的一部分，称为*KWSApo*。 示例 APO 只需剥离环回音频提供仅主麦克风音频上游。


<a name="requirements"></a>要求
------------

|||
|--- |--- |
|最低受支持的客户端|Windows 10 版本 19 H 1|
|Header|Ksmedia.h|

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>另请参阅

[KSPROPSETID\_INTERLEAVEDAUDIO](kspropsetid-interleavedaudio.md)

[KS_PIN](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksp_pin)





