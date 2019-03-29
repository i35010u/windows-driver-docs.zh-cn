---
title: 支持非 PCM 波形格式
description: 支持非 PCM 波形格式
ms.assetid: 76455e1f-4b00-49c4-a4e4-3cb4abe8f445
keywords:
- 非 PCM 音频格式 WDK
- WDM 音频驱动程序 WDK，非 PCM 波形格式
- 音频驱动程序 WDK，非 PCM 波形格式
- 格式 WDK 音频，非-PCM
- PCM 格式 WDK 音频
- 音频非 PCM 格式 WDK
ms.date: 10/27/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8f514fabe610acf94764ad6cce38869fb92bd85e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56567832"
---
# <a name="supporting-non-pcm-wave-formats"></a>支持非 PCM 波形格式


## <span id="supporting_non_pcm_wave_formats"></span><span id="SUPPORTING_NON_PCM_WAVE_FORMATS"></span>

本部分介绍在早期版本的 Windows 客户端会阻止播放非 PCM 音频，并提供了一组指南，用于调整 WDM 音频驱动程序以支持较新版本的 Windows 上的非 PCM 数据格式的限制。

此外，本部分介绍新的子格式为压缩的音频格式提供支持 Windows 7 中的 Guid。

本部分包括以下主题：

[背景的非 PCM 支持](background-of-non-pcm-support.md)

[非 PCM Pin 工厂的要求](requirements-for-a-non-pcm-pin-factory.md)

[压缩的音频格式的子格式 Guid](subformat-guids-for-compressed-audio-formats.md)

[格式标记与子格式 Guid 之间进行转换](converting-between-format-tags-and-subformat-guids.md)

[KS 拓扑注意事项](ks-topology-considerations.md)

[有关 waveOut 客户端的具体信息](specifics-for-waveout-clients.md)

[DirectSound 客户端的详细信息](specifics-for-directsound-clients.md)

[S/PDIF 直通传输的非 PCM 流](s-pdif-pass-through-transmission-of-non-pcm-streams.md)

[指定 ac-3 数据范围](specifying-ac-3-data-ranges.md)

[指定 WMA Pro 数据范围](specifying-wma-pro-data-ranges.md)

[对非 PCM 格式的 USB 音频支持](usb-audio-support-for-non-pcm-formats.md)


 

 




