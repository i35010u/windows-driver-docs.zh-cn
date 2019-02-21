---
title: Ksmedia.h
description: 本部分包含 Ksmedia.h 标头的参考主题。
ms.assetid: D5654BC1-45F5-4EC9-9E93-60318EF4C159
ms.date: 11/27/2018
ms.localizationpriority: medium
ms.openlocfilehash: 763afb3b4f28d1b66b8476f2d37ce193c0681cdf
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56520559"
---
# <a name="ksmediah"></a>Ksmedia.h

本部分包含 Ksmedia.h 标头的参考主题。

## <a name="span-idinthissectionspanin-this-section"></a><span id="in_this_section"></span>在本部分中

|主题|描述|
|--- |--- |
|[KSEVENT_CONTROL_CHANGE](ksevent-control-change.md)|KSEVENT_CONTROL_CHANGE 事件指示控件值的更改发生在表示硬件音量控制旋钮、 静音开关或手动控制其他类型的节点。 事件值类型 （操作数据） 是通知的 KSEVENTDATA 结构，它指定要对某个事件使用类型。|Pin|[KSE_NODE](https://msdn.microsoft.com/library/windows/hardware/ff561937)|[KSEVENTDATA](https://msdn.microsoft.com/library/windows/hardware/ff561750)|
|[KSEVENT_LOOPEDSTREAMING_POSITION](ksevent-loopedstreaming-position.md)|KSEVENT_LOOPEDSTREAMING_POSITION 事件指示音频流已到达循环缓冲区中的指定的位置。|
|[KSEVENT_SOUNDDETECTOR_MATCHDETECTED](ksevent-sounddetector-matchdetected.md)|音频驱动程序以通知操作系统，每当检测到匹配项时生成 KSEVENT_SOUNDDETECTOR_MATCHDETECTED 事件。|
|[KSJACK_DESCRIPTION](ksjack-description.md)|KSJACK_DESCRIPTION 结构指定的音频插孔的物理属性。|
|[KSJACK_DESCRIPTION2](ksjack-description2.md)|KSJACK_DESCRIPTION2 结构指定的功能和支持插孔在场检测 jack 的当前状态。|
|[KSPROPERTY_AC3_ALTERNATE_AUDIO](ksproperty-ac3-alternate-audio.md)|KSPROPERTY_AC3_ALTERNATE_AUDIO 属性指定的 AC-3 编码流中的两个 mono 通道应解释为立体声对还是两个独立的程序通道。|
|[KSPROPERTY_AC3_BIT_STREAM_MODE](ksproperty-ac3-bit-stream-mode.md)|KSPROPERTY_AC3_BIT_STREAM_MODE 属性指定的位流模式，它是到 ac-3 流编码的音频服务的类型。|
|[KSPROPERTY_AC3_DIALOGUE_LEVEL](ksproperty-ac3-dialogue-level.md)|KSPROPERTY_AC3_DIALOGUE_LEVEL 属性 AC-3 编码流中指定语言音频程序内对话的平均信息量的级别。|
|[KSPROPERTY_AC3_DOWNMIX](ksproperty-ac3-downmix.md)|KSPROPERTY_AC3_DOWNMIX 属性指定是否需要被以适应扬声器配置的混合 AC-3 编码的流中的程序通道。|
|[KSPROPERTY_AC3_ERROR_CONCEALMENT](ksproperty-ac3-error-concealment.md)|KSPROPERTY_AC3_ERROR_CONCEALMENT 属性指定在播放期间应在其中隐藏 AC-3 编码流中的错误的方式。|
|[KSPROPERTY_AC3_LANGUAGE_CODE](ksproperty-ac3-language-code.md)|KSPROPERTY_AC3_LANGUAGE_CODE 属性指定的语言代码的 AC-3 编码流。|
|[KSPROPERTY_AC3_ROOM_TYPE](ksproperty-ac3-room-type.md)|KSPROPERTY_AC3_ROOM_TYPE 属性指定的类型和在其中生成最终的音频会话混合聊天室的校准。|
|[KSPROPERTY_AEC_MODE](ksproperty-aec-mode.md)|KSPROPERTY_AEC_MODE 属性用于控制的操作的 AEC 节点的模式。 此为可选的 AEC 节点的属性 ([KSNODETYPE_ACOUSTIC_ECHO_CANCEL](ksnodetype-acoustic-echo-cancel.md))。|
|[KSPROPERTY_AEC_NOISE_FILL_ENABLE](ksproperty-aec-noise-fill-enable.md)|KSPROPERTY_AEC_NOISE_FILL_ENABLE 属性用于启用和禁用背景噪音填充。 此为可选的 AEC 节点的属性 ([KSNODETYPE_ACOUSTIC_ECHO_CANCEL](ksnodetype-acoustic-echo-cancel.md))。|
|[KSPROPERTY_AEC_STATUS](ksproperty-aec-status.md)|KSPROPERTY_AEC_STATUS 属性用于监视的 AEC 节点状态 ([KSNODETYPE_ACOUSTIC_ECHO_CANCEL](ksnodetype-acoustic-echo-cancel.md))。 这是可选的 AEC 节点的属性。|
|[KSPROPERTY_AUDIO_3D_INTERFACE](ksproperty-audio-3d-interface.md)|KSPROPERTY_AUDIO_3D_INTERFACE 属性指定要用于处理声音缓冲区中的数据的三维算法。|
|[KSPROPERTY_AUDIO_AGC](ksproperty-audio-agc.md)|KSPROPERTY_AUDIO_AGC 属性 AGC 节点中为通道指定 AGC （自动增益控制） 的状态 ([KSNODETYPE_AGC](ksnodetype-agc.md))。|
|[KSPROPERTY_AUDIO_ALGORITHM_INSTANCE](ksproperty-audio-algorithm-instance.md)|KSPROPERTY_AUDIO_ALGORITHM_INSTANCE 属性指定数字信号处理 (DSP) 算法，用于实现节点将应用于的音频数据的流的第三方效果。 为此属性定义的影响包括回声和干扰禁止显示。|
|[KSPROPERTY_AUDIO_BASS](ksproperty-audio-bass.md)|KSPROPERTY_AUDIO_BASS 属性音节点中指定一个通道的低音级别 ([KSNODETYPE_TONE](ksnodetype-tone.md))。|
|[KSPROPERTY_AUDIO_BASS_BOOST](ksproperty-audio-bass-boost.md)|KSPROPERTY_AUDIO_BASS_BOOST 属性启用和禁用通道音节点中的低音增强 ([KSNODETYPE_TONE](ksnodetype-tone.md))。|
|[KSPROPERTY_AUDIO_BUFFER_DURATION](ksproperty-audio-buffer-duration.md)|KSPROPERTY_AUDIO_BUFFER_DURATION 属性允许客户端应用程序缓冲区被报告为持续时间的大小。|
|[KSPROPERTY_AUDIO_CHANNEL_CONFIG](ksproperty-audio-channel-config.md)|KSPROPERTY_AUDIO_CHANNEL_CONFIG 属性节点输出音频流中指定通道的实际空间的位置。|
|[KSPROPERTY_AUDIO_CHORUS_LEVEL](ksproperty-audio-chorus-level.md)|KSPROPERTY_AUDIO_CHORUS_LEVEL 属性指定合唱团级别。 这是合唱团节点的属性 ([KSNODETYPE_CHORUS](ksnodetype-chorus.md))。|
|[KSPROPERTY_AUDIO_CHORUS_MODULATION_DEPTH](ksproperty-audio-chorus-modulation-depth.md)|KSPROPERTY_AUDIO_CHORUS_MODULATION_DEPTH 属性指定合唱团调制深度。 这是合唱团节点的属性 ([KSNODETYPE_CHORUS](ksnodetype-chorus.md))。|
|[KSPROPERTY_AUDIO_CHORUS_MODULATION_RATE](ksproperty-audio-chorus-modulation-rate.md)|KSPROPERTY_AUDIO_CHORUS_MODULATION_RATE 属性指定合唱团调制速率。 这是合唱团节点的属性 ([KSNODETYPE_CHORUS](ksnodetype-chorus.md))。|
|[KSPROPERTY_AUDIO_COPY_PROTECTION](ksproperty-audio-copy-protection.md)|KSPROPERTY_AUDIO_COPY_PROTECTION 属性指定的音频流的复制保护状态。|
|[KSPROPERTY_AUDIO_CPU_RESOURCES](ksproperty-audio-cpu-resources.md)|KSPROPERTY_AUDIO_CPU_RESOURCES 属性指定是否在硬件中实现节点的功能，或在主机 CPU 运行的软件中模拟。|
|[KSPROPERTY_AUDIO_DELAY](ksproperty-audio-delay.md)|KSPROPERTY_AUDIO_DELAY 属性指示滞后时间的延迟节点 ([KSNODETYPE_DELAY](ksnodetype-delay.md)) 引入到指定的通道。|
|[KSPROPERTY_AUDIO_DEMUX_DEST](ksproperty-audio-demux-dest.md)|KSPROPERTY_AUDIO_DEMUX_DEST 属性指定信号分离器将其输入的流定向到的目标流。 这是多路分解器节点的属性 ([KSNODETYPE_DEMUX](ksnodetype-demux.md))。|
|[KSPROPERTY_AUDIO_DEV_SPECIFIC](ksproperty-audio-dev-specific.md)|KSPROPERTY_AUDIO_DEV_SPECIFIC 属性用于访问特定于设备的节点中的特定于设备的属性 ([KSNODETYPE_DEV_SPECIFIC](ksnodetype-dev-specific.md))。|
|[KSPROPERTY_AUDIO_DYNAMIC_RANGE](ksproperty-audio-dynamic-range.md)|KSPROPERTY_AUDIO_DYNAMIC_RANGE 属性指定是从响度节点的输出音频流的动态范围 ([KSNODETYPE_LOUDNESS](ksnodetype-loudness.md))。|
|[KSPROPERTY_AUDIO_DYNAMIC_SAMPLING_RATE](ksproperty-audio-dynamic-sampling-rate.md)|KSPROPERTY_AUDIO_DYNAMIC_SAMPLING_RATE 属性用于启用和禁用动态跟踪的节点的采样率。|
|[KSPROPERTY_AUDIO_EQ_BANDS](ksproperty-audio-eq-bands.md)|KSPROPERTY_AUDIO_EQ_BANDS 属性指定频率均衡表中的带区的集。 这是通道 EQ 节点中的一个只读属性 ([KSNODETYPE_EQUALIZER](ksnodetype-equalizer.md))。|
|[KSPROPERTY_AUDIO_EQ_LEVEL](ksproperty-audio-eq-level.md)|KSPROPERTY_AUDIO_EQ_LEVEL 属性指定包含 n 频率带区的条目的均衡表的均衡级别。 这是 EQ 节点中的通道的属性 ([KSNODETYPE_EQUALIZER](ksnodetype-equalizer.md))。|
|[KSPROPERTY_AUDIO_FILTER_STATE](ksproperty-audio-filter-state.md)|KSPROPERTY_AUDIO_FILTER_STATE 属性用于查询 GFX 筛选器，它支持的属性集的列表。 中的属性集 Guid 数组的形式检索列表。|
|[KSPROPERTY_AUDIO_LATENCY](ksproperty-audio-latency.md)|KSPROPERTY_AUDIO_LATENCY 属性用于报告的延迟 （或音频缓冲量） 与流相关联。|
|[KSPROPERTY_AUDIO_LINEAR_BUFFER_POSITION](ksproperty-audio-linear-buffer-position.md)|KSPROPERTY_AUDIO_LINEAR_BUFFER_POSITION 属性请求检索一个数字，表示从音频缓冲区，DMA 具有提取自流开始后的字节数。|
|[KSPROPERTY_AUDIO_LOUDNESS](ksproperty-audio-loudness.md)|KSPROPERTY_AUDIO_LOUDNESS 属性指定是启用还是禁用响度节点中为通道响度 （总体动态范围和低音增强） ([KSNODETYPE_LOUDNESS](ksnodetype-loudness.md))。|
|[KSPROPERTY_AUDIO_MANUFACTURE_GUID](ksproperty-audio-manufacture-guid.md)|此参数名称保留供将来使用。|
|[KSPROPERTY_AUDIO_MIC_ARRAY_GEOMETRY](ksproperty-audio-mic-array-geometry.md)|KSPROPERTY_AUDIO_MIC_ARRAY_GEOMETRY 属性指定几何图形的麦克风阵列。|
|[KSPROPERTY_AUDIO_MIC_SENSITIVITY](ksproperty-audio-mic-sensitivity.md)|KSPROPERTY_AUDIO_MIC_SENSITIVITY 属性指定相对于完整扩展 (dBFS) 单元分贝麦克风敏感度。|
|[KSPROPERTY_AUDIO_MIC_SNR](ksproperty-audio-mic-snr.md)|KSPROPERTY_AUDIO_MIC_SNR 属性指定数据库单位中的麦克风信号分配到干扰比率 (SNR) 度量值。|
|[KSPROPERTY_AUDIO_MID](ksproperty-audio-mid.md)|KSPROPERTY_AUDIO_MID 属性音节点中指定的通道的中间频率级别 ([KSNODETYPE_TONE](ksnodetype-tone.md))。|
|[KSPROPERTY_AUDIO_MIX_LEVEL_CAPS](ksproperty-audio-mix-level-caps.md)|KSPROPERTY_AUDIO_MIX_LEVEL_CAPS 属性指定 supermixer 节点的混合级别功能 ([KSNODETYPE_SUPERMIX](ksnodetype-supermix.md))。 单个的 get 属性请求检索的所有组合的输入和输出通道的信息。|
|[KSPROPERTY_AUDIO_MIX_LEVEL_TABLE](ksproperty-audio-mix-level-table.md)|KSPROPERTY_AUDIO_MIX_LEVEL_TABLE 属性指定 supermixer 节点的混合级别 ([KSNODETYPE_SUPERMIX](ksnodetype-supermix.md))。 它提供所有输入和输出通道的信息。|
|[KSPROPERTY_AUDIO_MUTE](ksproperty-audio-mute.md)|KSPROPERTY_AUDIO_MUTE 属性指定是否在静音节点上的通道 ([KSNODETYPE_MUTE](ksnodetype-mute.md)) 或不处于静音状态。|
|[KSPROPERTY_AUDIO_MUX_SOURCE](ksproperty-audio-mux-source.md)|KSPROPERTY_AUDIO_MUX_SOURCE 属性指定的输出流的多路复用器的源。 这是 MUX 节点的属性 ([KSNODETYPE_MUX](ksnodetype-mux.md))。|
|[KSPROPERTY_AUDIO_NUM_EQ_BANDS](ksproperty-audio-num-eq-bands.md)|KSPROPERTY_AUDIO_NUM_EQ_BANDS 属性用于检索频率均衡表中的带区的数目。 这是通道 EQ 节点中的一个只读属性 ([KSNODETYPE_EQUALIZER](ksnodetype-equalizer.md))。|
|[KSPROPERTY_AUDIO_PEAKMETER](ksproperty-audio-peakmeter.md)|KSPROPERTY_AUDIO_PEAKMETER 属性检索 peakmeter 节点处出现的最大的音频信号级别 ([KSNODETYPE_PEAKMETER](ksnodetype-peakmeter.md)) 自上次 peakmeter 节点已重置。|
|[KSPROPERTY_AUDIO_PEAKMETER2](ksproperty-audio-peakmeter2.md)|Windows 8 引入了报告自上次复位 peakmeter 节点 peakmeter 节点 (KSNODETYPE_PEAKMETER) 处出现的最大的音频信号级别的 KSPROPERTY_AUDIO_PEAKMETER2 属性。|
|[KSPROPERTY_AUDIO_POSITION](ksproperty-audio-position.md)|KSPROPERTY_AUDIO_POSITION 属性指定 pin 的音频流的声音缓冲区中的播放和写入游标的当前位置。|
|[KSPROPERTY_AUDIO_POSITIONEX](ksproperty-audio-positionex.md)|KSPROPERTY_AUDIO_POSITIONEX 属性提供的流位置和流式处理 (KS) 内核的关联的时间戳信息的调用方-基于音频驱动程序。|
|[KSPROPERTY_AUDIO_PREFERRED_STATUS](ksproperty-audio-preferred-status.md)|KSPROPERTY_AUDIO_PREFERRED_STATUS 属性通知设备它是系统的首选音频设备。|
|[KSPROPERTY_AUDIO_PRESENTATION_POSITION](ksproperty-audio-presentation-position.md)|KSPROPERTY_AUDIO_PRESENTATION_POSITION 属性请求检索结构，它指定要呈现到终结点的音频数据中的当前位置。|
|[KSPROPERTY_AUDIO_PRODUCT_GUID](ksproperty-audio-product-guid.md)|此参数名称保留供将来使用。|
|[KSPROPERTY_AUDIO_QUALITY](ksproperty-audio-quality.md)|KSPROPERTY_AUDIO_QUALITY 属性指定节点的输出流的质量的级别。 这是 SRC 节点的属性 ([KSNODETYPE_SRC](ksnodetype-src.md))。|
|[KSPROPERTY_AUDIO_REVERB_LEVEL](ksproperty-audio-reverb-level.md)|KSPROPERTY_AUDIO_REVERB_LEVEL 属性指定当前混响级别。 这是混响节点的属性 ([KSNODETYPE_REVERB](ksnodetype-reverb.md))。|
|[KSPROPERTY_AUDIO_REVERB_TIME](ksproperty-audio-reverb-time.md)|KSPROPERTY_AUDIO_REVERB_TIME 属性指定混响时间。 这是混响节点的属性 ([KSNODETYPE_REVERB](ksnodetype-reverb.md))。|
|[KSPROPERTY_AUDIO_SAMPLING_RATE](ksproperty-audio-sampling-rate.md)|KSPROPERTY_AUDIO_SAMPLING_RATE 属性指定一个节点以便生成的输出流示例其输入的流的速率。|
|[KSPROPERTY_AUDIO_STEREO_ENHANCE](ksproperty-audio-stereo-enhance.md)|此参数名称保留供将来使用。|
|[KSPROPERTY_AUDIO_STEREO_SPEAKER_GEOMETRY](ksproperty-audio-stereo-speaker-geometry.md)|结合使用 KSPROPERTY_AUDIO_STEREO_SPEAKER_GEOMETRY 属性[KSPROPERTY_AUDIO_CHANNEL_CONFIG](ksproperty-audio-channel-config.md)以实现硬件加速的 3D 音频 DirectSound 扬声器配置属性。 此为可选属性的 DAC 的节点 ([KSNODETYPE_DAC](ksnodetype-dac.md)) 和三维节点 ([KSNODETYPE_3D_EFFECTS](ksnodetype-3d-effects.md))。|
|[KSPROPERTY_AUDIO_SURROUND_ENCODE](ksproperty-audio-surround-encode.md)|KSPROPERTY_AUDIO_SURROUND_ENCODE 属性指定是启用还是禁用筛选器的外侧代码编码器。 外侧代码编码器节点 ([KSNODETYPE_PROLOGIC_ENCODER](ksnodetype-prologic-encoder.md)) 执行 Dolby 环绕 Pro 逻辑的编码。|
|[KSPROPERTY_AUDIO_TREBLE](ksproperty-audio-treble.md)|KSPROPERTY_AUDIO_TREBLE 属性音节点中指定一个通道的高音级别 ([KSNODETYPE_TONE](ksnodetype-tone.md))。|
|[KSPROPERTY_AUDIO_VOLUMELEVEL](ksproperty-audio-volumelevel.md)|KSPROPERTY_AUDIO_VOLUMELEVEL 属性卷节点中指定的通道的卷级别 ([KSNODETYPE_VOLUME](ksnodetype-volume.md))。|
|[KSPROPERTY_AUDIO_VOLUMELIMIT_ENGAGED](ksproperty-audio-volumelimit-engaged.md)|KSPROPERTY_AUDIO_VOLUMELIMIT_ENGAGED，是新 KS 属性已添加到 Windows 8.1 中设置的 KSPROPSETID_Audio 属性。|
|[KSPROPERTY_AUDIO_WAVERT_CURRENT_WRITE_POSITION](ksproperty-audio-wavert-current-write-position.md)|KSPROPERTY_AUDIO_WAVERT_CURRENT_WRITE_POSITION 属性请求指定当前以字节为单位写入 WaveRT 缓冲区的位置。 卸载驱动程序可以使用此写位置信息以了解有效的数据量是 WaveRT 缓冲区中。|
|[KSPROPERTY_AUDIO_WAVERT_CURRENT_WRITE_LASTBUFFER_POSITION](ksproperty-audio-wavert-current-write-lastbuffer-position.md)|KSPROPERTY_AUDIO_WAVERT_CURRENT_WRITE_LASTBUFFER_POSITION 属性用于指示音频缓冲区中的最后一个有效字节。|
|[KSPROPERTY_AUDIO_WIDE_MODE](ksproperty-audio-wide-mode.md)|此参数名称保留供将来使用。|
|[KSPROPERTY_AUDIO_WIDENESS](ksproperty-audio-wideness.md)|KSPROPERTY_AUDIO_WIDENESS 属性指定的立体声图像的宽度 （明显宽度）。|
|[KSPROPERTY_AUDIOENGINE](ksproperty-audioengine.md)|中包含的属性[KSPROPSETID_AudioEngine](kspropsetid-audioengine.md)属性集由此枚举定义，并且必须受[KSNODETYPE_AUDIO_ENGINE](ksnodetype-audio-engine.md)节点。|
|[KSPROPERTY_AUDIOENGINE_BUFFER_SIZE_RANGE](ksproperty-audioengine-buffer-size-limits.md)|[KSPROPERTY_AUDIOENGINE_BUFFER_SIZE_RANGE](ksproperty-audioengine-buffer-size-limits.md)属性指示该硬件音频引擎可以支持为给定的数据格式，在调用时的实例上的缓冲区的最小值和最大大小。 以字节为单位指定缓冲区大小。|
|[KSPROPERTY_AUDIOENGINE_DESCRIPTOR](ksproperty-audioengine-descriptor.md)|卸载支持的硬件解决方案的音频驱动程序使用[KSPROPERTY_AUDIOENGINE_DESCRIPTOR](ksproperty-audioengine-descriptor.md)提供表示硬件音频引擎的节点信息。|
|[KSPROPERTY_AUDIOENGINE_DEVICEFORMAT](ksproperty-audioengine-deviceformat.md)|[KSPROPERTY_AUDIOENGINE_DEVICEFORMAT](ksproperty-audioengine-deviceformat.md)属性请求检索或更改音频引擎节点，其设备格式设置有关的状态。|
|[KSPROPERTY_AUDIOENGINE_GFXENABLE](ksproperty-audioengine-gfx-enable.md)|[KSPROPERTY_AUDIOENGINE_GFXENABLE](ksproperty-audioengine-gfx-enable.md)属性请求将允许音频驱动程序检索或更改音频引擎节点，其处理能力的全局影响有关的状态。|
|[KSPROPERTY_AUDIOENGINE_LFXENABLE](ksproperty-audioengine-lfx-enable.md)|[KSPROPERTY_AUDIOENGINE_LFXENABLE](ksproperty-audioengine-lfx-enable.md)属性请求检索或更改音频引擎节点，有关其处理能力的本地效果的状态。|
|[KSPROPERTY_AUDIOENGINE_LOOPBACK_PROTECTION](ksproperty-audioengine-loopback-protection.md)|[KSPROPERTY_AUDIOENGINE_LOOPBACK_PROTECTION](ksproperty-audioengine-loopback-protection.md)属性请求将允许音频驱动程序设置的音频引擎节点的环回保护状态。|
|[KSPROPERTY_AUDIOENGINE_MIXFORMAT](ksproperty-audioengine-mixformat.md)|[KSPROPERTY_AUDIOENGINE_MIXFORMAT](ksproperty-audioengine-mixformat.md)属性请求检索 mixer 硬件音频引擎中的设置。|
|[KSPROPERTY_AUDIOENGINE_SUPPORTEDDEVICEFORMATS](ksproperty-audioengine-supporteddeviceformats.md)|[KSPROPERTY_AUDIOENGINE_SUPPORTEDDEVICEFORMATS](ksproperty-audioengine-supporteddeviceformats.md)属性请求检索硬件音频引擎所支持的设备格式。|
|[KSPROPERTY_AUDIOENGINE_VOLUMELEVEL](ksproperty-audioengine-volumelevel.md)|[KSPROPERTY_AUDIOENGINE_VOLUMELEVEL](ksproperty-audioengine-volumelevel.md)属性给定流中指定的通道的卷级别。|
|[KSPROPERTY_AUDIOGFX_CAPTURETARGETDEVICEID](ksproperty-audiogfx-capturetargetdeviceid.md)|KSPROPERTY_AUDIOGFX_CAPTURETARGETDEVICEID 属性用于通知是捕获流的源的音频设备的即插设备 ID 的 GFX 筛选器。|
|[KSPROPERTY_AUDIOGFX_RENDERTARGETDEVICEID](ksproperty-audiogfx-rendertargetdeviceid.md)|KSPROPERTY_AUDIOGFX_RENDERTARGETDEVICEID 属性用于通知 GFX 筛选器的呈现最终音频混合的音频设备的即插设备 ID。|
|[KSPROPERTY_AUDIOMODULE](ksproperty-audiomodule.md)|KSPROPERTY_AUDIOMODULE 枚举定义常数以音频驱动程序用于通信有关合作伙伴的信息定义音频模块。|
|[KSPROPERTY_AUDIOSIGNALPROCESSING](ksproperty-audiosignalprocessing.md)|KSPROPERTY_AUDIOSIGNALPROCESSING 枚举定义一个常量，它由与此插针上的音频处理模式相关的音频驱动程序。|
|[KSPROPERTY_AUDIOSIGNALPROCESSING_MODES](ksproperty-audiosignalprocessing-modes.md)|KSPROPERTY_AUDIOSIGNALPROCESSING_MODES 属性返回 pin 工厂所支持的音频信号处理模式的列表。|
|[KSPROPERTY_DIRECTSOUND3DBUFFER_ALL](ksproperty-directsound3dbuffer-all.md)|KSPROPERTY_DIRECTSOUND3DBUFFER_ALL 属性用于获取或设置为指定缓冲区 DirectSound 3D 缓冲区的所有属性。|
|[KSPROPERTY_DIRECTSOUND3DBUFFER_CONEANGLES](ksproperty-directsound3dbuffer-coneangles.md)|KSPROPERTY_DIRECTSOUND3DBUFFER_CONEANGLES 属性指定的内部和外部锥角 3D 声音缓冲区的声音投影圆锥。|
|[KSPROPERTY_DIRECTSOUND3DBUFFER_CONEORIENTATION](ksproperty-directsound3dbuffer-coneorientation.md)|KSPROPERTY_DIRECTSOUND3DBUFFER_CONEORIENTATION 属性指定的三维声音缓冲区声音投影圆锥体的方向。|
|[KSPROPERTY_DIRECTSOUND3DBUFFER_CONEOUTSIDEVOLUME](ksproperty-directsound3dbuffer-coneoutsidevolume.md)|KSPROPERTY_DIRECTSOUND3DBUFFER_CONEOUTSIDEVOLUME 属性指定的三维声音缓冲区圆锥体外部音量。|
|[KSPROPERTY_DIRECTSOUND3DBUFFER_MAXDISTANCE](ksproperty-directsound3dbuffer-maxdistance.md)|KSPROPERTY_DIRECTSOUND3DBUFFER_MAXDISTANCE 属性指定的三维声音缓冲区的最大距离。|
|[KSPROPERTY_DIRECTSOUND3DBUFFER_MINDISTANCE](ksproperty-directsound3dbuffer-mindistance.md)|KSPROPERTY_DIRECTSOUND3DBUFFER_MINDISTANCE 属性指定的三维声音缓冲区的最小距离。|
|[KSPROPERTY_DIRECTSOUND3DBUFFER_MODE](ksproperty-directsound3dbuffer-mode.md)|KSPROPERTY_DIRECTSOUND3DBUFFER_MODE 属性指定的三维声音缓冲区的处理模式。|
|[KSPROPERTY_DIRECTSOUND3DBUFFER_POSITION](ksproperty-directsound3dbuffer-position.md)|KSPROPERTY_DIRECTSOUND3DBUFFER_POSITION 属性指定的三维声音缓冲区的位置。|
|[KSPROPERTY_DIRECTSOUND3DBUFFER_VELOCITY](ksproperty-directsound3dbuffer-velocity.md)|KSPROPERTY_DIRECTSOUND3DBUFFER_VELOCITY 属性指定的三维声音缓冲区的速度。|
|[KSPROPERTY_DIRECTSOUND3DLISTENER_ALL](ksproperty-directsound3dlistener-all.md)|KSPROPERTY_DIRECTSOUND3DLISTENER_ALL 属性用于设置或获取指定的侦听器 ID DirectSound 3D 侦听器的所有属性|
|[KSPROPERTY_DIRECTSOUND3DLISTENER_ALLOCATION](ksproperty-directsound3dlistener-allocation.md)|KSPROPERTY_DIRECTSOUND3DLISTENER_ALLOCATION 属性用于告知驱动程序时分配和释放其侦听程序数据存储。 分配存储时创建，并且当删除侦听器时，释放侦听器。 此属性还可以用于查询驱动程序是否侦听程序的数据当前分配。|
|[KSPROPERTY_DIRECTSOUND3DLISTENER_BATCH](ksproperty-directsound3dlistener-batch.md)|KSPROPERTY_DIRECTSOUND3DLISTENER_BATCH 属性指定的批处理模式下设置为三维侦听器。|
|[KSPROPERTY_DIRECTSOUND3DLISTENER_DISTANCEFACTOR](ksproperty-directsound3dlistener-distancefactor.md)|KSPROPERTY_DIRECTSOUND3DLISTENER_DISTANCEFACTOR 属性指定应应用于任何距离值的距离因素。|
|[KSPROPERTY_DIRECTSOUND3DLISTENER_DOPPLERFACTOR](ksproperty-directsound3dlistener-dopplerfactor.md)|KSPROPERTY_DIRECTSOUND3DLISTENER_DOPPLERFACTOR 属性指定三维侦听器 Doppler 身份。|
|[KSPROPERTY_DIRECTSOUND3DLISTENER_ORIENTATION](ksproperty-directsound3dlistener-orientation.md)|KSPROPERTY_DIRECTSOUND3DLISTENER_ORIENTATION 属性指定的三维侦听器的方向。|
|[KSPROPERTY_DIRECTSOUND3DLISTENER_POSITION](ksproperty-directsound3dlistener-position.md)|KSPROPERTY_DIRECTSOUND3DLISTENER_POSITION 属性指定的三维侦听器的位置。|
|[KSPROPERTY_DIRECTSOUND3DLISTENER_ROLLOFFFACTOR](ksproperty-directsound3dlistener-rollofffactor.md)|KSPROPERTY_DIRECTSOUND3DLISTENER_ROLLOFFFACTOR 属性指定三维侦听器卷绕身份。|
|[KSPROPERTY_DIRECTSOUND3DLISTENER_VELOCITY](ksproperty-directsound3dlistener-velocity.md)|KSPROPERTY_DIRECTSOUND3DLISTENER_VELOCITY 属性指定三维侦听器速度的向量。|
|[KSPROPERTY_FMRX_ANTENNAENDPOINTID](ksproperty-fmrx-antennaendpointid.md)|[KSTOPOLOGY_ENDPOINTID](https://msdn.microsoft.com/library/windows/hardware/mt169886)属性包含有关要用作调频广播天线的终结点的信息。|
|[KSPROPERTY_FMRX_ENDPOINTID](ksproperty-fmrx-endpointid.md)|[KSTOPOLOGY_ENDPOINTID](https://msdn.microsoft.com/library/windows/hardware/mt169886)属性包含 FM 单选输出/呈现终结点的终结点 ID。|
|[KSPROPERTY_FMRX_VOLUME](ksproperty-fmrx-volume.md)|[KSPROPERTY_FMRX_VOLUME](ksproperty-fmrx-volume.md)属性控制调频广播的卷。|
|[KSPROPERTY_HRTF3D_FILTER_FORMAT](ksproperty-hrtf3d-filter-format.md)|KSPROPERTY_HRTF3D_FILTER_FORMAT 属性检索 HRTF 算法所用的筛选器格式。|
|[KSPROPERTY_HRTF3D_INITIALIZE](ksproperty-hrtf3d-initialize.md)|KSPROPERTY_HRTF3D_INITIALIZE 属性指定要用于初始化 HRTF 算法的参数值。|
|[KSPROPERTY_HRTF3D_PARAMS](ksproperty-hrtf3d-params.md)|KSPROPERTY_HRTF3D_PARAMS 属性适用于 HRTF 算法的一组三维参数值。|
|[KSPROPERTY_ITD3D_PARAMS](ksproperty-itd3d-params.md)|KSPROPERTY_ITD3D_PARAMS 属性用于设置一个三维节点 ITD 算法所用的参数。|
|[KSPROPERTY_JACK](ksproperty-jack.md)|KSPROPERTY_JACK 枚举定义新属性的音频插孔结构使用的 Id。|
|[KSPROPERTY_JACK_CONTAINERID](ksproperty-jack-containerid.md)|KSPROPERTY_JACK_CONTAINERID 属性实现为一个 pin-wise 属性，可通过使用筛选器句柄。|
|[KSPROPERTY_JACK_DESCRIPTION](ksproperty-jack-description.md)|为筛选器句柄可通过访问的多项、 pin-wise 属性实现 KSPROPERTY_JACK_DESCRIPTION 属性。|
|[KSPROPERTY_JACK_DESCRIPTION2](ksproperty-jack-description2.md)|KSPROPERTY_JACK_DESCRIPTION2 属性实现为一个 pin-wise 属性，可通过使用筛选器句柄。|
|[KSPROPERTY_JACK_SINK_INFO](ksproperty-jack-sink-info.md)|KSPROPERTY_JACK_SINK_INFO 属性实现为一个 pin-wise 属性，可通过使用筛选器句柄。|
|[KSPROPERTY_ONESHOT_DISCONNECT](ksproperty-oneshot-disconnect.md)|KSPROPERTY_ONESHOT_DISCONNECT 属性用于提示音频驱动程序以断开与蓝牙音频设备的连接。|
|[KSPROPERTY_ONESHOT_RECONNECT](ksproperty-oneshot-reconnect.md)|KSPROPERTY_ONESHOT_RECONNECT 属性用于提示要尝试连接到 Bluetooth 音频设备的音频驱动程序。|
|[KSPROPERTY_RTAUDIO_BUFFER](ksproperty-rtaudio-buffer.md)|KSPROPERTY_RTAUDIO_BUFFER 属性指定驱动程序分配的音频数据的循环缓冲区。|
|[KSPROPERTY_RTAUDIO_BUFFER_WITH_NOTIFICATION](ksproperty-rtaudio-buffer-with-notification.md)|KSPROPERTY_RTAUDIO_BUFFER_WITH_NOTIFICATION 属性指定驱动程序分配的音频数据的循环缓冲区，并标识事件通知要求。|
|[KSPROPERTY_RTAUDIO_CLOCKREGISTER](ksproperty-rtaudio-clockregister.md)|KSPROPERTY_RTAUDIO_CLOCKREGISTER 属性会映射到客户端可以访问的虚拟内存位置的音频设备的墙时钟寄存器。|
|[KSPROPERTY_RTAUDIO_GETREADPACKET](ksproperty-rtaudio-getreadpacket.md)|KSPROPERTY_RTAUDIO_GETREADPACKET 返回有关捕获音频的数据包的信息。|
|[KSPROPERTY_RTAUDIO_HWLATENCY](ksproperty-rtaudio-hwlatency.md)|KSPROPERTY_RTAUDIO_HWLATENCY 属性检索的音频硬件和其关联的数据路径的流延迟的说明。|
|[KSPROPERTY_RTAUDIO_PACKETCOUNT](ksproperty-rtaudio-packetcount.md)|KSPROPERTY_RTAUDIO_PACKETCOUNT 返回完全从 WaveRT 缓冲区传输到硬件的数据包 （从 1 开始） 计数。|
|[KSPROPERTY_RTAUDIO_POSITIONREGISTER](ksproperty-rtaudio-positionregister.md)|KSPROPERTY_RTAUDIO_POSITIONREGISTER 属性映射到客户端可以访问的虚拟内存位置的特定流的音频设备的位置寄存器。|
|[KSPROPERTY_RTAUDIO_PRESENTATION_POSITION](ksproperty-rtaudio-presentation-position.md)|KSPROPERTY_RTAUDIO_PRESENTATION_POSITION 返回流样式表信息。|
|[KSPROPERTY_RTAUDIO_QUERY_NOTIFICATION_SUPPORT](ksproperty-rtaudio-query-notification-support.md)|客户端应用程序使用 KSPROPERTY_RTAUDIO_QUERY_NOTIFICATION_SUPPORT 属性来确定是否音频驱动程序可以通知客户端应用程序时提交的缓冲区执行的进程已完成。|
|[KSPROPERTY_RTAUDIO_REGISTER_NOTIFICATION_EVENT](ksproperty-rtaudio-register-notification-event.md)|KSPROPERTY_RTAUDIO_REGISTER_NOTIFICATION_EVENT 属性注册 DMA 驱动事件通知的用户模式事件。 必须在成功调用注册的事件[KSPROPERTY_RTAUDIO_BUFFER_WITH_NOTIFICATION](ksproperty-rtaudio-buffer-with-notification.md)。|
|[KSPROPERTY_RTAUDIO_SETWRITEPACKET](ksproperty-rtaudio-setwritepacket.md)|KSPROPERTY_RTAUDIO_SETWRITEPACKET 告知 OS 已向 WaveRT 缓冲区写入有效的数据驱动程序。|
|[KSPROPERTY_RTAUDIO_UNREGISTER_NOTIFICATION_EVENT](ksproperty-rtaudio-unregister-notification-event.md)|KSPROPERTY_RTAUDIO_UNREGISTER_NOTIFICATION_EVENT 属性注销 DMA 驱动事件通知中的用户模式事件。|
|[KSPROPERTY_SOUNDDETECTOR](ksproperty-sounddetector.md)|[KSPROPERTY_SOUNDDETECTOR](ksproperty-sounddetector.md)枚举定义一些常量，用于注册还支持检测程序的音频捕获设备的筛选器。|
|[KSPROPERTY_SOUNDDETECTOR_ARMED](ksproperty-sounddetector-armed.md)|[KSPROPERTY_SOUNDDETECTOR_ARMED](ksproperty-sounddetector-armed.md)属性是检测程序的当前 arming 状态。|
|[KSPROPERTY_SOUNDDETECTOR_MATCHRESULT](ksproperty-sounddetector-matchresult.md)|KSPROPERTY_SOUNDDETECTOR_MATCHRESULT 属性包含匹配项的结果数据。|
|[KSPROPERTY_SOUNDDETECTOR_PATTERNS](ksproperty-sounddetector-patterns.md)|[KSPROPERTY_SOUNDDETECTOR_PATTERNS](ksproperty-sounddetector-patterns.md)操作系统设置属性来配置要检测到的关键字。|
|[KSPROPERTY_SOUNDDETECTOR_SUPPORTEDPATTERNS](ksproperty-sounddetector-supportedpatterns.md)|[KSPROPERTY_SOUNDDETECTOR_SUPPORTEDPATTERNS](ksproperty-sounddetector-supportedpatterns.md)属性用于获取标识的受支持的模式的类型的 Guid 的列表。|
|[KSPROPERTY_SYSAUDIO_ATTACH_VIRTUAL_SOURCE](ksproperty-sysaudio-attach-virtual-source.md)|KSPROPERTY_SYSAUDIO_ATTACH_VIRTUAL_SOURCE 属性将一个虚拟源附加到虚拟的音频设备上的 pin 实例。|
|[KSPROPERTY_SYSAUDIO_COMPONENT_ID](ksproperty-sysaudio-component-id.md)|KSPROPERTY_SYSAUDIO_COMPONENT_ID 属性从指定的虚拟音频设备使用的波次呈现设备中检索组件 ID。|
|[KSPROPERTY_SYSAUDIO_CREATE_VIRTUAL_SOURCE](ksproperty-sysaudio-create-virtual-source.md)|KSPROPERTY_SYSAUDIO_CREATE_VIRTUAL_SOURCE 属性创建一个新的虚拟源。|
|[KSPROPERTY_SYSAUDIO_DEVICE_COUNT](ksproperty-sysaudio-device-count.md)|KSPROPERTY_SYSAUDIO_DEVICE_COUNT 属性检索指定的虚拟 DirectSound 应用程序具有可供选择的音频设备的数量计数。|
|[KSPROPERTY_SYSAUDIO_DEVICE_FRIENDLY_NAME](ksproperty-sysaudio-device-friendly-name.md)|KSPROPERTY_SYSAUDIO_DEVICE_FRIENDLY_NAME 属性检索包含虚拟的音频设备的友好名称的 Unicode 字符串。|
|[KSPROPERTY_SYSAUDIO_DEVICE_INSTANCE](ksproperty-sysaudio-device-instance.md)|KSPROPERTY_SYSAUDIO_DEVICE_INSTANCE 属性指定虚拟的音频设备的当前实例。|
|[KSPROPERTY_SYSAUDIO_DEVICE_INTERFACE_NAME](ksproperty-sysaudio-device-interface-name.md)|KSPROPERTY_SYSAUDIO_DEVICE_INTERFACE_NAME 属性检索包含指定的虚拟音频设备的即插设备接口名称的 Unicode 字符串。|
|[KSPROPERTY_SYSAUDIO_INSTANCE_INFO](ksproperty-sysaudio-instance-info.md)|KSPROPERTY_SYSAUDIO_INSTANCE_INFO 属性打开虚拟的音频设备，并且指定该设备的配置标志。|
|[KSPROPERTY_SYSAUDIO_SELECT_GRAPH](ksproperty-sysaudio-select-graph.md)|KSPROPERTY_SYSAUDIO_SELECT_GRAPH 属性用于显式 SysAudio pin 实例为生成虚拟的音频设备的关系图中包括的可选节点。|
|[KSPROPERTY_TELEPHONY_CALLCONTROL](ksproperty-telephony-callcontrol.md)|KSPROPERTY_TELEPHONY_CALLCONTROL 属性用于启动和终止电话呼叫。|
|[KSPROPERTY_TELEPHONY_CALLHOLD](ksproperty-telephony-callhold.md)|[KSPROPERTY_TELEPHONY_CALLHOLD](ksproperty-telephony-callhold.md)属性用于控制电话呼叫的保留状态。|
|[KSPROPERTY_TELEPHONY_CALLINFO](ksproperty-telephony-callinfo.md)|[KSPROPERTY_TELEPHONY_CALLINFO](ksproperty-telephony-callinfo.md)属性用于检索当前的调用信息，例如调用状态和调用类型。|
|[KSPROPERTY_TELEPHONY_ENDPOINTIDPAIR](ksproperty-telephony-endpointidpair.md)|[KSPROPERTY_TELEPHONY_ENDPOINTIDPAIR](ksproperty-telephony-endpointidpair.md)属性包含用于移动电话音频路由的呈现和捕获终结点。|
|[KSPROPERTY_TELEPHONY_MUTE_TX](ksproperty-telephony-mute-tx.md)|[KSPROPERTY_TELEPHONY_MUTE_TX](ksproperty-telephony-mute-tx.md)属性用于控制是否将数据从本地麦克风发送到远程端调节到静音。|
|[KSPROPERTY_TELEPHONY_PROVIDERCHANGE](ksproperty-telephony-providerchange.md)|[KSPROPERTY_TELEPHONY_PROVIDERCHANGE](ksproperty-telephony-providerchange.md)属性用于单个单选语音呼叫连续性 (SRVCC) 开始或结束与音频驱动程序进行通信。|
|[KSPROPERTY_TELEPHONY_PROVIDERID](ksproperty-telephony-providerid.md)|[KSPROPERTY_TELEPHONY_PROVIDERID](ksproperty-telephony-providerid.md)音频驱动程序使用属性来将批筛选器提供程序标识符相关联。|
|[KSPROPERTY_TELEPHONY_VOLUME](ksproperty-telephony-volume.md)|[KSPROPERTY_TELEPHONY_VOLUME](ksproperty-telephony-volume.md)属性用于控制移动电话的所有调用的卷。|
|[KSPROPERTY_TOPOLOGYNODE_ENABLE](ksproperty-topologynode-enable.md)|KSPROPERTY_TOPOLOGYNODE_ENABLE 属性用于启用或禁用的已生成的拓扑中的拓扑节点。|
|[KSPROPERTY_TOPOLOGYNODE_RESET](ksproperty-topologynode-reset.md)|KSPROPERTY_TOPOLOGYNODE_RESET 属性重置节点完全，将其还原到其初始状态。|
|[KSRTAUDIO_BUFFER_PROPERTY](ksrtaudio-buffer-property.md)|KSRTAUDIO_BUFFER_PROPERTY 结构追加缓冲区基址和到请求的缓冲区大小[KSPROPERTY](https://msdn.microsoft.com/library/windows/hardware/ff564262)结构。 通过音频缓冲区的请求分配到客户端使用此结构[KSPROPERTY_RTAUDIO_BUFFER](ksproperty-rtaudio-buffer.md)。|


