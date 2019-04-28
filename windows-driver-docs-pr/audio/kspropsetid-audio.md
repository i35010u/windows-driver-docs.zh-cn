---
title: KSPROPSETID\_音频
description: KSPROPSETID\_音频
ms.assetid: b65620c1-0460-430d-999d-f46fe0a2702d
keywords:
- KSPROPSETID_Audio
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: bd44c7ca62cb07b866399ae3a7f438e923ce7830
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63332554"
---
# <a name="kspropsetidaudio"></a>KSPROPSETID\_音频


## <span id="ddk_kspropsetid_audio_ks"></span><span id="DDK_KSPROPSETID_AUDIO_KS"></span>


`KSPROPSETID_Audio`属性集指示的数据和支持的音频流的控制范围。 微型端口驱动程序应支持 KSPROPERTY\_音频\_延迟属性。 设置此属性中的所有其他属性是可选的。

在硬件不支持的功能的情况下，微型端口驱动程序应返回 get 和 set 属性调用的错误，以便上层驱动程序可以处理该呼叫。 例如，不支持卷的控制的硬件的微型端口驱动程序应返回的错误[ **KSPROPERTY\_音频\_VOLUMELEVEL** ](ksproperty-audio-volumelevel.md)调用，从而使驱动程序 （如内核混音器） 堆栈中的流将卷设置。

在此集中的属性项由 KSPROPERTY\_音频枚举值。

以下属性属于`KSPROPSETID_Audio`属性集：

[**KSPROPERTY\_AUDIO\_3D\_INTERFACE**](ksproperty-audio-3d-interface.md)

[**KSPROPERTY\_AUDIO\_AGC**](ksproperty-audio-agc.md)

[**KSPROPERTY\_音频\_算法\_实例**](ksproperty-audio-algorithm-instance.md)

[**KSPROPERTY\_AUDIO\_BASS**](ksproperty-audio-bass.md)

[**KSPROPERTY\_AUDIO\_BASS\_BOOST**](ksproperty-audio-bass-boost.md)

[**KSPROPERTY\_音频\_缓冲区\_持续时间**](ksproperty-audio-buffer-duration.md)

[**KSPROPERTY\_音频\_通道\_配置**](ksproperty-audio-channel-config.md)

[**KSPROPERTY\_音频\_合唱团\_级别**](ksproperty-audio-chorus-level.md)

[**KSPROPERTY\_音频\_合唱团\_调制\_深度**](ksproperty-audio-chorus-modulation-depth.md)

[**KSPROPERTY\_音频\_合唱团\_调制\_速率**](ksproperty-audio-chorus-modulation-rate.md)

[**KSPROPERTY\_AUDIO\_COPY\_PROTECTION**](ksproperty-audio-copy-protection.md)

[**KSPROPERTY\_AUDIO\_CPU\_RESOURCES**](ksproperty-audio-cpu-resources.md)

[**KSPROPERTY\_AUDIO\_DELAY**](ksproperty-audio-delay.md)

[**KSPROPERTY\_AUDIO\_DEMUX\_DEST**](ksproperty-audio-demux-dest.md)

[**KSPROPERTY\_AUDIO\_DEV\_SPECIFIC**](ksproperty-audio-dev-specific.md)

[**KSPROPERTY\_AUDIO\_DYNAMIC\_RANGE**](ksproperty-audio-dynamic-range.md)

[**KSPROPERTY\_AUDIO\_DYNAMIC\_SAMPLING\_RATE**](ksproperty-audio-dynamic-sampling-rate.md)

[**KSPROPERTY\_AUDIO\_EQ\_BANDS**](ksproperty-audio-eq-bands.md)

[**KSPROPERTY\_AUDIO\_EQ\_LEVEL**](ksproperty-audio-eq-level.md)

[**KSPROPERTY\_AUDIO\_FILTER\_STATE**](ksproperty-audio-filter-state.md)

[**KSPROPERTY\_音频\_延迟**](ksproperty-audio-latency.md)

