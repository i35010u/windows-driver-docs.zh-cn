---
title: 音频信号处理模式
description: 驱动程序声明每个设备支持的音频信号处理模式。
ms.assetid: 104275F8-2302-484B-B673-7448CAA1F793
ms.date: 05/14/2018
ms.localizationpriority: medium
ms.openlocfilehash: 28fffee7b4fc41648f146e752ea26da51f58780c
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72831322"
---
# <a name="audio-signal-processing-modes"></a>音频信号处理模式


驱动程序声明每个设备支持的音频信号处理模式。

## <a name="span-idavailable_signal_processing_modesspanspan-idavailable_signal_processing_modesspanspan-idavailable_signal_processing_modesspanavailable-signal-processing-modes"></a><span id="Available_Signal_Processing_Modes"></span><span id="available_signal_processing_modes"></span><span id="AVAILABLE_SIGNAL_PROCESSING_MODES"></span>可用的信号处理模式


音频类别（由应用程序选择）映射到音频模式（由驱动程序定义）。 Windows 定义了七种音频信号处理模式。 Oem 和 Ihv 可以确定要实现的模式。 建议 Ihv/Oem 利用新模式来添加音频效果，以优化音频信号以提供最佳用户体验。 下表汇总了这些模式。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><strong>模式</strong></td>
<td align="left"><strong>呈现/捕获</strong></td>
<td align="left"><strong>描述</strong></td>
</tr>
<tr class="even">
<td align="left">原始</td>
<td align="left">两者都是</td>
<td align="left"><p>Raw 模式指定不应对流应用任何信号处理。</p>
<p>应用程序可以请求完全不动并执行其自己的信号处理的原始流。</p></td>
</tr>
<tr class="odd">
<td align="left">Default</td>
<td align="left">两者都是</td>
<td align="left"><p>此模式定义默认音频处理。</p></td>
</tr>
<tr class="even">
<td align="left">部</td>
<td align="left">Render</td>
<td align="left">电影音频播放</td>
</tr>
<tr class="odd">
<td align="left">许可证</td>
<td align="left">两者都是</td>
<td align="left">音乐音频播放（大多数媒体流的默认值）</td>
</tr>
<tr class="even">
<td align="left">语速</td>
<td align="left">捕获</td>
<td align="left">人类语音捕获（例如 Cortana 的输入）</td>
</tr>
<tr class="odd">
<td align="left">联系</td>
<td align="left">两者都是</td>
<td align="left">VOIP 呈现和捕获（例如 Skype、Lync）</td>
</tr>
<tr class="even">
<td align="left">提醒</td>
<td align="left">Render</td>
<td align="left">铃声、警报、警报等。</td>
</tr>
</tbody>
</table>

 

Windows 10 中的 \* 新增。

## <a name="span-idsignal_processing_mode_driver_requirementsspanspan-idsignal_processing_mode_driver_requirementsspanspan-idsignal_processing_mode_driver_requirementsspansignal-processing-mode-driver-requirements"></a><span id="Signal_Processing_Mode_Driver_Requirements"></span><span id="signal_processing_mode_driver_requirements"></span><span id="SIGNAL_PROCESSING_MODE_DRIVER_REQUIREMENTS"></span>信号处理模式驱动程序要求


音频设备驱动程序需要至少支持*Raw*模式或*默认*模式。 支持附加模式是可选的。

可能并非所有模式都可用于特定系统。 驱动程序定义其支持的信号处理模式（即，驱动程序安装的类型为），并相应地通知操作系统。 如果驱动程序不支持某个特定模式，则 Windows 将使用下一个最佳匹配模式。

下图显示了支持多种模式的系统：

![多音频模式 ](images/audio-modes-win-10.png)

## <a name="span-idwindows_audio_stream_categoriesspanspan-idwindows_audio_stream_categoriesspanspan-idwindows_audio_stream_categoriesspanwindows-audio-stream-categories"></a><span id="Windows_Audio_Stream_Categories"></span><span id="windows_audio_stream_categories"></span><span id="WINDOWS_AUDIO_STREAM_CATEGORIES"></span>Windows 音频流类别


