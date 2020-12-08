---
title: 音频驱动程序结构
description: 音频驱动程序结构
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: c39a1bc46b76d68b4ed4c571758b8f2391954ab7
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96784997"
---
# <a name="audio-drivers-structures"></a>音频驱动程序结构

## <span id="ddk_audio_drivers_structures_ks"></span><span id="DDK_AUDIO_DRIVERS_STRUCTURES_KS"></span>

本部分介绍了 WDM 音频微型端口驱动程序使用的结构。 结构列表如下所示：

[**APO \_ REG \_ 属性**](/windows/win32/api/audioenginebaseapo/ns-audioenginebaseapo-apo_reg_properties)

[**APOInitBaseStruct**](/windows/win32/api/audioenginebaseapo/ns-audioenginebaseapo-apoinitbasestruct)

[**APOInitSystemEffects**](/windows/win32/api/audioenginebaseapo/ns-audioenginebaseapo-apoinitsystemeffects)

[**APOInitSystemEffects2**](/windows/win32/api/audioenginebaseapo/ns-audioenginebaseapo-apoinitsystemeffects2)

[**AudioFXExtensionParams**](/windows/win32/api/audioenginebaseapo/ns-audioenginebaseapo-audiofxextensionparams)

[**DMU \_ 内核 \_ 事件**](/windows-hardware/drivers/ddi/dmusicks/ns-dmusicks-_dmus_kernel_event)

[**DRMFORWARD**](/windows-hardware/drivers/ddi/drmk/ns-drmk-tagdrmforward)

[**DRMRIGHTS**](/windows-hardware/drivers/ddi/drmk/ns-drmk-tagdrmrights)

[**DS3DVECTOR**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_ds3dvector)

[**KSAC3 \_ 备用 \_ 音频**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksac3_alternate_audio)

[**KSAC3 \_ 位 \_ 流 \_ 模式**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksac3_bit_stream_mode)

[**KSAC3 \_ 对话框 \_ 级别**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksac3_dialogue_level)

[**KSAC3 \_ DOWNMIX**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksac3_downmix)

[**KSAC3 \_ 错误 \_ CONCEALMENT**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksac3_error_concealment)

[**KSAC3 \_ 语言 \_ 代码**](/previous-versions/windows/hardware/drivers/ff537081(v=vs.85))

[**KSAC3 \_ 房间 \_ 类型**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksac3_room_type)

[**KSAUDIO \_ 通道 \_ 配置**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksaudio_channel_config)

[**KSAUDIO \_ 复制 \_ 保护**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksaudio_copy_protection)

[**KSAUDIO \_ 动态 \_ 范围**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksaudio_dynamic_range)

[**KSAUDIO \_ MIC \_ 数组 \_ 几何图形**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksaudio_mic_array_geometry)

[**KSAUDIO \_ 麦克风 \_ 坐标**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksaudio_microphone_coordinates)

[**KSAUDIO \_ 混音 \_ 大写字母**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksaudio_mix_caps)

[**KSAUDIO \_ MIXCAP \_ 表**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksaudio_mixcap_table)

[**KSAUDIO \_ MIXLEVEL**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksaudio_mixlevel)

[**KSAUDIO \_ PACKETSIZE \_ 约束**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_ksaudio_packetsize_constraints)

[**KSAUDIO\_PACKETSIZE\_CONSTRAINTS2**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_ksaudio_packetsize_constraints2)

[**KSAUDIO \_ PACKETSIZE \_ PROCESSINGMODE \_ 约束**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_ksaudio_packetsize_signalprocessingmode_constraint)

[**KSAUDIO \_ 位置**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksaudio_position)

[**KSAUDIO \_ POSITIONEX**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksaudio_positionex)

[**KSAUDIO \_ 首选 \_ 状态**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksaudio_preferred_status)

[**KSAUDIO \_ 演示 \_ 位置**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksaudio_presentation_position)

[**KSAUDIOENGINE \_ 缓冲区 \_ 大小 \_ 范围**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_tagksaudioengine_buffer_size_range)

[**KSAUDIOENGINE \_ 描述符**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_tagksaudioengine_descriptor)

[**KSAUDIOENGINE \_ VOLUMELEVEL**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_tagksaudioengine_volumelevel)

[**KSDATAFORMAT \_ DSOUND**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksdataformat_dsound)

[**KSDATAFORMAT \_ WAVEFORMATEX**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksdataformat_waveformatex)

[**KSDATARANGE \_ 音频**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksdatarange_audio)

[**KSDATARANGE \_ 音乐**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksdatarange_music)

[**KSDRMAUDIOSTREAM \_ ID 为**](/windows-hardware/drivers/ddi/drmk/ns-drmk-ksdrmaudiostream_contentid)