[**KSPROPERTY\_音频\_线性\_缓冲区\_位置**](ksproperty-audio-linear-buffer-position.md)

[**KSPROPERTY\_音频\_响度**](ksproperty-audio-loudness.md)

[**KSPROPERTY\_音频\_制造\_GUID**](ksproperty-audio-manufacture-guid.md)

[**KSPROPERTY\_音频\_MIC\_数组\_GEOMETRY**](ksproperty-audio-mic-array-geometry.md)

[**KSPROPERTY\_AUDIO\_MIC\_SENSITIVITY**](ksproperty-audio-mic-sensitivity.md)

[**KSPROPERTY\_AUDIO\_MIC\_SNR**](ksproperty-audio-mic-snr.md)

[**KSPROPERTY\_音频\_MID**](ksproperty-audio-mid.md)

[**KSPROPERTY\_AUDIO\_MIX\_LEVEL\_CAPS**](ksproperty-audio-mix-level-caps.md)

[**KSPROPERTY\_AUDIO\_MIX\_LEVEL\_TABLE**](ksproperty-audio-mix-level-table.md)

[**KSPROPERTY\_AUDIO\_MUTE**](ksproperty-audio-mute.md)

[**KSPROPERTY\_AUDIO\_MUX\_SOURCE**](ksproperty-audio-mux-source.md)

[**KSPROPERTY\_AUDIO\_NUM\_EQ\_BANDS**](ksproperty-audio-num-eq-bands.md)

[**KSPROPERTY\_AUDIO\_PEAKMETER**](ksproperty-audio-peakmeter.md)

[**KSPROPERTY\_AUDIO\_PEAKMETER2**](ksproperty-audio-peakmeter2.md)

[**KSPROPERTY\_音频\_位置**](ksproperty-audio-position.md)

[**KSPROPERTY\_AUDIO\_POSITIONEX**](ksproperty-audio-positionex.md)

[**KSPROPERTY\_AUDIO\_PREFERRED\_STATUS**](ksproperty-audio-preferred-status.md)

[**KSPROPERTY\_AUDIO\_PRESENTATION\_POSITION**](ksproperty-audio-presentation-position.md)

[**KSPROPERTY\_音频\_产品\_GUID**](ksproperty-audio-product-guid.md)

[**KSPROPERTY\_AUDIO\_QUALITY**](ksproperty-audio-quality.md)

[**KSPROPERTY\_AUDIO\_REVERB\_LEVEL**](ksproperty-audio-reverb-level.md)

[**KSPROPERTY\_AUDIO\_REVERB\_TIME**](ksproperty-audio-reverb-time.md)

[**KSPROPERTY\_AUDIO\_SAMPLING\_RATE**](ksproperty-audio-sampling-rate.md)

[**KSPROPERTY\_音频\_立体声\_增强**](ksproperty-audio-stereo-enhance.md)

[**KSPROPERTY\_音频\_立体声\_演讲者\_GEOMETRY**](ksproperty-audio-stereo-speaker-geometry.md)

[**KSPROPERTY\_音频\_环绕\_编码**](ksproperty-audio-surround-encode.md)

[**KSPROPERTY\_AUDIO\_TREBLE**](ksproperty-audio-treble.md)

[**KSPROPERTY\_音频\_VOLUMELEVEL**](ksproperty-audio-volumelevel.md)

[**KSPROPERTY\_音频\_VOLUMELIMIT\_ENGAGED**](ksproperty-audio-volumelimit-engaged.md)

[**KSPROPERTY\_音频\_WAVERT\_当前\_编写\_位置**](ksproperty-audio-wavert-current-write-position.md)

[**KSPROPERTY\_音频\_WAVERT\_当前\_编写\_LASTBUFFER\_位置**](ksproperty-audio-wavert-current-write-lastbuffer-position.md)

[**KSPROPERTY\_音频\_宽\_模式**](ksproperty-audio-wide-mode.md)

[**KSPROPERTY\_音频\_宽度**](ksproperty-audio-wideness.md)

 

 