为了通知系统有关音频流的使用情况，应用程序可以选择使用特定的音频流类别标记流。 应用程序可以在创建音频流后使用任意音频 Api 设置音频类别。 在 Windows 10 中，有九个音频流类别。

|                |                                                                                                       |
|----------------|-------------------------------------------------------------------------------------------------------|
| **类别**   | **描述**                                                                                       |
| 电影          | 电影，带对话框的视频（替换 ForegroundOnlyMedia）                                              |
| Media          | 媒体播放的默认类别（替换 BackgroundCapableMedia）                                 |
| 游戏聊天      | 用户之间的游戏间通信（Windows 10 中的新类别）                                      |
| “语音”         | 语音输入（例如，个人助手）和输出（例如，导航应用）（Windows 10 中的新类别） |
| Communications | VOIP，实时聊天                                                                                  |
| 警报         | 警报，响铃音，通知                                                                       |
| 声音效果  | 嘟嘟声、dings 等                                                                                     |
| 游戏媒体     | 游戏音乐                                                                                         |
| 游戏效果   | 球弹跳，车载声音，项目符号，等等。                                                      |
| 其他          | 未分类的流                                                                                 |

 

如前所述，音频类别（由应用程序选择）映射到音频模式（由驱动程序定义）。 应用程序可以用10种音频类别之一标记其每个流。

应用程序不能选择更改音频类别和信号处理模式之间的映射。 应用程序不知道 "音频处理模式" 的概念。 它们找不到每个流所使用的模式。

**WASAPI 代码示例**

WASAPIAudio 示例中的以下 WASAPI 代码显示了如何设置不同的音频类别。

```cpp
// The ActivateAudioInterfaceAsync is a replacment for IMMDevice::Activate
IActivateAudioInterfaceAsyncOperation *asyncOp = nullptr;
HRESULT hr = S_OK;

String ^defaultRender = Windows::Media::Devices::MediaDevice::GetDefaultAudioRenderId( Windows::Media::Devices::AudioDeviceRole::Default );

hr = ActivateAudioInterfaceAsync( defaultRender->Data(), __uuidof( IAudioClient3 ), nullptr, this, &asyncOp );
if ( FAILED( hr ) ) { … }
…

// the app’s implementation of IActivateAudioInterfaceCompetionHandler is invoked asynchronously
HRESULT ActivateAudioInterfaceCompletionHandler::ActivateCompleted( IActivateAudioInterfaceAsyncOperation *activateOperation ) {
    HRESULT hr = S_OK;
    HRESULT hrActivateResult = S_OK;
    IUnknown *pUnknown = nullptr;
    IAudioClient3 *pAudioClient3 = nullptr;

    hr = activateOperation->GetActivateResult( &hrActivateResult, &pUnknown );
    if ( FAILED( hr ) )  { … }
    if ( FAILED( hrActivateResult ) ) { … }
    
    hr = pUnknown->QueryInterface( IID_PPV_ARGS( &pAudioClient3 ) );
    if ( FAILED( hr ) ) { … }

    // The IAudioClient3::SetClientProperties call needs to happen after activation completes, 
    // but before the call to IAudioClient3::Initialize or IAudioClient3::InitializeSharedAudioStream.
    AudioClientProperties props = {};
    props.cbSize = sizeof(props);
    props.eCategory = AudioCategory_GameEffects;
    pAudioClient3->SetClientProperties( &props );
    if ( FAILED( hr ) ) { … }

    hr = pAudioClient3->InitializeSharedAudioStream( … );
    if ( FAILED( hr ) ) { … }

    …
```

## <a name="span-idsignal_processing_modes_and_effectsspanspan-idsignal_processing_modes_and_effectsspanspan-idsignal_processing_modes_and_effectsspansignal-processing-modes-and-effects"></a><span id="Signal_Processing_Modes_and_Effects"></span><span id="signal_processing_modes_and_effects"></span><span id="SIGNAL_PROCESSING_MODES_AND_EFFECTS"></span>信号处理模式和效果


