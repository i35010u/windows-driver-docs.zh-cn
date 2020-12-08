---
title: KSPROPSETID \_ 音频
description: KSPROPSETID \_ 音频
keywords:
- KSPROPSETID_Audio
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2f79c8e3a86a436a7762d8465bc6d39b1e92cf07
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96801121"
---
# <a name="kspropsetid_audio"></a>KSPROPSETID \_ 音频


## <span id="ddk_kspropsetid_audio_ks"></span><span id="DDK_KSPROPSETID_AUDIO_KS"></span>


`KSPROPSETID_Audio`属性集指示音频流支持的数据范围和控件。 微型端口驱动程序应支持 KSPROPERTY \_ 音频 \_ 延迟属性。 此属性集中的所有其他属性都是可选的。

在硬件不支持功能的情况下，微型端口驱动程序应为 get 和 set 属性调用返回错误，使上层驱动程序可以处理调用。 例如，不支持音量控制的硬件的微型端口驱动程序应为 [**KSPROPERTY \_ 音频 \_ VOLUMELEVEL**](ksproperty-audio-volumelevel.md) 调用返回错误，从而使堆栈中更高的驱动程序 (如内核混合器) 来设置流的卷。

此集中的属性项由 KSPROPERTY 的 \_ 音频枚举值指定。

以下属性是属性集的一部分 `KSPROPSETID_Audio` ：

[**KSPROPERTY \_ AUDIO \_ 3d \_ 接口**](ksproperty-audio-3d-interface.md)

[**KSPROPERTY \_ 音频 \_ AGC**](ksproperty-audio-agc.md)

[**KSPROPERTY \_ 音频 \_ 算法 \_ 实例**](ksproperty-audio-algorithm-instance.md)

[**KSPROPERTY \_ 音频 \_ 低音**](ksproperty-audio-bass.md)

[**KSPROPERTY \_ 音频 \_ 低音 \_**](ksproperty-audio-bass-boost.md)

[**KSPROPERTY \_ 音频 \_ 缓冲区 \_ 持续时间**](ksproperty-audio-buffer-duration.md)

[**KSPROPERTY \_ 音频 \_ 通道 \_ 配置**](ksproperty-audio-channel-config.md)

[**KSPROPERTY \_ 音频 \_ CHORUS \_ 级别**](ksproperty-audio-chorus-level.md)

[**KSPROPERTY \_ 音频 \_ CHORUS \_ 调制 \_ 深度**](ksproperty-audio-chorus-modulation-depth.md)

[**KSPROPERTY \_ 音频 \_ CHORUS \_ 调制 \_ 速率**](ksproperty-audio-chorus-modulation-rate.md)

[**KSPROPERTY \_ 音频 \_ 复制 \_ 保护**](ksproperty-audio-copy-protection.md)

[**KSPROPERTY \_ 音频 \_ CPU \_ 资源**](ksproperty-audio-cpu-resources.md)

[**KSPROPERTY \_ 音频 \_ 延迟**](ksproperty-audio-delay.md)

[**KSPROPERTY \_ AUDIO \_ 多路分解器 \_ DEST**](ksproperty-audio-demux-dest.md)

[**KSPROPERTY \_ \_ \_ 特定于音频的开发**](ksproperty-audio-dev-specific.md)

[**KSPROPERTY \_ 音频 \_ 动态 \_ 范围**](ksproperty-audio-dynamic-range.md)

[**KSPROPERTY \_ 音频 \_ 动态 \_ 采样 \_ 速率**](ksproperty-audio-dynamic-sampling-rate.md)

[**KSPROPERTY \_ 音频 \_ EQ \_ 带区**](ksproperty-audio-eq-bands.md)

[**KSPROPERTY \_ 音频 \_ EQ \_ 级别**](ksproperty-audio-eq-level.md)

[**KSPROPERTY \_ 音频 \_ 筛选器 \_ 状态**](ksproperty-audio-filter-state.md)

[**KSPROPERTY \_ 音频 \_ 延迟**](ksproperty-audio-latency.md)

[**KSPROPERTY \_ 音频 \_ 线性 \_ 缓冲区 \_ 位置**](ksproperty-audio-linear-buffer-position.md)

