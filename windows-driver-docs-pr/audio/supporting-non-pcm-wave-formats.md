---
title: 支持非 PCM 波形格式
description: 支持非 PCM 波形格式
keywords:
- 非 PCM 音频格式 WDK
- WDM 音频驱动程序 WDK，非 PCM 波浪格式
- 音频驱动程序 WDK，非 PCM 波浪格式
- 格式化 WDK 音频，非 PCM
- PCM 音频格式
- 音频非 PCM 格式 WDK
ms.date: 10/27/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4e930d08c1b7a6fd6de27c16f9b187fd01a46526
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96800565"
---
# <a name="supporting-non-pcm-wave-formats"></a>支持非 PCM 波形格式


## <span id="supporting_non_pcm_wave_formats"></span><span id="SUPPORTING_NON_PCM_WAVE_FORMATS"></span>

本部分介绍 Windows 的早期版本中阻止客户端播放非 PCM 音频的限制，并提供一组指导原则，用于调整 WDM 音频驱动程序，以支持最新版本的 Windows 上的非 PCM 数据格式。

此外，本部分还介绍了 Windows 7 中提供压缩音频格式支持的新 subformat Guid。

本节包括下列主题：

[非 PCM 支持的背景](background-of-non-pcm-support.md)

[非 PCM 引脚工厂的要求](requirements-for-a-non-pcm-pin-factory.md)

[压缩的音频格式的子格式 GUID](subformat-guids-for-compressed-audio-formats.md)

[在格式标记与子格式 GUID 之间进行转换](converting-between-format-tags-and-subformat-guids.md)

[KS 拓扑注意事项](ks-topology-considerations.md)

[有关 waveOut 客户端的具体信息](specifics-for-waveout-clients.md)

[有关 DirectSound 客户端的具体信息](specifics-for-directsound-clients.md)

[非 PCM 流的 S/PDIF 直通传输](s-pdif-pass-through-transmission-of-non-pcm-streams.md)

[指定 AC-3 数据范围](specifying-ac-3-data-ranges.md)

[指定 WMA Pro 数据范围](specifying-wma-pro-data-ranges.md)

[对非 PCM 格式的 USB 音频支持](usb-audio-support-for-non-pcm-formats.md)


 

 