Oem 定义将用于每个模式的影响。 Windows 定义了十七种类型的音频效果的列表。

若要了解如何关联模式，请参阅[实现音频处理对象](implementing-audio-processing-objects.md)。

应用程序可以询问将应用于特定流以进行原始或非原始处理的影响。 应用程序还可以要求在效果或原始处理状态发生变化时得到通知。 应用程序可以使用此信息来确定特定的流类别（如通信）是否可用，或者是否仅使用原始模式。 如果只提供 RAW 模式，应用程序可以确定要添加多少音频处理。

如果 RawProcessingSupported 为 true，则应用程序还可以选择在某些流上设置 "使用原始" 标志 AudioDevice。 如果 RawProcessingSupported 为 false，则应用程序不能设置 "使用原始" 标志。

应用程序不能了解有多少模式，但 RAW/非原始模式除外。

无论音频硬件配置如何，应用程序都应请求最佳的音频效果处理。 例如，将流标记为通信后，Windows 会使 Windows 知道暂停背景音乐。

有关静态音频流类别的详细信息，请参阅[AudioCategory 枚举](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Media.AudioCategory)和[AudioCategory 属性](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.MediaElement#Windows_UI_Xaml_Controls_MediaElement_AudioCategory)。

## <a name="span-idclsids_for_system_effectsspanspan-idclsids_for_system_effectsspanspan-idclsids_for_system_effectsspanclsids-for-system-effects"></a><span id="CLSIDs_for_System_Effects"></span><span id="clsids_for_system_effects"></span><span id="CLSIDS_FOR_SYSTEM_EFFECTS"></span>系统效果的 Clsid


**FX\_发现\_效果\_APO\_CLSID**

这是 MsApoFxProxy "代理效果" 的 CLSID，它查询驱动程序以获取活动效果列表;

```cpp
FX_DISCOVER_EFFECTS_APO_CLSID  = "{889C03C8-ABAD-4004-BF0A-BC7BB825E166}"
```

**KSATTRIBUTEID\_AUDIOSIGNALPROCESSING\_模式**

KSATTRIBUTEID\_AUDIOSIGNALPROCESSING\_模式是内核流式处理的标识符，用于标识所引用的特定属性，即信号处理模式属性。

此处显示的 \#定义语句在 KSMedia 头文件中可用。

```cpp
#define STATIC_KSATTRIBUTEID_AUDIOSIGNALPROCESSING_MODE 0xe1f89eb5, 0x5f46, 0x419b, 0x96, 0x7b, 0xff, 0x67, 0x70, 0xb9, 0x84, 0x1
DEFINE_GUIDSTRUCT("E1F89EB5-5F46-419B-967B-FF6770B98401", KSATTRIBUTEID_AUDIOSIGNALPROCESSING_MODE);
#define KSATTRIBUTEID_AUDIOSIGNALPROCESSING_MODE DEFINE_GUIDNAMED(KSATTRIBUTEID_AUDIOSIGNALPROCESSING_MODE)
```

KSATTRIBUTEID\_AUDIOSIGNALPROCESSING\_模式用于通过包含[**KSATTRIBUTE\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksattribute_list)的[**KSDATARANGE**](https://docs.microsoft.com/previous-versions/ff561658(v=vs.85))结构的模式感知驱动程序。 此列表中的单个元素为[**KSATTRIBUTE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksattribute)。 **KSATTRIBUTE**结构的属性成员设置为 KSATTRIBUTEID\_AUDIOSIGNALPROCESSING\_模式。

## <a name="span-idaudio_effectsspanspan-idaudio_effectsspanspan-idaudio_effectsspanaudio-effects"></a><span id="Audio_Effects"></span><span id="audio_effects"></span><span id="AUDIO_EFFECTS"></span>音频效果


以下音频效果可用于 Windows 10。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left">回声取消（AEC）</td>
<td align="left"><p>在音频流中已经存在回音后，通过删除回声来改善音频质量。</p></td>
</tr>
<tr class="even">
<td align="left">干扰（NS）</td>
<td align="left"><p>当出现在音频流中时，噪声抑制（NS）会取消噪音，如 humming 和蜂鸣。</p></td>
</tr>
<tr class="odd">
<td align="left">自动增益控制（AGC）</td>
<td align="left"><p>自动增益控制（AGC）-设计为在其输出中提供受控信号波幅，而不考虑输入信号中的波幅的变化。 使用 "平均" 或 "峰值" 输出信号级别，可以将输入到输出的增益动态调整到适当的值，启用稳定级别的输出，甚至可以使用各种输入信号级别。</p></td>
</tr>
<tr class="even">
<td align="left">横梁形成（BF）</td>
<td align="left"><p>横梁形成（BF）是一种用于定向信号传输或接收的信号处理技术。 这是通过将分阶段数组中的元素组合在一起来实现的，这样一来，在特定角度发出信号会出现建设性干扰，而其他人则会遇到破坏性干扰 与全向接收/传输相比，其改进称为接收/传输增益（或丢失）。</p></td>
</tr>
<tr class="odd">
<td align="left">删除恒定音调</td>
<td align="left"><p>使用 "恒定音调删除" 衰减固定背景噪音，如胶带电流嘶嘶声、电风扇或 hums。</p></td>
</tr>
<tr class="even">
<td align="left">Equalizer</td>
<td align="left"><p>均衡器效果用于利用线性筛选器改变音频系统的频率响应。 这允许提升信号的不同部分，类似于高音或低音设置。</p></td>
</tr>
<tr class="odd">
<td align="left">响度均衡器</td>
<td align="left"><p>响度均衡器效果通过对音频输出进行调节，使更高和更高的声音比平均响度更接近，从而减少了预期的音量差异。</p></td>
</tr>
<tr class="even">
<td align="left">低音增强</td>
<td align="left"><p>在具有有限低音功能的扬声器的系统（如便携式计算机）中，有时可以通过在扬声器支持的频率范围内提升低音响应来提高音频的感知质量。 通过提高中端低音范围内的增益，低音提高了移动设备上非常小的扬声器声音。</p></td>
</tr>
<tr class="odd">
<td align="left">虚拟环绕</td>
<td align="left"><p>虚环绕使用简单数字方法将多通道信号合并为两个通道。 这是通过使用大多数新式音频接收器提供的 Pro 逻辑解码器，使转换后的信号恢复为原始多通道信号的方式。 对于具有双通道声音硬件的系统和具有环绕声增强机制的接收方，虚拟环绕是理想之选。</p></td>
</tr>
<tr class="even">
<td align="left">虚拟耳机</td>
<td align="left"><p>通过虚拟化环绕声，戴耳机的用户可将声音从正面和背面区分开来。 这是通过传输空间提示来实现的，这些提示有助于大脑本地化声音并将声音集成到声音字段。 这使得声音看起来像是超越耳机，这就是创建 "外部" 收听体验。 这种效果是通过使用一种名为头相关传输功能（HRTF）的高级技术实现的。 HRTF 生成基于人体的声音提示。 这些提示不仅有助于侦听器找到声音的方向和来源，还增强了侦听器周围声音环境的类型。</p></td>
</tr>
<tr class="odd">
<td align="left">扬声器填充</td>
<td align="left"><p>大多数音乐仅具有两个通道，因此不会针对典型音频或视频发烧的多通道音频设备进行优化。 因此，只需使用使用和 loudspeakers 的音乐，就不会获得理想的音频体验。 演讲者填充模拟多通道扬声器设置。 它允许在房间内的所有 loudspeakers 上播放仅在两个扬声器上播放的音乐，从而增强空间成名。</p></td>
</tr>
<tr class="even">
<td align="left">房间修正</td>
<td align="left"><p>房间更正通过自动计算延迟、频率响应和增益调整的最佳组合，为房间中的特定位置（例如，沙发的中心缓冲）优化倾听体验。</p>
<p>房间更正功能可以更好地匹配视频屏幕上的图像，而且在桌面扬声器置于非标准位置时也很有用。 房间更正处理是对高端接收方中类似功能的改进，因为它可以更好地用于人体耳处理声音的方式。</p>
<p>校准是使用麦克风的帮助来执行的，并且该过程可用于立体声和多通道系统。 用户将麦克风置于用户打算坐下来的麦克风，然后激活一个向导来测量房间响应。 该向导依次从每个扬声器播放一组特别设计的声音，并测量每个扬声器从麦克风位置的距离、频率响应和总体收益。</p></td>
</tr>
<tr class="odd">
<td align="left">低音管理</td>
<td align="left"><p>有两种低音管理模式：转发低音管理和反向低音管理。</p>
<p><em>正向低音 management</em>筛选出音频数据流的低频率内容。 正向低音管理算法将筛选输出重定向到低音炮，或重定向到左侧和右侧的扬声器通道，具体取决于可以处理深度低音频率的通道。 此决定基于 LRBig 标志的设置。 若要设置 LRBig 标志，用户可以使用 "控制面板" 中的 "声音小程序" 来访问 "低音管理设置" 对话框。 用户选中一个复选框以指示，例如，右前方和左左扬声器是完整范围，此操作将设置 LRBig 标志。 若要清除此标志，请单击复选框将其清除。</p>
<p><em>反向低音管理</em>将信号从低音炮通道分发到其他输出通道。 该信号将定向到所有通道，或者定向到左侧和前右通道，具体取决于 LRBig 标志的设置。 将低音炮信号混合到其他通道时，此过程将使用大幅降低。 使用的低音管理模式取决于低音炮的可用性和主要扬声器的低音处理功能。 在 Windows 中，用户通过控制面板中的 "声音" 小程序提供了此信息。</p></td>
</tr>
<tr class="even">
<td align="left">环境影响</td>
<td align="left"><p>环境影响可以更准确地模拟真实世界的音频环境，从而提高音频播放的现实。 您可以选择多种不同的环境，例如 "体育场" 模拟体育体育场的噪声。</p></td>
</tr>
<tr class="odd">
<td align="left">扬声器保护</td>
<td align="left"><p>演讲者防护的目的在于抑制 resonant 频率，这会导致扬声器对任何电脑的系统组件进行物理损坏。 例如，某些物理硬盘驱动器可能会损坏，只需以适当的频率播放声音。 其次，发言人防护可以通过在信号超过特定值时 attenuating 信号来最大程度地减少对扬声器的损害。</p></td>
</tr>
<tr class="even">
<td align="left">扬声器补偿</td>
<td align="left"><p>有些扬声器比其他扬声器更好于重现声音。 例如，某个扬声器可能衰减低于 100 Hz。 有时，音频驱动程序和固件 DSP 解决方案需要知道他们正在播放的扬声器的具体性能特征，并可以添加处理以补偿扬声器限制的处理。 例如，可以创建终结点效果（EFX），以将增益应用到低于 100 Hz 的频率。 当与物理扬声器中的衰减结合时，会产生增强的音频保真。</p></td>
</tr>
<tr class="odd">
<td align="left">动态范围压缩</td>
<td align="left"><p>动态范围压缩加大声音或 "压缩" 音频信号的动态范围。 音频压缩加大静止声音，它们低于特定的阈值，而声音却不受影响。</p></td>
</tr>
</tbody>
</table>

 

此处显示的 \#定义语句在 KSMedia 头文件中可用。

默认值

```cpp
#define STATIC_AUDIO_SIGNALPROCESSINGMODE_DEFAULT 0xc18e2f7e, 0x933d, 0x4965, 0xb7, 0xd1, 0x1e, 0xef, 0x22, 0x8d, 0x2a, 0xf3
DEFINE_GUIDSTRUCT("C18E2F7E-933D-4965-B7D1-1EEF228D2AF3", AUDIO_SIGNALPROCESSINGMODE_DEFAULT);
#define AUDIO_SIGNALPROCESSINGMODE_DEFAULT DEFINE_GUIDNAMED(AUDIO_SIGNALPROCESSINGMODE_DEFAULT)
```

原材料

```cpp
#define STATIC_AUDIO_SIGNALPROCESSINGMODE_RAW 0x9e90ea20, 0xb493, 0x4fd1, 0xa1, 0xa8, 0x7e, 0x13, 0x61, 0xa9, 0x56, 0xcf
DEFINE_GUIDSTRUCT("9E90EA20-B493-4FD1-A1A8-7E1361A956CF", AUDIO_SIGNALPROCESSINGMODE_RAW);
#define AUDIO_SIGNALPROCESSINGMODE_RAW DEFINE_GUIDNAMED(AUDIO_SIGNALPROCESSINGMODE_RAW)
```

回声取消

```cpp
#define STATIC_AUDIO_EFFECT_TYPE_ACOUSTIC_ECHO_CANCELLATION 0x6f64adbe, 0x8211, 0x11e2, 0x8c, 0x70, 0x2c, 0x27, 0xd7, 0xf0, 0x01, 0xfa
DEFINE_GUIDSTRUCT("6f64adbe-8211-11e2-8c70-2c27d7f001fa", AUDIO_EFFECT_TYPE_ACOUSTIC_ECHO_CANCELLATION);
#define AUDIO_EFFECT_TYPE_ACOUSTIC_ECHO_CANCELLATION DEFINE_GUIDNAMED(AUDIO_EFFECT_TYPE_ACOUSTIC_ECHO_CANCELLATION)
```

干扰性抑制

```cpp
#define STATIC_AUDIO_EFFECT_TYPE_NOISE_SUPPRESSION          0x6f64adbf, 0x8211, 0x11e2, 0x8c, 0x70, 0x2c, 0x27, 0xd7, 0xf0, 0x01, 0xfa
DEFINE_GUIDSTRUCT("6f64adbf-8211-11e2-8c70-2c27d7f001fa", AUDIO_EFFECT_TYPE_NOISE_SUPPRESSION);
#define AUDIO_EFFECT_TYPE_NOISE_SUPPRESSION DEFINE_GUIDNAMED(AUDIO_EFFECT_TYPE_NOISE_SUPPRESSION)
```

自动增益控制

```cpp
#define STATIC_AUDIO_EFFECT_TYPE_AUTOMATIC_GAIN_CONTROL     0x6f64adc0, 0x8211, 0x11e2, 0x8c, 0x70, 0x2c, 0x27, 0xd7, 0xf0, 0x01, 0xfa
DEFINE_GUIDSTRUCT("6f64adc0-8211-11e2-8c70-2c27d7f001fa", AUDIO_EFFECT_TYPE_AUTOMATIC_GAIN_CONTROL);
#define AUDIO_EFFECT_TYPE_AUTOMATIC_GAIN_CONTROL DEFINE_GUIDNAMED(AUDIO_EFFECT_TYPE_AUTOMATIC_GAIN_CONTROL)
```

BEAMFORMING

```cpp
#define STATIC_AUDIO_EFFECT_TYPE_BEAMFORMING                0x6f64adc1, 0x8211, 0x11e2, 0x8c, 0x70, 0x2c, 0x27, 0xd7, 0xf0, 0x01, 0xfa
DEFINE_GUIDSTRUCT("6f64adc1-8211-11e2-8c70-2c27d7f001fa", AUDIO_EFFECT_TYPE_BEAMFORMING);
#define AUDIO_EFFECT_TYPE_BEAMFORMING DEFINE_GUIDNAMED(AUDIO_EFFECT_TYPE_BEAMFORMING)
```

删除恒定音调

```cpp
#define STATIC_AUDIO_EFFECT_TYPE_CONSTANT_TONE_REMOVAL      0x6f64adc2, 0x8211, 0x11e2, 0x8c, 0x70, 0x2c, 0x27, 0xd7, 0xf0, 0x01, 0xfa
DEFINE_GUIDSTRUCT("6f64adc2-8211-11e2-8c70-2c27d7f001fa", AUDIO_EFFECT_TYPE_CONSTANT_TONE_REMOVAL);
#define AUDIO_EFFECT_TYPE_CONSTANT_TONE_REMOVAL DEFINE_GUIDNAMED(AUDIO_EFFECT_TYPE_CONSTANT_TONE_REMOVAL)
```

均衡

```cpp
#define STATIC_AUDIO_EFFECT_TYPE_EQUALIZER                  0x6f64adc3, 0x8211, 0x11e2, 0x8c, 0x70, 0x2c, 0x27, 0xd7, 0xf0, 0x01, 0xfa
DEFINE_GUIDSTRUCT("6f64adc3-8211-11e2-8c70-2c27d7f001fa", AUDIO_EFFECT_TYPE_EQUALIZER);
#define AUDIO_EFFECT_TYPE_EQUALIZER DEFINE_GUIDNAMED(AUDIO_EFFECT_TYPE_EQUALIZER)
```

响度均衡器

```cpp
#define STATIC_AUDIO_EFFECT_TYPE_LOUDNESS_EQUALIZER         0x6f64adc4, 0x8211, 0x11e2, 0x8c, 0x70, 0x2c, 0x27, 0xd7, 0xf0, 0x01, 0xfa
DEFINE_GUIDSTRUCT("6f64adc4-8211-11e2-8c70-2c27d7f001fa", AUDIO_EFFECT_TYPE_LOUDNESS_EQUALIZER);
#define AUDIO_EFFECT_TYPE_LOUDNESS_EQUALIZER DEFINE_GUIDNAMED(AUDIO_EFFECT_TYPE_LOUDNESS_EQUALIZER)
```

低音增强

```cpp
#define STATIC_AUDIO_EFFECT_TYPE_BASS_BOOST                 0x6f64adc5, 0x8211, 0x11e2, 0x8c, 0x70, 0x2c, 0x27, 0xd7, 0xf0, 0x01, 0xfa
DEFINE_GUIDSTRUCT("6f64adc5-8211-11e2-8c70-2c27d7f001fa", AUDIO_EFFECT_TYPE_BASS_BOOST);
#define AUDIO_EFFECT_TYPE_BASS_BOOST DEFINE_GUIDNAMED(AUDIO_EFFECT_TYPE_BASS_BOOST)
```

虚环绕

```cpp
#define STATIC_AUDIO_EFFECT_TYPE_VIRTUAL_SURROUND           0x6f64adc6, 0x8211, 0x11e2, 0x8c, 0x70, 0x2c, 0x27, 0xd7, 0xf0, 0x01, 0xfa
DEFINE_GUIDSTRUCT("6f64adc6-8211-11e2-8c70-2c27d7f001fa", AUDIO_EFFECT_TYPE_VIRTUAL_SURROUND);
#define AUDIO_EFFECT_TYPE_VIRTUAL_SURROUND DEFINE_GUIDNAMED(AUDIO_EFFECT_TYPE_VIRTUAL_SURROUND)
```

虚拟耳机

```cpp
#define STATIC_AUDIO_EFFECT_TYPE_VIRTUAL_HEADPHONES         0x6f64adc7, 0x8211, 0x11e2, 0x8c, 0x70, 0x2c, 0x27, 0xd7, 0xf0, 0x01, 0xfa
DEFINE_GUIDSTRUCT("6f64adc7-8211-11e2-8c70-2c27d7f001fa", AUDIO_EFFECT_TYPE_VIRTUAL_HEADPHONES);
#define AUDIO_EFFECT_TYPE_VIRTUAL_HEADPHONES DEFINE_GUIDNAMED(AUDIO_EFFECT_TYPE_VIRTUAL_HEADPHONES)
```

房间更正

```cpp
#define STATIC_AUDIO_EFFECT_TYPE_ROOM_CORRECTION            0x6f64adc9, 0x8211, 0x11e2, 0x8c, 0x70, 0x2c, 0x27, 0xd7, 0xf0, 0x01, 0xfa
DEFINE_GUIDSTRUCT("6f64adc9-8211-11e2-8c70-2c27d7f001fa", AUDIO_EFFECT_TYPE_ROOM_CORRECTION);
#define AUDIO_EFFECT_TYPE_ROOM_CORRECTION DEFINE_GUIDNAMED(AUDIO_EFFECT_TYPE_ROOM_CORRECTION)
```

低音管理

```cpp
#define STATIC_AUDIO_EFFECT_TYPE_BASS_MANAGEMENT            0x6f64adca, 0x8211, 0x11e2, 0x8c, 0x70, 0x2c, 0x27, 0xd7, 0xf0, 0x01, 0xfa
DEFINE_GUIDSTRUCT("6f64adca-8211-11e2-8c70-2c27d7f001fa", AUDIO_EFFECT_TYPE_BASS_MANAGEMENT);
#define AUDIO_EFFECT_TYPE_BASS_MANAGEMENT DEFINE_GUIDNAMED(AUDIO_EFFECT_TYPE_BASS_MANAGEMENT)
```

环境影响

```cpp
#define STATIC_AUDIO_EFFECT_TYPE_ENVIRONMENTAL_EFFECTS      0x6f64adcb, 0x8211, 0x11e2, 0x8c, 0x70, 0x2c, 0x27, 0xd7, 0xf0, 0x01, 0xfa
DEFINE_GUIDSTRUCT("6f64adcb-8211-11e2-8c70-2c27d7f001fa", AUDIO_EFFECT_TYPE_ENVIRONMENTAL_EFFECTS);
#define AUDIO_EFFECT_TYPE_ENVIRONMENTAL_EFFECTS DEFINE_GUIDNAMED(AUDIO_EFFECT_TYPE_ENVIRONMENTAL_EFFECTS)
```

扬声器保护

```cpp
#define STATIC_AUDIO_EFFECT_TYPE_SPEAKER_PROTECTION         0x6f64adcc, 0x8211, 0x11e2, 0x8c, 0x70, 0x2c, 0x27, 0xd7, 0xf0, 0x01, 0xfa
DEFINE_GUIDSTRUCT("6f64adcc-8211-11e2-8c70-2c27d7f001fa", AUDIO_EFFECT_TYPE_SPEAKER_PROTECTION);
#define AUDIO_EFFECT_TYPE_SPEAKER_PROTECTION DEFINE_GUIDNAMED(AUDIO_EFFECT_TYPE_SPEAKER_PROTECTION)
```

扬声器补偿

```cpp
#define STATIC_AUDIO_EFFECT_TYPE_SPEAKER_COMPENSATION       0x6f64adcd, 0x8211, 0x11e2, 0x8c, 0x70, 0x2c, 0x27, 0xd7, 0xf0, 0x01, 0xfa
DEFINE_GUIDSTRUCT("6f64adcd-8211-11e2-8c70-2c27d7f001fa", AUDIO_EFFECT_TYPE_SPEAKER_COMPENSATION);
#define AUDIO_EFFECT_TYPE_SPEAKER_COMPENSATION DEFINE_GUIDNAMED(AUDIO_EFFECT_TYPE_SPEAKER_COMPENSATION)
```

动态范围压缩

```cpp
#define STATIC_AUDIO_EFFECT_TYPE_DYNAMIC_RANGE_COMPRESSION  0x6f64adce, 0x8211, 0x11e2, 0x8c, 0x70, 0x2c, 0x27, 0xd7, 0xf0, 0x01, 0xfa
DEFINE_GUIDSTRUCT("6f64adce-8211-11e2-8c70-2c27d7f001fa", AUDIO_EFFECT_TYPE_DYNAMIC_RANGE_COMPRESSION);
#define AUDIO_EFFECT_TYPE_DYNAMIC_RANGE_COMPRESSION DEFINE_GUIDNAMED(AUDIO_EFFECT_TYPE_DYNAMIC_RANGE_COMPRESSION)
```

 

 




