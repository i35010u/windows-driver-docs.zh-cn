---
title: KSNODETYPE\_AUDIO\_KEYWORDDETECTOR
description: KSNODETYPE\_音频\_KEYWORDDETECTOR 音频终结点是可用于 Windows 10 和更高版本的 Windows 的新终结点。 KSNODETYPE\_音频\_KEYWORDDETECTOR 允许受支持检测程序音频捕获驱动程序。
ms.assetid: 7D4CD2B7-F4B4-4A81-B18A-2B7E86D1EF80
keywords:
- KSNODETYPE_AUDIO_KEYWORDDETECTOR 音频设备
topic_type:
- apiref
api_name:
- KSNODETYPE_AUDIO_KEYWORDDETECTOR
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 907d58ddd8e69da248406d74cd812fcf4394f57c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56564378"
---
# <a name="ksnodetypeaudiokeyworddetector"></a>KSNODETYPE\_AUDIO\_KEYWORDDETECTOR


KSNODETYPE\_音频\_KEYWORDDETECTOR 音频终结点是可用于 Windows 10 和更高版本的 Windows 的新终结点。 KSNODETYPE\_音频\_KEYWORDDETECTOR 允许受支持检测程序音频捕获驱动程序。

不能与其他捕获设备共享此筛选器。 筛选器都具有一个 KS pin 工厂，它具有 pin 类别 KSNODETYPE\_音频\_KEYWORDDETECTOR。 不能有多个 pin 工厂给定 KS 筛选器实例中具有此 KS pin 类别。

KSNODETYPE\_音频\_KEYWORDDETECTOR 音频终结点必须支持以下 KS 属性：

[**KSPROPERTY\_SOUNDDETECTOR\_SUPPORTEDPATTERNS**](ksproperty-sounddetector-supportedpatterns.md)

[**KSPROPERTY\_SOUNDDETECTOR\_模式**](ksproperty-sounddetector-patterns.md)

[**KSPROPERTY\_SOUNDDETECTOR\_ARMED**](ksproperty-sounddetector-armed.md)

[**KSPROPERTY\_SOUNDDETECTOR\_MATCHRESULT**](ksproperty-sounddetector-matchresult.md)

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>另请参阅


[KSPROPSETID\_SoundDetector](kspropsetid-sounddetector.md)

 

 






