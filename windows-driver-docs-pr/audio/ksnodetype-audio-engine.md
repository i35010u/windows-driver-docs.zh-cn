---
title: KSNODETYPE\_音频\_引擎
description: KSNODETYPE\_音频\_引擎音频终结点是可用于 Windows 8 和更高版本的 Windows 的新终结点。
ms.assetid: C1A7E136-655A-4024-A280-F252F1AE1282
keywords:
- KSNODETYPE_AUDIO_ENGINE 音频设备
topic_type:
- apiref
api_name:
- KSNODETYPE_AUDIO_ENGINE
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 049a30fb920fa833d448b4c603e780332fa9dbf8
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56546332"
---
# <a name="ksnodetypeaudioengine"></a>KSNODETYPE\_音频\_引擎


KSNODETYPE\_音频\_引擎音频终结点是可用于 Windows 8 和更高版本的 Windows 的新终结点。 KSNODETYPE\_音频\_引擎音频终结点包含在流式处理 (KS) 音频筛选器，一个批内核和允许的音频驱动程序来公开硬件音频引擎的功能。

KSNODETYPE\_音频\_引擎音频终结点是必需的终结点和其简介进行必然需要开发新的终结点直接连接到新一波数据接收器 pin 工厂。

KSNODETYPE\_音频\_引擎音频终结点必须支持[ **KSPROPERTY\_AUDIOENGINE** ](ksproperty-audioengine.md)枚举值以及以下 KS属性：

[**KSPROPERTY\_AUDIO\_MUTE**](ksproperty-audio-mute.md)

[**KSPROPERTY\_AUDIO\_PEAKMETER**](ksproperty-audio-peakmeter.md)

[**KSPROPERTY\_音频\_VOLUMELEVEL**](ksproperty-audio-volumelevel.md)

[KSPROPSETID\_AudioEngine](kspropsetid-audioengine.md)

 

 





