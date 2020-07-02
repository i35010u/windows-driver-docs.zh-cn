---
title: KSPROPERTY \_ INTERLEAVEDAUDIO_FORMATINFORMATION
description: KSPROPERTY \_ INTERLEAVEDAUDIO_FORMATINFORMATION 属性提供有关环回音频和捕获音频交叉的其他信息。
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
ms.date: 07/11/2019
ms.localizationpriority: medium
ms.openlocfilehash: e41fe6d8f4dd0550d3b74f19d2f129339f484bdf
ms.sourcegitcommit: 7a69c2e0abf91a57407b13a30faf24925f677970
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/01/2020
ms.locfileid: "85829034"
---
# <a name="ksproperty_interleavedaudio_formatinformation"></a>KSPROPERTY \_ INTERLEAVEDAUDIO_FORMATINFORMATION

**KSPROPERTY \_ INTERLEAVEDAUDIO_FORMATINFORMATION**属性提供有关环回音频和捕获音频交叉的其他信息。

## <a name="usage-summary-table"></a>使用情况摘要表

 |获取|设置|目标|属性描述符类型|属性值类型|
|--- |--- |--- |--- |--- |
|是|否|引脚|[KS_PIN](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksp_pin)|[INTERLEAVED_AUDIO_FORMAT_INFORMATION](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_interleaved_audio_format_information)|

### <a name="return-value"></a>返回值

 对于 get， **KSPROPERTY \_ INTERLEAVEDAUDIO_FORMATINFORMATION**返回[INTERLEAVED_AUDIO_FORMAT_INFORMATION](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_interleaved_audio_format_information)结构，该结构包含有关在音频流中交叉环回音频和捕获音频的其他信息。

从 Windows 10 19H1 开始，如果 \_ 系统支持将麦克风和回送音频组合到单个流中的硬件关键字 Spotter （HW KWS），则需要设置 KSPROPERTY INTERLEAVEDAUDIO_FORMATINFORMATION 属性键，以便对关键字突发输出使用 AEC APO。 有关详细信息，请参阅[语音激活](voice-activation.md)。

## <a name="remarks"></a>备注

此属性仅用于硬件关键字 Spotter pin，并提供一种方法，用于将环回音频与麦克风音频交错使用。 这是通过交叉硬件关键字 Spotter 将音频和回送音频固定到单个 PCM 音频流中完成的，然后通过此属性与包含环回和麦克风音频的通道进行通信。

可以使用此属性的示例 APO。 它在 GitHub 上作为 sysvad 示例驱动程序的一部分，称为*KWSApo*。 该示例 APO 只需去除环回音频，只提供主麦克风音频上游。

## <a name="requirements"></a>要求

|要求|值|
|--- |--- |
|最低受支持的客户端|Windows 10 版本19H1|
|标头|Ksmedia.h|

## <a name="see-also"></a>请参阅

[KSPROPSETID \_ INTERLEAVEDAUDIO](kspropsetid-interleavedaudio.md)

[KS_PIN](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksp_pin)

[INTERLEAVED_AUDIO_FORMAT_INFORMATION](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_interleaved_audio_format_information)