[**KSDSOUND \_ BUFFERDESC**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksdsound_bufferdesc)

[**KSDS3D \_ BUFFER \_ ALL**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksds3d_buffer_all)

[**KSDS3D \_ 缓冲器 \_ \_ 角度**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksds3d_buffer_cone_angles)

[**KSDS3D \_ HRTF \_ FILTER \_ 格式 \_ 消息**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksds3d_hrtf_filter_format_msg)

[**KSDS3D \_ HRTF \_ INIT \_ MSG**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksds3d_hrtf_init_msg)

[**KSDS3D \_ HRTF \_ PARAMS \_ MSG**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksds3d_hrtf_params_msg)

[**KSDS3D \_ ITD \_ 参数**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksds3d_itd_params)

[**KSDS3D \_ ITD \_ 参数 \_ 消息**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksds3d_itd_params_msg)

[**\_全部 KSDS3D 侦听器 \_**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksds3d_listener_all)

[**KSDS3D \_ 侦听器 \_ 方向**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksds3d_listener_orientation)

[**KSJACK \_ 说明**](ksjack-description.md)

[**KSJACK \_ DESCRIPTION2**](ksjack-description2.md)

[**KSJACK \_ 接收器 \_ 信息**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_tagksjack_sink_information)

[**KSMUSICFORMAT**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksmusicformat)

[**KSNODEPROPERTY**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksnodeproperty)

[**KSNODEPROPERTY \_ 音频 \_ 通道**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksnodeproperty_audio_channel)

[**KSP \_ DRMAUDIOSTREAM \_ ID 为**](/windows-hardware/drivers/ddi/drmk/ns-drmk-ksp_drmaudiostream_contentid)

[**KSP \_ PINMODE**](/windows/win32/api/msapofxproxy/ns-msapofxproxy-ksp_pinmode)

[KSRTAUDIO 结构](/windows-hardware/drivers/ddi/ksmedia/index)

[**KSTELEPHONY \_ CALLCONTROL**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_tagkstelephony_callcontrol)

[**KSTELEPHONY \_ CALLINFO**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_tagkstelephony_callinfo)

[**KSTELEPHONY \_ PROVIDERCHANGE**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_tagkstelephony_providerchange)

[**KSTOPOLOGY \_ ENDPOINTID**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_tagkstopology_endpointid)

[**KSTOPOLOGY \_ ENDPOINTIDPAIR**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_tagkstopology_endpointidpair)

[**LOOPEDSTREAMING \_ 位置 \_ 事件 \_ 数据**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-loopedstreaming_position_event_data)

[**MDEVICECAPSEX**](/windows/win32/api/mmddk/ns-mmddk-mdevicecapsex)

[**MIDIOPENDESC**](/windows/win32/api/mmddk/ns-mmddk-midiopendesc)

[**RTAUDIO \_ GETREADPACKET \_ 信息**](/previous-versions/windows/hardware/drivers/mt169891(v=vs.85))

[**RTAUDIO \_ SETWRITEPACKET \_ 信息**](/previous-versions/windows/hardware/drivers/mt169892(v=vs.85))

[**SOUNDDETECTOR \_ PATTERNHEADER**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-sounddetector_patternheader)

[**合成 \_ 缓冲器**](/windows-hardware/drivers/ddi/dmusprop/ns-dmusprop-_synth_buffer)

[**合成 \_ PORTPARAMS**](/windows-hardware/drivers/ddi/dmusprop/ns-dmusprop-_synth_portparams)

[**合成 \_ 统计信息**](/windows-hardware/drivers/ddi/dmusprop/ns-dmusprop-_synth_stats)

[**SYNTHCAPS**](/windows-hardware/drivers/ddi/dmusprop/ns-dmusprop-_synthcaps)

[**SYNTHDOWNLOAD**](/windows-hardware/drivers/ddi/dmusprop/ns-dmusprop-_synthdownload)

[**SYNTHVOICEPRIORITY \_ 实例**](/windows-hardware/drivers/ddi/dmusprop/ns-dmusprop-_synthvoicepriority_instance)

[**SYSAUDIO \_ 附加 \_ 虚拟 \_ 源**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-sysaudio_attach_virtual_source)

[**SYSAUDIO \_ 创建 \_ 虚拟 \_ 源**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-sysaudio_create_virtual_source)

[**SYSAUDIO \_ 实例 \_ 信息**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-sysaudio_instance_info)

[**SYSAUDIO \_ 选择 \_ 图形**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-sysaudio_select_graph)

[**UNCOMPRESSEDAUDIOFORMAT**](/windows/win32/api/audiomediatype/ns-audiomediatype-uncompressedaudioformat)

[**WAVEFORMATEX**](/windows/win32/api/mmreg/ns-mmreg-waveformatex)

[**WAVEFORMATEXTENSIBLE**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-waveformatextensible)
