---
title: 对非 PCM 格式的 USB 音频支持
description: 对非 PCM 格式的 USB 音频支持
ms.assetid: e4479a67-ec45-45f1-9c42-f050cb0f2eb2
keywords:
- USBAudio 类系统驱动程序 WDK 音频
- 非 PCM 音频格式 WDK USBAudio
- 原始 ac-3 WDK 音频
- Ac-3 WDK 音频
- 非 PCM 音频格式 WDK、 ac-3
- USB 音频
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1f338f58f3fb616eb454ebf7ba0632f526ede748
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56567825"
---
# <a name="usb-audio-support-for-non-pcm-formats"></a>对非 PCM 格式的 USB 音频支持


## <span id="usb_audio_support_for_non_pcm_formats"></span><span id="USB_AUDIO_SUPPORT_FOR_NON_PCM_FORMATS"></span>


Microsoft 的[USBAudio 类系统驱动程序](kernel-mode-wdm-audio-components.md#usbaudio_class_system_driver)，Usbaudio.sys，当前不支持 USB 音频类型 III 格式，并填充 ac-3。 有关详细信息，请参阅*通用串行总线的设备类定义数据格式以音频*规范[USB 实现论坛](https://go.microsoft.com/fwlink/p/?linkid=8780)网站。

USBAudio 可以接受已打包、"原始"ac-3 （而不是接受 PortCls 驱动程序的填充，AC-3-over-S/PDIF 格式）。 USBAudio 支持 DirectShow 的 DVD 拆分器筛选器的内部格式 (请参阅[在 Windows 中的 DVD 解码器支持](https://msdn.microsoft.com/library/windows/hardware/ff558763))，这可以直接连接到受控制的 KsProxy USBAudio (请参阅[内核流式处理代理](https://msdn.microsoft.com/library/windows/hardware/ff560877)). 具体而言，由 USBAudio 公开的 nonpadded ac-3 数据范围是 KSDATAFORMAT\_子类型\_AC3\_音频，这是相同的 GUID 值 MEDIASUBTYPE\_DOLBY\_AC3。

USBAudio 目前不支持非 PCM 音频数据的 DirectSound 播放。

 

 




