---
title: Ksmedia.h
description: 本部分包含 Ksmedia 标头的参考主题。
ms.assetid: D5654BC1-45F5-4EC9-9E93-60318EF4C159
ms.date: 11/27/2018
ms.localizationpriority: medium
ms.openlocfilehash: 7b7d75c681eebfad714520911a5660ca2424a613
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89207035"
---
# <a name="ksmediah"></a>Ksmedia.h

本部分包含 Ksmedia 标头的参考主题。

## <a name="span-idin_this_sectionspanin-this-section"></a><span id="in_this_section"></span>本部分中的内容

|主题|说明|
|--- |--- |
|[KSEVENT_CONTROL_CHANGE](ksevent-control-change.md)|KSEVENT_CONTROL_CHANGE 事件指示在表示硬件卷控制旋钮、静音开关或其他类型手动控制的节点上发生了控件值更改。  (操作数据) 的事件值类型是一个 KSEVENTDATA 结构，它指定要用于事件的通知类型。|Pin|[KSE_NODE](/windows-hardware/drivers/ddi/ks/ns-ks-kse_node)|[KSEVENTDATA](/windows-hardware/drivers/ddi/ks/ns-ks-kseventdata)|
|[KSEVENT_LOOPEDSTREAMING_POSITION](ksevent-loopedstreaming-position.md)|KSEVENT_LOOPEDSTREAMING_POSITION 事件指示音频流已到达循环缓冲区中的指定位置。|
|[KSEVENT_SOUNDDETECTOR_MATCHDETECTED](ksevent-sounddetector-matchdetected.md)|KSEVENT_SOUNDDETECTOR_MATCHDETECTED 事件由音频驱动程序生成，每当检测到匹配项时，通知操作系统。|
|[KSJACK_DESCRIPTION](ksjack-description.md)|KSJACK_DESCRIPTION 结构指定音频插孔的物理属性。|
|[KSJACK_DESCRIPTION2](ksjack-description2.md)|KSJACK_DESCRIPTION2 结构指定支持插孔存在检测的插孔的功能和当前状态。|
|[KSPROPERTY_AC3_ALTERNATE_AUDIO](ksproperty-ac3-alternate-audio.md)|KSPROPERTY_AC3_ALTERNATE_AUDIO 属性指定是否应将 AC 3 编码流中的两个 mono 通道解释为立体声对或两个独立的程序通道。|
|[KSPROPERTY_AC3_BIT_STREAM_MODE](ksproperty-ac3-bit-stream-mode.md)|KSPROPERTY_AC3_BIT_STREAM_MODE 属性指定位流模式，这是编码为 AC 3 流的音频服务的类型。|
|[KSPROPERTY_AC3_DIALOGUE_LEVEL](ksproperty-ac3-dialogue-level.md)|KSPROPERTY_AC3_DIALOGUE_LEVEL 属性指定 AC 3 编码流中音频程序内的口述对话的平均音量级别。|
|[KSPROPERTY_AC3_DOWNMIX](ksproperty-ac3-downmix.md)|KSPROPERTY_AC3_DOWNMIX 属性指定是否需要 downmixed 在 AC 3 编码流中使用程序通道来容纳扬声器配置。|
|[KSPROPERTY_AC3_ERROR_CONCEALMENT](ksproperty-ac3-error-concealment.md)|KSPROPERTY_AC3_ERROR_CONCEALMENT 属性指定在播放过程中应隐藏 AC 3 编码流中的错误的方式。|
|[KSPROPERTY_AC3_LANGUAGE_CODE](ksproperty-ac3-language-code.md)|KSPROPERTY_AC3_LANGUAGE_CODE 属性指定 AC 3 编码流的语言代码。|
|[KSPROPERTY_AC3_ROOM_TYPE](ksproperty-ac3-room-type.md)|KSPROPERTY_AC3_ROOM_TYPE 属性指定生成最终音频会话的混合聊天室的类型和校准。|
|[KSPROPERTY_AEC_MODE](ksproperty-aec-mode.md)|KSPROPERTY_AEC_MODE 属性用于控制 AEC 节点的操作模式。 这是 AEC 节点 ([KSNODETYPE_ACOUSTIC_ECHO_CANCEL](ksnodetype-acoustic-echo-cancel.md)) 的可选属性。|
|[KSPROPERTY_AEC_NOISE_FILL_ENABLE](ksproperty-aec-noise-fill-enable.md)|KSPROPERTY_AEC_NOISE_FILL_ENABLE 属性用于启用和禁用背景杂色填充。 这是 AEC 节点 ([KSNODETYPE_ACOUSTIC_ECHO_CANCEL](ksnodetype-acoustic-echo-cancel.md)) 的可选属性。|
|[KSPROPERTY_AEC_STATUS](ksproperty-aec-status.md)|KSPROPERTY_AEC_STATUS 属性用于监视 AEC 节点 ([KSNODETYPE_ACOUSTIC_ECHO_CANCEL](ksnodetype-acoustic-echo-cancel.md)) 的状态。 这是 AEC 节点的一个可选属性。|
|[KSPROPERTY_AUDIO_3D_INTERFACE](ksproperty-audio-3d-interface.md)|KSPROPERTY_AUDIO_3D_INTERFACE 属性指定了用于处理声音缓冲区中的数据的3D 算法。|
|[KSPROPERTY_AUDIO_AGC](ksproperty-audio-agc.md)|KSPROPERTY_AUDIO_AGC 属性指定 AGC 节点 ([KSNODETYPE_AGC](ksnodetype-agc.md)) 中通道的 AGC (自动获得控制) 的状态。|
|[KSPROPERTY_AUDIO_ALGORITHM_INSTANCE](ksproperty-audio-algorithm-instance.md)|KSPROPERTY_AUDIO_ALGORITHM_INSTANCE 属性指定了用于实现节点应用于音频数据流的第三方效果 (DSP) 算法的数字信号处理。 为此属性定义的效果包括声音回声取消和干扰抑制。|
|[KSPROPERTY_AUDIO_BASS](ksproperty-audio-bass.md)|KSPROPERTY_AUDIO_BASS 属性指定低音节点中通道的低音级别， ([KSNODETYPE_TONE](ksnodetype-tone.md)) 。|
|[KSPROPERTY_AUDIO_BASS_BOOST](ksproperty-audio-bass-boost.md)|KSPROPERTY_AUDIO_BASS_BOOST 属性为色调节点 ([KSNODETYPE_TONE](ksnodetype-tone.md)) 中的通道启用和禁用低音提升。|
|[KSPROPERTY_AUDIO_BUFFER_DURATION](ksproperty-audio-buffer-duration.md)|KSPROPERTY_AUDIO_BUFFER_DURATION 属性允许将客户端应用程序缓冲区的大小报告为时间长度。|
|[KSPROPERTY_AUDIO_CHANNEL_CONFIG](ksproperty-audio-channel-config.md)|KSPROPERTY_AUDIO_CHANNEL_CONFIG 属性指定节点输出的音频流中的通道的实际空间位置。|
|[KSPROPERTY_AUDIO_CHORUS_LEVEL](ksproperty-audio-chorus-level.md)|KSPROPERTY_AUDIO_CHORUS_LEVEL 属性指定 CHORUS 级别。 这是 ([KSNODETYPE_CHORUS](ksnodetype-chorus.md)) 的 chorus 节点的属性。|
|[KSPROPERTY_AUDIO_CHORUS_MODULATION_DEPTH](ksproperty-audio-chorus-modulation-depth.md)|KSPROPERTY_AUDIO_CHORUS_MODULATION_DEPTH 属性指定 CHORUS 的调制深度。 这是 ([KSNODETYPE_CHORUS](ksnodetype-chorus.md)) 的 chorus 节点的属性。|
|[KSPROPERTY_AUDIO_CHORUS_MODULATION_RATE](ksproperty-audio-chorus-modulation-rate.md)|KSPROPERTY_AUDIO_CHORUS_MODULATION_RATE 属性指定 CHORUS 的调制速率。 这是 ([KSNODETYPE_CHORUS](ksnodetype-chorus.md)) 的 chorus 节点的属性。|
|[KSPROPERTY_AUDIO_COPY_PROTECTION](ksproperty-audio-copy-protection.md)|KSPROPERTY_AUDIO_COPY_PROTECTION 属性指定音频流的复制保护状态。|
|[KSPROPERTY_AUDIO_CPU_RESOURCES](ksproperty-audio-cpu-resources.md)|KSPROPERTY_AUDIO_CPU_RESOURCES 属性指定是否在硬件中实现节点的功能，或在主机 CPU 上运行的软件中进行模拟。|
|[KSPROPERTY_AUDIO_DELAY](ksproperty-audio-delay.md)|KSPROPERTY_AUDIO_DELAY 属性指示延迟节点 ([KSNODETYPE_DELAY](ksnodetype-delay.md)) 引入指定通道的时间延迟。|
|[KSPROPERTY_AUDIO_DEMUX_DEST](ksproperty-audio-demux-dest.md)|KSPROPERTY_AUDIO_DEMUX_DEST 属性指定信号分离器定向到其输入流的目标流。 这是 ([KSNODETYPE_DEMUX](ksnodetype-demux.md)) 的多路分解器节点的属性。|
|[KSPROPERTY_AUDIO_DEV_SPECIFIC](ksproperty-audio-dev-specific.md)|KSPROPERTY_AUDIO_DEV_SPECIFIC 属性用于访问特定于设备的节点 ([KSNODETYPE_DEV_SPECIFIC](ksnodetype-dev-specific.md)) 中特定于设备的属性。|
|[KSPROPERTY_AUDIO_DYNAMIC_RANGE](ksproperty-audio-dynamic-range.md)|KSPROPERTY_AUDIO_DYNAMIC_RANGE 属性指定从响度节点输出的音频流的动态范围 ([KSNODETYPE_LOUDNESS](ksnodetype-loudness.md)) 。|
|[KSPROPERTY_AUDIO_DYNAMIC_SAMPLING_RATE](ksproperty-audio-dynamic-sampling-rate.md)|KSPROPERTY_AUDIO_DYNAMIC_SAMPLING_RATE 属性用于启用和禁用节点采样率的动态跟踪。|
|[KSPROPERTY_AUDIO_EQ_BANDS](ksproperty-audio-eq-bands.md)|KSPROPERTY_AUDIO_EQ_BANDS 属性指定均衡表中的一组频段。 这是 ([KSNODETYPE_EQUALIZER](ksnodetype-equalizer.md)) 的 EQ 节点中通道的获取属性。|
|[KSPROPERTY_AUDIO_EQ_LEVEL](ksproperty-audio-eq-level.md)|KSPROPERTY_AUDIO_EQ_LEVEL 属性指定包含 n 个 frequency 区段条目的均衡表的均衡级别。 这是 EQ 节点中通道的属性 ([KSNODETYPE_EQUALIZER](ksnodetype-equalizer.md)) 。|
|[KSPROPERTY_AUDIO_FILTER_STATE](ksproperty-audio-filter-state.md)|KSPROPERTY_AUDIO_FILTER_STATE 属性用于查询 GFX 筛选器，以获取它支持的属性集的列表。 列表以属性集 Guid 数组的形式进行检索。|
|[KSPROPERTY_AUDIO_LATENCY](ksproperty-audio-latency.md)|KSPROPERTY_AUDIO_LATENCY 属性用于报告与流关联的 (或音频缓冲) 数量的延迟。|
|[KSPROPERTY_AUDIO_LINEAR_BUFFER_POSITION](ksproperty-audio-linear-buffer-position.md)|KSPROPERTY_AUDIO_LINEAR_BUFFER_POSITION 属性请求检索一个数字，该数字表示自流开始以来 DMA 从音频缓冲区中提取的字节数。|
|[KSPROPERTY_AUDIO_LOUDNESS](ksproperty-audio-loudness.md)|KSPROPERTY_AUDIO_LOUDNESS 属性指定是否为响度节点 ([KSNODETYPE_LOUDNESS](ksnodetype-loudness.md)) 中的通道启用或禁用响度 (总体动态范围和低音提升) 。|
|[KSPROPERTY_AUDIO_MANUFACTURE_GUID](ksproperty-audio-manufacture-guid.md)|此参数名称保留供将来使用。|
|[KSPROPERTY_AUDIO_MIC_ARRAY_GEOMETRY](ksproperty-audio-mic-array-geometry.md)|KSPROPERTY_AUDIO_MIC_ARRAY_GEOMETRY 属性指定麦克风阵列的几何。|
|[KSPROPERTY_AUDIO_MIC_SENSITIVITY](ksproperty-audio-mic-sensitivity.md)|KSPROPERTY_AUDIO_MIC_SENSITIVITY 属性以分贝相对于 (dBFS) 单位指定麦克风敏感度。|
|[KSPROPERTY_AUDIO_MIC_SNR](ksproperty-audio-mic-snr.md)|KSPROPERTY_AUDIO_MIC_SNR 属性指定) dB 单位的 (SNR 度量值的麦克风信号。|
|[KSPROPERTY_AUDIO_MID](ksproperty-audio-mid.md)|KSPROPERTY_AUDIO_MID 属性指定色调节点中通道的中间频率级别， ([KSNODETYPE_TONE](ksnodetype-tone.md)) 。|
|[KSPROPERTY_AUDIO_MIX_LEVEL_CAPS](ksproperty-audio-mix-level-caps.md)|KSPROPERTY_AUDIO_MIX_LEVEL_CAPS 属性指定 supermixer 节点的混合级别功能 ([KSNODETYPE_SUPERMIX](ksnodetype-supermix.md)) 。 单个 get 属性请求检索输入和输出通道的所有组合的信息。|
|[KSPROPERTY_AUDIO_MIX_LEVEL_TABLE](ksproperty-audio-mix-level-table.md)|KSPROPERTY_AUDIO_MIX_LEVEL_TABLE 属性指定 supermixer 节点 ([KSNODETYPE_SUPERMIX](ksnodetype-supermix.md)) 的混合级别。 它提供所有输入和输出通道的信息。|
|[KSPROPERTY_AUDIO_MUTE](ksproperty-audio-mute.md)|KSPROPERTY_AUDIO_MUTE 属性指定静音节点上的通道是否 ([KSNODETYPE_MUTE](ksnodetype-mute.md)) 静音。|
|[KSPROPERTY_AUDIO_MUX_SOURCE](ksproperty-audio-mux-source.md)|KSPROPERTY_AUDIO_MUX_SOURCE 属性指定多路复用器的输出流的源。 这是 MUX 节点 ([KSNODETYPE_MUX](ksnodetype-mux.md)) 的属性。|
|[KSPROPERTY_AUDIO_NUM_EQ_BANDS](ksproperty-audio-num-eq-bands.md)|KSPROPERTY_AUDIO_NUM_EQ_BANDS 属性用于检索均衡表中的频率带区数。 这是 ([KSNODETYPE_EQUALIZER](ksnodetype-equalizer.md)) 的 EQ 节点中通道的获取属性。|
|[KSPROPERTY_AUDIO_PEAKMETER](ksproperty-audio-peakmeter.md)|KSPROPERTY_AUDIO_PEAKMETER 属性检索 PEAKMETER 节点上次重置后在 PEAKMETER 节点上发生的最高音频信号级别， ([KSNODETYPE_PEAKMETER](ksnodetype-peakmeter.md)) 。|
|[KSPROPERTY_AUDIO_PEAKMETER2](ksproperty-audio-peakmeter2.md)|Windows 8 引入了 KSPROPERTY_AUDIO_PEAKMETER2 属性，该属性报告自上次重置 peakmeter 节点后，在 peakmeter 节点上发生的最大音频信号级别 (KSNODETYPE_PEAKMETER) 。|
|[KSPROPERTY_AUDIO_POSITION](ksproperty-audio-position.md)|KSPROPERTY_AUDIO_POSITION 属性为 pin 的音频流指定声音缓冲区中播放和写入光标的当前位置。|
|[KSPROPERTY_AUDIO_POSITIONEX](ksproperty-audio-positionex.md)|KSPROPERTY_AUDIO_POSITIONEX 属性为调用方提供有关内核流式处理 (KS) 音频驱动程序的流位置和关联时间戳信息。|
|[KSPROPERTY_AUDIO_PREFERRED_STATUS](ksproperty-audio-preferred-status.md)|KSPROPERTY_AUDIO_PREFERRED_STATUS 属性向设备通知设备是系统的首选音频设备。|
|[KSPROPERTY_AUDIO_PRESENTATION_POSITION](ksproperty-audio-presentation-position.md)|KSPROPERTY_AUDIO_PRESENTATION_POSITION 属性请求检索一个结构，该结构指定向终结点呈现的音频数据内的当前位置。|
|[KSPROPERTY_AUDIO_PRODUCT_GUID](ksproperty-audio-product-guid.md)|此参数名称保留供将来使用。|
|[KSPROPERTY_AUDIO_QUALITY](ksproperty-audio-quality.md)|KSPROPERTY_AUDIO_QUALITY 属性指定节点输出流的质量级别。 这是 SRC 节点 ([KSNODETYPE_SRC](ksnodetype-src.md)) 的属性。|
|[KSPROPERTY_AUDIO_REVERB_LEVEL](ksproperty-audio-reverb-level.md)|KSPROPERTY_AUDIO_REVERB_LEVEL 属性指定当前 reverberation 级别。 这是 ([KSNODETYPE_REVERB](ksnodetype-reverb.md)) 的 "回音" 节点的属性。|
|[KSPROPERTY_AUDIO_REVERB_TIME](ksproperty-audio-reverb-time.md)|KSPROPERTY_AUDIO_REVERB_TIME 属性指定 reverberation 时间。 这是 ([KSNODETYPE_REVERB](ksnodetype-reverb.md)) 的 "回音" 节点的属性。|
|[KSPROPERTY_AUDIO_SAMPLING_RATE](ksproperty-audio-sampling-rate.md)|KSPROPERTY_AUDIO_SAMPLING_RATE 属性指定节点采样其输入流以生成其输出流的速率。|
|[KSPROPERTY_AUDIO_STEREO_ENHANCE](ksproperty-audio-stereo-enhance.md)|此参数名称保留供将来使用。|
|[KSPROPERTY_AUDIO_STEREO_SPEAKER_GEOMETRY](ksproperty-audio-stereo-speaker-geometry.md)|KSPROPERTY_AUDIO_STEREO_SPEAKER_GEOMETRY 属性与 [KSPROPERTY_AUDIO_CHANNEL_CONFIG](ksproperty-audio-channel-config.md) 结合使用来实现硬件加速3d 音频的 DirectSound 扬声器配置属性。 这是 DAC 节点 ([KSNODETYPE_DAC](ksnodetype-dac.md)) 和3d 节点 ([KSNODETYPE_3D_EFFECTS](ksnodetype-3d-effects.md)) 的可选属性。|
|[KSPROPERTY_AUDIO_SURROUND_ENCODE](ksproperty-audio-surround-encode.md)|KSPROPERTY_AUDIO_SURROUND_ENCODE 属性指定是启用还是禁用筛选器的环绕编码器。 环绕编码器节点 ([KSNODETYPE_PROLOGIC_ENCODER](ksnodetype-prologic-encoder.md)) 执行杜包围 Pro 逻辑编码。|
|[KSPROPERTY_AUDIO_TREBLE](ksproperty-audio-treble.md)|KSPROPERTY_AUDIO_TREBLE 属性为色调节点中通道指定高音级别， ([KSNODETYPE_TONE](ksnodetype-tone.md)) 。|
|[KSPROPERTY_AUDIO_VOLUMELEVEL](ksproperty-audio-volumelevel.md)|KSPROPERTY_AUDIO_VOLUMELEVEL 属性指定 [KSNODETYPE_VOLUME](ksnodetype-volume.md))  (卷节点中通道的音量级别。|
|[KSPROPERTY_AUDIO_VOLUMELIMIT_ENGAGED](ksproperty-audio-volumelimit-engaged.md)|KSPROPERTY_AUDIO_VOLUMELIMIT_ENGAGED 是一种新的 KS 属性，已添加到 Windows 8.1 的 KSPROPSETID_Audio 属性集中。|
|[KSPROPERTY_AUDIO_WAVERT_CURRENT_WRITE_POSITION](ksproperty-audio-wavert-current-write-position.md)|KSPROPERTY_AUDIO_WAVERT_CURRENT_WRITE_POSITION 属性请求指定 WaveRT 缓冲区的当前写入位置（以字节为单位）。 卸载驱动程序可以使用此写入位置信息来了解 WaveRT 缓冲区中的有效数据量。|
|[KSPROPERTY_AUDIO_WAVERT_CURRENT_WRITE_LASTBUFFER_POSITION](ksproperty-audio-wavert-current-write-lastbuffer-position.md)|KSPROPERTY_AUDIO_WAVERT_CURRENT_WRITE_LASTBUFFER_POSITION 属性用于指示音频缓冲区中的最后一个有效字节。|
|[KSPROPERTY_AUDIO_WIDE_MODE](ksproperty-audio-wide-mode.md)|此参数名称保留供将来使用。|
|[KSPROPERTY_AUDIO_WIDENESS](ksproperty-audio-wideness.md)|KSPROPERTY_AUDIO_WIDENESS 属性指定立体声图像的宽度 (明显宽度) 。|
|[KSPROPERTY_AUDIOENGINE](ksproperty-audioengine.md)|此枚举定义 [KSPROPSETID_AudioEngine](kspropsetid-audioengine.md) 属性集中包含的属性，必须由 [KSNODETYPE_AUDIO_ENGINE](ksnodetype-audio-engine.md) 节点支持。|
|[KSPROPERTY_AUDIOENGINE_BUFFER_SIZE_RANGE](ksproperty-audioengine-buffer-size-limits.md)|[KSPROPERTY_AUDIOENGINE_BUFFER_SIZE_RANGE](ksproperty-audioengine-buffer-size-limits.md)属性指示在调用时，硬件音频引擎可为给定数据格式支持的缓冲区的最小大小和最大大小。 指定缓冲区大小（以字节为单位）。|
|[KSPROPERTY_AUDIOENGINE_DESCRIPTOR](ksproperty-audioengine-descriptor.md)|适用于卸载的硬件解决方案的音频驱动程序使用 [KSPROPERTY_AUDIOENGINE_DESCRIPTOR](ksproperty-audioengine-descriptor.md) 提供有关表示硬件音频引擎的节点的信息。|
|[KSPROPERTY_AUDIOENGINE_DEVICEFORMAT](ksproperty-audioengine-deviceformat.md)|[KSPROPERTY_AUDIOENGINE_DEVICEFORMAT](ksproperty-audioengine-deviceformat.md)属性请求检索或更改音频引擎节点的状态，有关其设备格式设置。|
|[KSPROPERTY_AUDIOENGINE_GFXENABLE](ksproperty-audioengine-gfx-enable.md)|[KSPROPERTY_AUDIOENGINE_GFXENABLE](ksproperty-audioengine-gfx-enable.md)属性请求允许音频驱动程序检索或更改音频引擎节点的状态，这与它的全局效果处理能力相关。|
|[KSPROPERTY_AUDIOENGINE_LFXENABLE](ksproperty-audioengine-lfx-enable.md)|[KSPROPERTY_AUDIOENGINE_LFXENABLE](ksproperty-audioengine-lfx-enable.md)属性请求检索或更改音频引擎节点的状态，有关其本地效果处理能力。|
|[KSPROPERTY_AUDIOENGINE_LOOPBACK_PROTECTION](ksproperty-audioengine-loopback-protection.md)|[KSPROPERTY_AUDIOENGINE_LOOPBACK_PROTECTION](ksproperty-audioengine-loopback-protection.md)属性请求允许音频驱动程序设置音频引擎节点的环回保护状态。|
|[KSPROPERTY_AUDIOENGINE_MIXFORMAT](ksproperty-audioengine-mixformat.md)|[KSPROPERTY_AUDIOENGINE_MIXFORMAT](ksproperty-audioengine-mixformat.md)属性请求在硬件音频引擎中检索混音器的设置。|
|[KSPROPERTY_AUDIOENGINE_SUPPORTEDDEVICEFORMATS](ksproperty-audioengine-supporteddeviceformats.md)|[KSPROPERTY_AUDIOENGINE_SUPPORTEDDEVICEFORMATS](ksproperty-audioengine-supporteddeviceformats.md)属性请求检索硬件音频引擎支持的设备格式。|
|[KSPROPERTY_AUDIOENGINE_VOLUMELEVEL](ksproperty-audioengine-volumelevel.md)|[KSPROPERTY_AUDIOENGINE_VOLUMELEVEL](ksproperty-audioengine-volumelevel.md)属性指定给定流中通道的音量级别。|
|[KSPROPERTY_AUDIOGFX_CAPTURETARGETDEVICEID](ksproperty-audiogfx-capturetargetdeviceid.md)|KSPROPERTY_AUDIOGFX_CAPTURETARGETDEVICEID 属性用于通知 GFX 筛选器，该筛选器是捕获流源的音频设备的即插即用设备 ID。|
|[KSPROPERTY_AUDIOGFX_RENDERTARGETDEVICEID](ksproperty-audiogfx-rendertargetdeviceid.md)|KSPROPERTY_AUDIOGFX_RENDERTARGETDEVICEID 属性用于通知 GFX 筛选器，其中显示了呈现最终音频组合的音频设备的即插即用设备 ID。|
|[KSPROPERTY_AUDIOMODULE](ksproperty-audiomodule.md)|KSPROPERTY_AUDIOMODULE 枚举定义音频驱动程序用于传达有关合作伙伴定义的音频模块的信息的常量。|
|[KSPROPERTY_AUDIOSIGNALPROCESSING](ksproperty-audiosignalprocessing.md)|KSPROPERTY_AUDIOSIGNALPROCESSING 枚举定义音频驱动程序在与 pin 上的音频处理模式连接时使用的常量。|
|[KSPROPERTY_AUDIOSIGNALPROCESSING_MODES](ksproperty-audiosignalprocessing-modes.md)|KSPROPERTY_AUDIOSIGNALPROCESSING_MODES 属性返回 pin 工厂支持的音频信号处理模式的列表。|
|[KSPROPERTY_DIRECTSOUND3DBUFFER_ALL](ksproperty-directsound3dbuffer-all.md)|KSPROPERTY_DIRECTSOUND3DBUFFER_ALL 属性用于获取或设置指定缓冲区的所有 DirectSound 3D 缓冲区属性。|
|[KSPROPERTY_DIRECTSOUND3DBUFFER_CONEANGLES](ksproperty-directsound3dbuffer-coneangles.md)|KSPROPERTY_DIRECTSOUND3DBUFFER_CONEANGLES 属性指定3D 声音缓冲区的声音投影圆锥的内部和外部锥角。|
|[KSPROPERTY_DIRECTSOUND3DBUFFER_CONEORIENTATION](ksproperty-directsound3dbuffer-coneorientation.md)|KSPROPERTY_DIRECTSOUND3DBUFFER_CONEORIENTATION 属性指定三维声音缓冲区的声音投影圆锥的方向。|
|[KSPROPERTY_DIRECTSOUND3DBUFFER_CONEOUTSIDEVOLUME](ksproperty-directsound3dbuffer-coneoutsidevolume.md)|KSPROPERTY_DIRECTSOUND3DBUFFER_CONEOUTSIDEVOLUME 属性指定3D 声音缓冲区的 "圆锥外" 音量。|
|[KSPROPERTY_DIRECTSOUND3DBUFFER_MAXDISTANCE](ksproperty-directsound3dbuffer-maxdistance.md)|KSPROPERTY_DIRECTSOUND3DBUFFER_MAXDISTANCE 属性指定三维声音缓冲区的最大距离。|
|[KSPROPERTY_DIRECTSOUND3DBUFFER_MINDISTANCE](ksproperty-directsound3dbuffer-mindistance.md)|KSPROPERTY_DIRECTSOUND3DBUFFER_MINDISTANCE 属性指定三维声音缓冲区的最小距离。|
|[KSPROPERTY_DIRECTSOUND3DBUFFER_MODE](ksproperty-directsound3dbuffer-mode.md)|KSPROPERTY_DIRECTSOUND3DBUFFER_MODE 属性指定三维声音缓冲区的处理模式。|
|[KSPROPERTY_DIRECTSOUND3DBUFFER_POSITION](ksproperty-directsound3dbuffer-position.md)|KSPROPERTY_DIRECTSOUND3DBUFFER_POSITION 属性指定三维声音缓冲区的位置。|
|[KSPROPERTY_DIRECTSOUND3DBUFFER_VELOCITY](ksproperty-directsound3dbuffer-velocity.md)|KSPROPERTY_DIRECTSOUND3DBUFFER_VELOCITY 属性指定三维声音缓冲区的速度。|
|[KSPROPERTY_DIRECTSOUND3DLISTENER_ALL](ksproperty-directsound3dlistener-all.md)|KSPROPERTY_DIRECTSOUND3DLISTENER_ALL 属性用于设置或获取指定侦听器 ID 的所有 DirectSound 3D 侦听器属性。|
|[KSPROPERTY_DIRECTSOUND3DLISTENER_ALLOCATION](ksproperty-directsound3dlistener-allocation.md)|KSPROPERTY_DIRECTSOUND3DLISTENER_ALLOCATION 属性用于告知驱动程序何时为其侦听器数据分配并释放存储。 在创建侦听器时分配存储，并在删除侦听器时释放存储。 此属性还可用于查询驱动程序是否当前已分配侦听器数据。|
|[KSPROPERTY_DIRECTSOUND3DLISTENER_BATCH](ksproperty-directsound3dlistener-batch.md)|KSPROPERTY_DIRECTSOUND3DLISTENER_BATCH 属性指定3D 侦听器的批处理模式设置。|
|[KSPROPERTY_DIRECTSOUND3DLISTENER_DISTANCEFACTOR](ksproperty-directsound3dlistener-distancefactor.md)|KSPROPERTY_DIRECTSOUND3DLISTENER_DISTANCEFACTOR 属性指定应应用于任何距离值的距离系数。|
|[KSPROPERTY_DIRECTSOUND3DLISTENER_DOPPLERFACTOR](ksproperty-directsound3dlistener-dopplerfactor.md)|KSPROPERTY_DIRECTSOUND3DLISTENER_DOPPLERFACTOR 属性指定3D 侦听器的 Doppler 系数。|
|[KSPROPERTY_DIRECTSOUND3DLISTENER_ORIENTATION](ksproperty-directsound3dlistener-orientation.md)|KSPROPERTY_DIRECTSOUND3DLISTENER_ORIENTATION 属性指定3D 侦听器的方向。|
|[KSPROPERTY_DIRECTSOUND3DLISTENER_POSITION](ksproperty-directsound3dlistener-position.md)|KSPROPERTY_DIRECTSOUND3DLISTENER_POSITION 属性指定3D 侦听器的位置。|
|[KSPROPERTY_DIRECTSOUND3DLISTENER_ROLLOFFFACTOR](ksproperty-directsound3dlistener-rollofffactor.md)|KSPROPERTY_DIRECTSOUND3DLISTENER_ROLLOFFFACTOR 属性指定3D 侦听器的 rolloff 系数。|
|[KSPROPERTY_DIRECTSOUND3DLISTENER_VELOCITY](ksproperty-directsound3dlistener-velocity.md)|KSPROPERTY_DIRECTSOUND3DLISTENER_VELOCITY 属性指定3D 侦听器的速度矢量。|
|[KSPROPERTY_FMRX_ANTENNAENDPOINTID](ksproperty-fmrx-antennaendpointid.md)|[KSTOPOLOGY_ENDPOINTID](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_tagkstopology_endpointid)属性包含有关要用作调频天线的终结点的信息。|
|[KSPROPERTY_FMRX_ENDPOINTID](ksproperty-fmrx-endpointid.md)|[KSTOPOLOGY_ENDPOINTID](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_tagkstopology_endpointid)属性包含调频无线电输出/呈现端点的端点 ID。|
|[KSPROPERTY_FMRX_VOLUME](ksproperty-fmrx-volume.md)|[KSPROPERTY_FMRX_VOLUME](ksproperty-fmrx-volume.md)属性控制调频无线电的音量。|
|[KSPROPERTY_HRTF3D_FILTER_FORMAT](ksproperty-hrtf3d-filter-format.md)|KSPROPERTY_HRTF3D_FILTER_FORMAT 属性检索 HRTF 算法使用的筛选器格式。|
|[KSPROPERTY_HRTF3D_INITIALIZE](ksproperty-hrtf3d-initialize.md)|KSPROPERTY_HRTF3D_INITIALIZE 属性指定用来初始化 HRTF 算法的参数值。|
|[KSPROPERTY_HRTF3D_PARAMS](ksproperty-hrtf3d-params.md)|KSPROPERTY_HRTF3D_PARAMS 属性将一组3-d 参数值应用于 HRTF 算法。|
|[KSPROPERTY_ITD3D_PARAMS](ksproperty-itd3d-params.md)|KSPROPERTY_ITD3D_PARAMS 属性用于设置3D 节点的 ITD 算法使用的参数。|
|[KSPROPERTY_JACK](ksproperty-jack.md)|KSPROPERTY_JACK 枚举定义音频插孔结构使用的新属性 Id。|
|[KSPROPERTY_JACK_CONTAINERID](ksproperty-jack-containerid.md)|KSPROPERTY_JACK_CONTAINERID 属性实现为使用筛选器句柄访问的按位数属性。|
|[KSPROPERTY_JACK_DESCRIPTION](ksproperty-jack-description.md)|KSPROPERTY_JACK_DESCRIPTION 属性作为多项、固定的属性实现，该属性通过筛选器句柄进行访问。|
|[KSPROPERTY_JACK_DESCRIPTION2](ksproperty-jack-description2.md)|KSPROPERTY_JACK_DESCRIPTION2 属性实现为使用筛选器句柄访问的按位数属性。|
|[KSPROPERTY_JACK_SINK_INFO](ksproperty-jack-sink-info.md)|KSPROPERTY_JACK_SINK_INFO 属性实现为使用筛选器句柄访问的按位数属性。|
|[KSPROPERTY_ONESHOT_DISCONNECT](ksproperty-oneshot-disconnect.md)|KSPROPERTY_ONESHOT_DISCONNECT 属性用于提示音频驱动程序与蓝牙音频设备断开连接。|
|[KSPROPERTY_ONESHOT_RECONNECT](ksproperty-oneshot-reconnect.md)|KSPROPERTY_ONESHOT_RECONNECT 属性用于提示音频驱动程序尝试连接到蓝牙音频设备。|
|[KSPROPERTY_RTAUDIO_BUFFER](ksproperty-rtaudio-buffer.md)|KSPROPERTY_RTAUDIO_BUFFER 属性指定用于音频数据的驱动程序分配的循环缓冲区。|
|[KSPROPERTY_RTAUDIO_BUFFER_WITH_NOTIFICATION](ksproperty-rtaudio-buffer-with-notification.md)|KSPROPERTY_RTAUDIO_BUFFER_WITH_NOTIFICATION 属性指定用于音频数据的驱动程序分配的循环缓冲区，并标识事件通知要求。|
|[KSPROPERTY_RTAUDIO_CLOCKREGISTER](ksproperty-rtaudio-clockregister.md)|KSPROPERTY_RTAUDIO_CLOCKREGISTER 属性将音频设备的墙壁时钟寄存器映射到客户端可以访问的虚拟内存位置。|
|[KSPROPERTY_RTAUDIO_GETREADPACKET](ksproperty-rtaudio-getreadpacket.md)|KSPROPERTY_RTAUDIO_GETREADPACKET 返回有关捕获的音频数据包的信息。|
|[KSPROPERTY_RTAUDIO_HWLATENCY](ksproperty-rtaudio-hwlatency.md)|KSPROPERTY_RTAUDIO_HWLATENCY 属性检索音频硬件的流延迟及其关联数据路径的说明。|
|[KSPROPERTY_RTAUDIO_PACKETCOUNT](ksproperty-rtaudio-packetcount.md)|KSPROPERTY_RTAUDIO_PACKETCOUNT 返回完全从 WaveRT 缓冲区传输到硬件的 (从1开始的数据包) 计数。|
|[KSPROPERTY_RTAUDIO_POSITIONREGISTER](ksproperty-rtaudio-positionregister.md)|KSPROPERTY_RTAUDIO_POSITIONREGISTER 属性将特定流的音频设备位置注册映射到客户端可以访问的虚拟内存位置。|
|[KSPROPERTY_RTAUDIO_PRESENTATION_POSITION](ksproperty-rtaudio-presentation-position.md)|KSPROPERTY_RTAUDIO_PRESENTATION_POSITION 返回流显示信息。|
|[KSPROPERTY_RTAUDIO_QUERY_NOTIFICATION_SUPPORT](ksproperty-rtaudio-query-notification-support.md)|客户端应用程序使用 KSPROPERTY_RTAUDIO_QUERY_NOTIFICATION_SUPPORT 属性来确定音频驱动程序是否可以在提交的缓冲区上执行的进程完成时通知客户端应用程序。|
|[KSPROPERTY_RTAUDIO_REGISTER_NOTIFICATION_EVENT](ksproperty-rtaudio-register-notification-event.md)|KSPROPERTY_RTAUDIO_REGISTER_NOTIFICATION_EVENT 属性为 DMA 驱动的事件通知注册用户模式事件。 成功调用 [KSPROPERTY_RTAUDIO_BUFFER_WITH_NOTIFICATION](ksproperty-rtaudio-buffer-with-notification.md)后，必须注册事件。|
|[KSPROPERTY_RTAUDIO_SETWRITEPACKET](ksproperty-rtaudio-setwritepacket.md)|KSPROPERTY_RTAUDIO_SETWRITEPACKET 通知驱动程序操作系统已将有效数据写入 WaveRT 缓冲区。|
|[KSPROPERTY_RTAUDIO_UNREGISTER_NOTIFICATION_EVENT](ksproperty-rtaudio-unregister-notification-event.md)|KSPROPERTY_RTAUDIO_UNREGISTER_NOTIFICATION_EVENT 属性从 DMA 驱动的事件通知中注销用户模式事件。|
|[KSPROPERTY_SOUNDDETECTOR](ksproperty-sounddetector.md)|[KSPROPERTY_SOUNDDETECTOR](ksproperty-sounddetector.md)枚举定义用于为还支持检测程序的音频捕获设备注册筛选器的常量。|
|[KSPROPERTY_SOUNDDETECTOR_ARMED](ksproperty-sounddetector-armed.md)|[KSPROPERTY_SOUNDDETECTOR_ARMED](ksproperty-sounddetector-armed.md)属性是探测器的当前武装状态。|
|[KSPROPERTY_SOUNDDETECTOR_MATCHRESULT](ksproperty-sounddetector-matchresult.md)|KSPROPERTY_SOUNDDETECTOR_MATCHRESULT 属性保留匹配项的结果数据。|
|[KSPROPERTY_SOUNDDETECTOR_PATTERNS](ksproperty-sounddetector-patterns.md)|[KSPROPERTY_SOUNDDETECTOR_PATTERNS](ksproperty-sounddetector-patterns.md)属性由操作系统设置，用于配置要检测的关键字。|
|[KSPROPERTY_SOUNDDETECTOR_SUPPORTEDPATTERNS](ksproperty-sounddetector-supportedpatterns.md)|[KSPROPERTY_SOUNDDETECTOR_SUPPORTEDPATTERNS](ksproperty-sounddetector-supportedpatterns.md)属性用于获取 guid 列表，这些 guid 用于标识支持模式的类型。|
|[KSPROPERTY_SYSAUDIO_ATTACH_VIRTUAL_SOURCE](ksproperty-sysaudio-attach-virtual-source.md)|KSPROPERTY_SYSAUDIO_ATTACH_VIRTUAL_SOURCE 属性将虚拟源附加到虚拟音频设备上的 pin 实例。|
|[KSPROPERTY_SYSAUDIO_COMPONENT_ID](ksproperty-sysaudio-component-id.md)|KSPROPERTY_SYSAUDIO_COMPONENT_ID 属性从指定的虚拟音频设备使用的声波渲染设备检索组件 ID。|
|[KSPROPERTY_SYSAUDIO_CREATE_VIRTUAL_SOURCE](ksproperty-sysaudio-create-virtual-source.md)|KSPROPERTY_SYSAUDIO_CREATE_VIRTUAL_SOURCE 属性创建新的虚拟源。|
|[KSPROPERTY_SYSAUDIO_DEVICE_COUNT](ksproperty-sysaudio-device-count.md)|KSPROPERTY_SYSAUDIO_DEVICE_COUNT 属性检索指定 DirectSound 应用程序必须从中选择的虚拟音频设备数的计数。|
|[KSPROPERTY_SYSAUDIO_DEVICE_FRIENDLY_NAME](ksproperty-sysaudio-device-friendly-name.md)|KSPROPERTY_SYSAUDIO_DEVICE_FRIENDLY_NAME 属性检索包含虚拟音频设备友好名称的 Unicode 字符串。|
|[KSPROPERTY_SYSAUDIO_DEVICE_INSTANCE](ksproperty-sysaudio-device-instance.md)|KSPROPERTY_SYSAUDIO_DEVICE_INSTANCE 属性指定虚拟音频设备的当前实例。|
|[KSPROPERTY_SYSAUDIO_DEVICE_INTERFACE_NAME](ksproperty-sysaudio-device-interface-name.md)|KSPROPERTY_SYSAUDIO_DEVICE_INTERFACE_NAME 属性检索包含指定虚拟音频设备的即插即用设备接口名称的 Unicode 字符串。|
|[KSPROPERTY_SYSAUDIO_INSTANCE_INFO](ksproperty-sysaudio-instance-info.md)|KSPROPERTY_SYSAUDIO_INSTANCE_INFO 属性将打开一个虚拟音频设备，并指定该设备的配置标志。|
|[KSPROPERTY_SYSAUDIO_SELECT_GRAPH](ksproperty-sysaudio-select-graph.md)|KSPROPERTY_SYSAUDIO_SELECT_GRAPH 属性用于在图形中显式包含一个可选节点，SysAudio 为虚拟音频设备上的 pin 实例生成此节点。|
|[KSPROPERTY_TELEPHONY_CALLCONTROL](ksproperty-telephony-callcontrol.md)|KSPROPERTY_TELEPHONY_CALLCONTROL 属性用于启动和终止电话呼叫。|
|[KSPROPERTY_TELEPHONY_CALLHOLD](ksproperty-telephony-callhold.md)|[KSPROPERTY_TELEPHONY_CALLHOLD](ksproperty-telephony-callhold.md)属性用于控制电话呼叫的保持状态。|
|[KSPROPERTY_TELEPHONY_CALLINFO](ksproperty-telephony-callinfo.md)|[KSPROPERTY_TELEPHONY_CALLINFO](ksproperty-telephony-callinfo.md)属性用于检索当前调用信息，如调用状态和调用类型。|
|[KSPROPERTY_TELEPHONY_ENDPOINTIDPAIR](ksproperty-telephony-endpointidpair.md)|[KSPROPERTY_TELEPHONY_ENDPOINTIDPAIR](ksproperty-telephony-endpointidpair.md)属性包含移动电话音频路由的呈现和捕获终结点。|
|[KSPROPERTY_TELEPHONY_MUTE_TX](ksproperty-telephony-mute-tx.md)|[KSPROPERTY_TELEPHONY_MUTE_TX](ksproperty-telephony-mute-tx.md)属性用于控制是否将从本地麦克风传输的数据静音到远程端。|
|[KSPROPERTY_TELEPHONY_PROVIDERCHANGE](ksproperty-telephony-providerchange.md)|[KSPROPERTY_TELEPHONY_PROVIDERCHANGE](ksproperty-telephony-providerchange.md)属性用于与音频驱动程序通信， (SRVCC) 的开始或结束。|
|[KSPROPERTY_TELEPHONY_PROVIDERID](ksproperty-telephony-providerid.md)|[KSPROPERTY_TELEPHONY_PROVIDERID](ksproperty-telephony-providerid.md)属性由音频驱动程序用来将提供程序标识符关联到波形筛选器。|
|[KSPROPERTY_TELEPHONY_VOLUME](ksproperty-telephony-volume.md)|[KSPROPERTY_TELEPHONY_VOLUME](ksproperty-telephony-volume.md)属性用于控制所有手机呼叫的卷。|
|[KSPROPERTY_TOPOLOGYNODE_ENABLE](ksproperty-topologynode-enable.md)|KSPROPERTY_TOPOLOGYNODE_ENABLE 属性用于打开或关闭已构建拓扑中的拓扑节点。|
|[KSPROPERTY_TOPOLOGYNODE_RESET](ksproperty-topologynode-reset.md)|KSPROPERTY_TOPOLOGYNODE_RESET 属性完全重置节点，并将其还原为其初始状态。|
|[KSRTAUDIO_BUFFER_PROPERTY](ksrtaudio-buffer-property.md)|KSRTAUDIO_BUFFER_PROPERTY 结构将缓冲区基址和请求的缓冲区大小追加到 [KSPROPERTY](/previous-versions/ff564262(v=vs.85)) 结构。 此结构由客户端用于请求通过 [KSPROPERTY_RTAUDIO_BUFFER](ksproperty-rtaudio-buffer.md)分配音频缓冲区。|