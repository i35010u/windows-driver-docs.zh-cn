---
title: 对非 PCM 格式的 USB 音频支持
description: 对非 PCM 格式的 USB 音频支持
ms.assetid: e4479a67-ec45-45f1-9c42-f050cb0f2eb2
keywords:
- USBAudio 类系统驱动程序 WDK 音频
- 非 PCM 音频格式 WDK，USBAudio
- 原始 AC 3 WDK 音频
- AC 3 WDK 音频
- 非 PCM 音频格式 WDK、AC 3
- USB 音频
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ca00c33b73d894e83342460ccce9154ef5d6e997
ms.sourcegitcommit: 98930ca95b9adbb6e5e472f89e91ab084e67e31d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/08/2020
ms.locfileid: "82925518"
---
# <a name="usb-audio-support-for-non-pcm-formats"></a>对非 PCM 格式的 USB 音频支持


## <span id="usb_audio_support_for_non_pcm_formats"></span><span id="USB_AUDIO_SUPPORT_FOR_NON_PCM_FORMATS"></span>


Microsoft 的[USBAudio 类系统驱动程序](kernel-mode-wdm-audio-components.md#usbaudio_class_system_driver)USBAudio 目前不支持带填充 AC-3 的 USB 音频类型 III 格式。 有关详细信息，请参阅[USB 实现论坛](https://www.usb.org/)网站上的*音频数据格式的通用串行总线设备类定义*。

USBAudio 可以接受打包的 "原始" AC-3 （而不是 PortCls 驱动程序接受的已填充 AC-3/PDIF 格式）。 USBAudio 支持 DirectShow 的 DVD 拆分器筛选器的内部格式（请参阅[Windows 中的 DVD 解码器支持](https://docs.microsoft.com/windows-hardware/drivers/stream/dvd-decoder-support-in-windows)），该格式可以直接连接到 KsProxy 控制下的 USBAudio （请参阅[内核流式处理代理](https://docs.microsoft.com/windows-hardware/drivers/ddi/_stream/index)）。 具体来说，由 USBAudio 公开的 nonpadded AC-3 数据范围为\_KSDATAFORMAT\_子\_类型 E-AC3 音频，这是与 MEDIASUBTYPE\_杜比\_e-ac3 相同的 GUID 值。

USBAudio 目前不支持 DirectSound 播放非 PCM 音频数据。

 

 




