---
title: KSNODETYPE \_ 音频 \_ 引擎
description: KSNODETYPE \_ 音频 \_ 引擎音频终结点是 windows 8 及更高版本的 windows 中可用的新终结点。
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
ms.openlocfilehash: 22ff08a835426bc7c2ca80bf6991225a43dab600
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96784653"
---
# <a name="ksnodetype_audio_engine"></a>KSNODETYPE \_ 音频 \_ 引擎


KSNODETYPE \_ 音频 \_ 引擎音频终结点是 windows 8 及更高版本的 windows 中可用的新终结点。 KSNODETYPE \_ 音频 \_ 引擎音频终结点包含在 Wave 内核流式处理 (KS) 音频过滤器内，并允许音频驱动程序公开硬件音频引擎的功能。

KSNODETYPE \_ 音频 \_ 引擎音频终结点是必需的终结点及其引入的内容，因此必须开发新的波形数据接收器 pin 工厂，新终结点才能直接连接到该终结点。

KSNODETYPE \_ 音频 \_ 引擎音频终结点必须支持 [**KSPROPERTY \_ AUDIOENGINE**](ksproperty-audioengine.md) 枚举值以及以下 KS 属性：

[**KSPROPERTY \_ 音频 \_ 静音**](ksproperty-audio-mute.md)

[**KSPROPERTY \_ 音频 \_ PEAKMETER**](ksproperty-audio-peakmeter.md)

[**KSPROPERTY \_ 音频 \_ VOLUMELEVEL**](ksproperty-audio-volumelevel.md)

[KSPROPSETID \_ AudioEngine](kspropsetid-audioengine.md)

 

 