[**KSPROPERTY \_ 音频 \_ 响度**](ksproperty-audio-loudness.md)

[**KSPROPERTY \_ 音频 \_ 制造商 \_ GUID**](ksproperty-audio-manufacture-guid.md)

[**KSPROPERTY \_ 音频 \_ MIC \_ 数组 \_ 几何图形**](ksproperty-audio-mic-array-geometry.md)

[**KSPROPERTY\_AUDIO\_MIC\_SENSITIVITY**](ksproperty-audio-mic-sensitivity.md)

[**KSPROPERTY\_AUDIO\_MIC\_SNR**](ksproperty-audio-mic-snr.md)

[**KSPROPERTY \_ 音频 \_ MID**](ksproperty-audio-mid.md)

[**KSPROPERTY \_ 音频 \_ 混合 \_ 电平 \_**](ksproperty-audio-mix-level-caps.md)

[**KSPROPERTY \_ AUDIO \_ 混音 \_ 级 \_ 表**](ksproperty-audio-mix-level-table.md)

[**KSPROPERTY \_ 音频 \_ 静音**](ksproperty-audio-mute.md)

[**KSPROPERTY \_ 音频 \_ MUX \_ 源**](ksproperty-audio-mux-source.md)

[**KSPROPERTY \_ 音频 \_ 数字 \_ EQ \_ 带区**](ksproperty-audio-num-eq-bands.md)

[**KSPROPERTY \_ 音频 \_ PEAKMETER**](ksproperty-audio-peakmeter.md)

[**KSPROPERTY \_ 音频 \_ PEAKMETER2**](ksproperty-audio-peakmeter2.md)

[**KSPROPERTY \_ 音频 \_ 位置**](ksproperty-audio-position.md)

[**KSPROPERTY \_ 音频 \_ POSITIONEX**](ksproperty-audio-positionex.md)

[**KSPROPERTY \_ 音频 \_ 首选 \_ 状态**](ksproperty-audio-preferred-status.md)

[**KSPROPERTY \_ 音频 \_ 演示 \_ 位置**](ksproperty-audio-presentation-position.md)

[**KSPROPERTY \_ 音频 \_ 产品 \_ GUID**](ksproperty-audio-product-guid.md)

[**KSPROPERTY \_ 音频 \_ 质量**](ksproperty-audio-quality.md)

[**KSPROPERTY \_ 音频 \_ 回音 \_ 电平**](ksproperty-audio-reverb-level.md)

[**KSPROPERTY \_ 音频 \_ 回音 \_ 时间**](ksproperty-audio-reverb-time.md)

[**KSPROPERTY \_ 音频 \_ 采样 \_ 率**](ksproperty-audio-sampling-rate.md)

[**KSPROPERTY \_ 音频 \_ 立体声 \_ 增强**](ksproperty-audio-stereo-enhance.md)

[**KSPROPERTY \_ 音频 \_ 立体声 \_ 扬声器 \_ 几何**](ksproperty-audio-stereo-speaker-geometry.md)

[**KSPROPERTY \_ 音频 \_ 环绕 \_ 编码**](ksproperty-audio-surround-encode.md)

[**KSPROPERTY \_ 音频 \_ 高音**](ksproperty-audio-treble.md)

[**KSPROPERTY \_ 音频 \_ VOLUMELEVEL**](ksproperty-audio-volumelevel.md)

[**KSPROPERTY \_ 音频 \_ VOLUMELIMIT \_**](ksproperty-audio-volumelimit-engaged.md)

[**KSPROPERTY \_ 音频 \_ WAVERT \_ 当前 \_ 写入 \_ 位置**](ksproperty-audio-wavert-current-write-position.md)

[**KSPROPERTY \_ 音频 \_ WAVERT \_ 当前 \_ 写入 \_ LASTBUFFER \_ 位置**](ksproperty-audio-wavert-current-write-lastbuffer-position.md)

[**KSPROPERTY \_ 音频 \_ 宽 \_ 模式**](ksproperty-audio-wide-mode.md)

[**KSPROPERTY \_ 音频 \_ 宽度**](ksproperty-audio-wideness.md)

 

 





