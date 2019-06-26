---
title: 音频信号处理模式
description: 驱动程序声明支持的音频信号处理模式下为每个设备。
ms.assetid: 104275F8-2302-484B-B673-7448CAA1F793
ms.date: 05/14/2018
ms.localizationpriority: medium
ms.openlocfilehash: 430cdfae2c6ea60336ad325814f58595c23a6320
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67355656"
---
# <a name="audio-signal-processing-modes"></a>音频信号处理模式


驱动程序声明支持的音频信号处理模式下为每个设备。

## <a name="span-idavailablesignalprocessingmodesspanspan-idavailablesignalprocessingmodesspanspan-idavailablesignalprocessingmodesspanavailable-signal-processing-modes"></a><span id="Available_Signal_Processing_Modes"></span><span id="available_signal_processing_modes"></span><span id="AVAILABLE_SIGNAL_PROCESSING_MODES"></span>可用的信号处理模式


（所选应用程序） 的音频类别将映射到音频模式 （由驱动程序定义）。 Windows 定义了七个音频信号处理模式。 Oem 和 Ihv 可以确定他们想要实现的模式。 建议 Ihv/Oem 利用新的模式来添加优化要提供最佳用户体验的音频信号的音频效果。 如下所示的表总结了模式。

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
<td align="left"><strong>说明</strong></td>
</tr>
<tr class="even">
<td align="left">原始</td>
<td align="left">两者</td>
<td align="left"><p>Raw 模式指定不应不进行任何应用于流的信号处理。</p>
<p>应用程序可以请求将完全保持不变的原始流并执行其自己的信号处理。</p></td>
</tr>
<tr class="odd">
<td align="left">默认</td>
<td align="left">两者</td>
<td align="left"><p>此模式下定义的默认音频处理。</p></td>
</tr>
<tr class="even">
<td align="left">电影 *</td>
<td align="left">呈现</td>
<td align="left">电影音频播放</td>
</tr>
<tr class="odd">
<td align="left">媒体 *</td>
<td align="left">两者</td>
<td align="left">音频播放音乐 （大多数媒体流的默认值）</td>
</tr>
<tr class="even">
<td align="left">语音 *</td>
<td align="left">捕获</td>
<td align="left">（例如输入 Cortana） 的人的语音捕获</td>
</tr>
<tr class="odd">
<td align="left">通信 *</td>
<td align="left">两者</td>
<td align="left">VOIP 呈现并捕获 （例如 Skype、 Lync）</td>
</tr>
<tr class="even">
<td align="left">通知 *</td>
<td align="left">呈现</td>
<td align="left">铃声，警报、 警报等。</td>
</tr>
</tbody>
</table>

 

\* Windows 10 中的新增功能。

## <a name="span-idsignalprocessingmodedriverrequirementsspanspan-idsignalprocessingmodedriverrequirementsspanspan-idsignalprocessingmodedriverrequirementsspansignal-processing-mode-driver-requirements"></a><span id="Signal_Processing_Mode_Driver_Requirements"></span><span id="signal_processing_mode_driver_requirements"></span><span id="SIGNAL_PROCESSING_MODE_DRIVER_REQUIREMENTS"></span>信号处理模式驱动程序要求


音频设备驱动程序需要支持至少*Raw*或*默认*模式。 在支持其他模式是可选的。

很可能不是所有模式可能都是可供特定的系统。 驱动程序定义的信号处理它们支持的模式 （即哪些类型的未安装该驱动程序的一部分），并相应地告知操作系统。 如果驱动程序不支持特定的模式下，Windows 将使用下一步最佳匹配模式。

下图显示了支持多个模式的系统：

![多个音频模式 ](images/audio-modes-win-10.png)

## <a name="span-idwindowsaudiostreamcategoriesspanspan-idwindowsaudiostreamcategoriesspanspan-idwindowsaudiostreamcategoriesspanwindows-audio-stream-categories"></a><span id="Windows_Audio_Stream_Categories"></span><span id="windows_audio_stream_categories"></span><span id="WINDOWS_AUDIO_STREAM_CATEGORIES"></span>Windows 音频 Stream 类别


有关音频流的使用情况情况通知给系统，以便应用程序可以选择以标记与特定的音频流类别流。 应用程序可以设置音频类别，创建音频流后，只需使用任何音频 Api。 Windows 10 中有九个音频流类别。

|                |                                                                                                       |
|----------------|-------------------------------------------------------------------------------------------------------|
| **类别**   | **说明**                                                                                       |
| 电影          | 电影、 视频中，对话框 (替换 ForegroundOnlyMedia)                                              |
| Media          | 媒体的播放 (替换 BackgroundCapableMedia) 的默认类别                                 |
| 游戏聊天      | 中的游戏用户之间的沟通 （Windows 10 中的新类别）                                      |
| 语音         | 语音输入 （例如个人助理） 和输出 （例如导航应用程序） （Windows 10 中的新类别） |
| Communications | VOIP，实时聊天                                                                                  |
| 警报         | 警报、 电话铃声、 通知                                                                       |
| 声音效果  | 嘟嘟声、 磕碰等等                                                                                     |
| 游戏的媒体     | 在游戏的音乐                                                                                         |
| 游戏效果   | 球跳动，汽车引擎声音、 项目符号，等等。                                                      |
| 其他          | 未分类的流                                                                                 |

 

正如前面提到，音频 （所选应用程序） 的类别将映射到音频模式 （由驱动程序定义）。 应用程序可以标记每个与一个 10 个音频类别其流。

应用程序没有更改音频类别和信号处理模式之间的映射的选项。 应用程序具有"音频处理模式"的概念不知道。 它们不能找出为每个其流使用哪些模式。

**Wasapi 就可以了代码示例**

WASAPIAudio 示例中的以下 wasapi 就可以了代码演示如何设置不同的音频类别。

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

## <a name="span-idsignalprocessingmodesandeffectsspanspan-idsignalprocessingmodesandeffectsspanspan-idsignalprocessingmodesandeffectsspansignal-processing-modes-and-effects"></a><span id="Signal_Processing_Modes_and_Effects"></span><span id="signal_processing_modes_and_effects"></span><span id="SIGNAL_PROCESSING_MODES_AND_EFFECTS"></span>信号处理模式和效果


Oem 定义影响将是用于每种模式。 Windows 定义的音频效果的 17 个类型的列表。

有关如何将不与模式相关联的信息，请参阅[实现音频处理对象](implementing-audio-processing-objects.md)。

它是应用程序可以询问哪些因素影响将 RAW 或非原始处理应用于特定的流。 应用程序还可以要求为时收到通知的效果或更改的原始数据处理状态。 应用程序可能会使用此信息以确定是否这样的通信的特定流类别不可用，或者如果只将 RAW 模式中使用。 如果只有 RAW 模式，则该应用程序可以确定其自己要添加音频的处理的程度。

如果 System.Devices.AudioDevice.RawProcessingSupported 为 true，应用程序还具有特定的流设置"使用 RAW"标志的选项。 如果 System.Devices.AudioDevice.RawProcessingSupported 为 false，应用程序不能设置"使用 RAW"标志。

应用程序看不到多少模式都存在，但 RAW/非 RAW 除外。

应用程序应请求处理，而不考虑音频硬件配置的最佳音频效果。 例如，标记流，如通信会让 Windows 知道暂停背景音乐。

有关静态音频流类别的详细信息，请参阅[AudioCategory 枚举](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Media.AudioCategory)并[MediaElement.AudioCategory 属性](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.MediaElement#Windows_UI_Xaml_Controls_MediaElement_AudioCategory)。

## <a name="span-idclsidsforsystemeffectsspanspan-idclsidsforsystemeffectsspanspan-idclsidsforsystemeffectsspanclsids-for-system-effects"></a><span id="CLSIDs_for_System_Effects"></span><span id="clsids_for_system_effects"></span><span id="CLSIDS_FOR_SYSTEM_EFFECTS"></span>系统效果的 Clsid


**FX\_DISCOVER\_EFFECTS\_APO\_CLSID**

这是 MsApoFxProxy.dll"代理效果"查询驱动程序以获取活动的效果; 的列表的 CLSID

```cpp
FX_DISCOVER_EFFECTS_APO_CLSID  = "{889C03C8-ABAD-4004-BF0A-BC7BB825E166}"
```

**KSATTRIBUTEID\_AUDIOSIGNALPROCESSING\_MODE**

KSATTRIBUTEID\_AUDIOSIGNALPROCESSING\_模式是为内核流式播放内容，用于标识正在引用该特定属性是信号处理模式属性的标识符。

\#定义语句如下所示，KSMedia.h 标头文件中都可用。

```cpp
#define STATIC_KSATTRIBUTEID_AUDIOSIGNALPROCESSING_MODE 0xe1f89eb5, 0x5f46, 0x419b, 0x96, 0x7b, 0xff, 0x67, 0x70, 0xb9, 0x84, 0x1
DEFINE_GUIDSTRUCT("E1F89EB5-5F46-419B-967B-FF6770B98401", KSATTRIBUTEID_AUDIOSIGNALPROCESSING_MODE);
#define KSATTRIBUTEID_AUDIOSIGNALPROCESSING_MODE DEFINE_GUIDNAMED(KSATTRIBUTEID_AUDIOSIGNALPROCESSING_MODE)
```

KSATTRIBUTEID\_AUDIOSIGNALPROCESSING\_的模式识别驱动程序与使用模式[ **KSDATARANGE** ](https://docs.microsoft.com/previous-versions/ff561658(v=vs.85))结构包含[ **KSATTRIBUTE\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksattribute_list)。 此列表中这是具有单个元素[ **KSATTRIBUTE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksattribute)。 属性成员**KSATTRIBUTE**结构设置为 KSATTRIBUTEID\_AUDIOSIGNALPROCESSING\_模式。

## <a name="span-idaudioeffectsspanspan-idaudioeffectsspanspan-idaudioeffectsspanaudio-effects"></a><span id="Audio_Effects"></span><span id="audio_effects"></span><span id="AUDIO_EFFECTS"></span>音频效果


适用于 Windows 10 中以下音频效果。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left">回声抵消 (AEC)</td>
<td align="left"><p>声学回声抵消 (AEC) 可提高通过删除 echo 之后它之后已在音频流中存在, 的音频质量。</p></td>
</tr>
<tr class="even">
<td align="left">干扰抑制 (NS)</td>
<td align="left"><p>干扰抑制 (NS) 禁止显示如嗡嗡和嗡嗡声，如果存在音频流中的干扰。</p></td>
</tr>
<tr class="odd">
<td align="left">自动增益控制 (AGC)</td>
<td align="left"><p>自动增益控制 (AGC)-专为提供其输出，尽管 amplitude 输入信号中的变体在受控的信号振幅。 平均值或最大资源输出信号级别用于动态调整为适当的值，启用输出，甚至使用各种输入的信号级别稳定级别输入 / 输出性能提升。</p></td>
</tr>
<tr class="even">
<td align="left">无线发送形成 (BF)</td>
<td align="left"><p>电子束以形成 (BF) 是一个信号处理技术用于定向信号传输或接收。 这是合并，实现特定成信号遇到建设性干扰，而其他人遇到破坏性会相互干扰的方式分阶段数组中的元素。 与全向接收/传输进行比较的改进称为传输接收/收益 （或丢失）。</p></td>
</tr>
<tr class="odd">
<td align="left">常量音删除</td>
<td align="left"><p>常量音删除用于会如磁带电流嘶嘶声、 电力赛事的球迷们或嗡嗡声常量背景噪音。</p></td>
</tr>
<tr class="even">
<td align="left">均衡器</td>
<td align="left"><p>均衡器效果用于更改使用线性筛选器的音频系统的频率响应。 这样的信号是提升，类似于高音或低音设置的不同部分。</p></td>
</tr>
<tr class="odd">
<td align="left">响度均衡器</td>
<td align="left"><p>响度均衡器效果调节音频输出，以便更大和更安静听起来更接近于响度的平均级别，可减少感知到的音量差别。</p></td>
</tr>
<tr class="even">
<td align="left">低音增强</td>
<td align="left"><p>在系统中具有有效的低音功能扬声器的便携式计算机例如，则有时可以通过提升受说话人的频率范围中的低音响应提高感知到的音频质量。 低音增强通过增加中间低音范围中的提升改进了使用非常小的发言人的移动设备上的声音。</p></td>
</tr>
<tr class="odd">
<td align="left">虚拟环绕</td>
<td align="left"><p>虚拟环绕使用简单的数字方法来合并两个通道的多渠道的信号。 这是允许要还原到原始多渠道信号，同时使用大多数现代音频接收器中可用的 Pro 逻辑解码器的转换后的信号的方式。 虚拟外侧代码非常适用于有两个通道声音硬件和接收方，具有环绕声音增强机制的系统。</p></td>
</tr>
<tr class="even">
<td align="left">虚拟耳机</td>
<td align="left"><p>虚拟化的环绕声允许用户将戴耳机来区分从前到后也按从左到右的声音。 这是通过传输空间帮助大脑本地化声音并将它们集成到声音字段的提示。 发出的声音感觉像超越耳机，创建"外部 head"侦听体验效果。 使用先进的技术称为头相关传输函数 (HRTF) 可实现此效果。 HRTF 生成基于人机头的形状的声学提示。 这些提示不仅可帮助查找方向的侦听器和源的声音，但它还增强了围绕侦听器的声学环境的类型。</p></td>
</tr>
<tr class="odd">
<td align="left">扬声器填充</td>
<td align="left"><p>大多数音乐生成只有两个频道和，因此，没有为优化多声道的音频设备的典型音频或视频酷爱钻研技术。 因此使用，从仅 front 左侧和 front 右侧 loudspeakers 音乐是不太理想的音频体验。 演讲者填充模拟多渠道扬声器安装程序。 这样，否则将只有两个扬声器播放上所有的协助，增强空间成名 loudspeakers 播放的音乐。</p></td>
</tr>
<tr class="even">
<td align="left">房间修正</td>
<td align="left"><p>聊天室更正通过自动计算延迟，频率响应的最佳组合优化空间，例如，在躺椅 center 缓冲中的特定位置的侦听体验，并获得调整。</p>
<p>聊天室更正功能更好地匹配到视频的屏幕上的图像的声音并也是在桌面的演讲者在使用了非标准位置中的放置位置的情况下很有用。 因为它更好地解释人耳在其中处理声音的方式，房间更正处理是对高端接收器中的类似功能的改进。</p>
<p>使用的麦克风，帮助执行校准和过程可以用于立体声和多通道系统。 用户将麦克风用户想要位于的位置，然后激活向导，用于测量空间响应。 该向导反过来，播放一组专门设计发出每个扬声器的声音并测量距离、 频率响应和整体提高麦克风的位置从每个扬声器。</p></td>
</tr>
<tr class="odd">
<td align="left">低音管理</td>
<td align="left"><p>有两种低音管理模式： 正向低音管理及反向低音管理。</p>
<p><em>转发低音管理</em>筛选出低频率流内容的音频数据。 正向低音管理算法与低音或到 front 左和 front 右扬声器的渠道，具体取决于可以处理深度低音频率的通道筛选的输出重定向。 此决定基于 LRBig 标志的设置。 若要设置 LRBig 标志，用户使用声音小程序在 Control Panel 中访问低音管理设置对话框。 用户选择一个复选框以指示，例如，前端右和从前端左扬声器完整范围，此操作设置 LRBig 标志。 若要清除此标志，请单击复选框以将其清除。</p>
<p><em>反向低音管理</em>将分发到其他输出通道从低音通道信号。 信号是定向到的所有通道或前端左和 front 右通道，具体取决于 LRBig 标志的设置。 到其他通道混合低音信号时，此过程将使用大量提升减少。 使用低音管理模式依赖于了重低音喇叭的可用性和主要发言人的低音处理功能。 在 Windows 中，用户提供此信息通过控制面板中的声音小程序。</p></td>
</tr>
<tr class="even">
<td align="left">环境影响</td>
<td align="left"><p>环境影响工作，以增加更多的准确地模拟实际音频环境的音频播放的实际情况。 有多种不同的环境，可进行选择，例如"stadium"模拟的体育体育场噪声。</p></td>
</tr>
<tr class="odd">
<td align="left">演讲者保护</td>
<td align="left"><p>说话人保护的目的是禁止 resonant 频率会导致执行物理到电脑的系统组件的任何损害和扬声器。 例如，某些物理硬盘可以通过在正确的频率播放大声声音已损坏。 其次，说话人保护致力于通过衰减信号，当超过特定值时到扬声器的损害降到最低。</p></td>
</tr>
<tr class="even">
<td align="left">演讲者补偿</td>
<td align="left"><p>某些扬声器是更好地重现比其他声音。 例如，特定说话人可能会如下 100 Hz 的声音。 有时音频驱动程序和固件 DSP 解决方案具有特定的性能特征的演讲者，他们所扮演的知识和他们可以添加用于补偿的演讲者限制的处理。 例如，终结点影响 (EFX) 可以创建适用于低于 100 Hz 的频率的提升。 这种效果，与在物理说话人的衰减结合使用时将导致增强音频保真度。</p></td>
</tr>
<tr class="odd">
<td align="left">动态范围压缩</td>
<td align="left"><p>动态范围压缩而安静声音放大通过收缩或"压缩"音频信号的动态范围。 音频压缩会加大静默声音的下方特定阈值时不会影响很大的声音。</p></td>
</tr>
</tbody>
</table>

 

\#定义语句如下所示，KSMedia.h 标头文件中都可用。

默认值

```cpp
#define STATIC_AUDIO_SIGNALPROCESSINGMODE_DEFAULT 0xc18e2f7e, 0x933d, 0x4965, 0xb7, 0xd1, 0x1e, 0xef, 0x22, 0x8d, 0x2a, 0xf3
DEFINE_GUIDSTRUCT("C18E2F7E-933D-4965-B7D1-1EEF228D2AF3", AUDIO_SIGNALPROCESSINGMODE_DEFAULT);
#define AUDIO_SIGNALPROCESSINGMODE_DEFAULT DEFINE_GUIDNAMED(AUDIO_SIGNALPROCESSINGMODE_DEFAULT)
```

RAW

```cpp
#define STATIC_AUDIO_SIGNALPROCESSINGMODE_RAW 0x9e90ea20, 0xb493, 0x4fd1, 0xa1, 0xa8, 0x7e, 0x13, 0x61, 0xa9, 0x56, 0xcf
DEFINE_GUIDSTRUCT("9E90EA20-B493-4FD1-A1A8-7E1361A956CF", AUDIO_SIGNALPROCESSINGMODE_RAW);
#define AUDIO_SIGNALPROCESSINGMODE_RAW DEFINE_GUIDNAMED(AUDIO_SIGNALPROCESSINGMODE_RAW)
```

回声

```cpp
#define STATIC_AUDIO_EFFECT_TYPE_ACOUSTIC_ECHO_CANCELLATION 0x6f64adbe, 0x8211, 0x11e2, 0x8c, 0x70, 0x2c, 0x27, 0xd7, 0xf0, 0x01, 0xfa
DEFINE_GUIDSTRUCT("6f64adbe-8211-11e2-8c70-2c27d7f001fa", AUDIO_EFFECT_TYPE_ACOUSTIC_ECHO_CANCELLATION);
#define AUDIO_EFFECT_TYPE_ACOUSTIC_ECHO_CANCELLATION DEFINE_GUIDNAMED(AUDIO_EFFECT_TYPE_ACOUSTIC_ECHO_CANCELLATION)
```

干扰禁止显示

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

常量音删除

```cpp
#define STATIC_AUDIO_EFFECT_TYPE_CONSTANT_TONE_REMOVAL      0x6f64adc2, 0x8211, 0x11e2, 0x8c, 0x70, 0x2c, 0x27, 0xd7, 0xf0, 0x01, 0xfa
DEFINE_GUIDSTRUCT("6f64adc2-8211-11e2-8c70-2c27d7f001fa", AUDIO_EFFECT_TYPE_CONSTANT_TONE_REMOVAL);
#define AUDIO_EFFECT_TYPE_CONSTANT_TONE_REMOVAL DEFINE_GUIDNAMED(AUDIO_EFFECT_TYPE_CONSTANT_TONE_REMOVAL)
```

均衡器

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

虚拟外侧代码

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

聊天室更正

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

演讲者保护

```cpp
#define STATIC_AUDIO_EFFECT_TYPE_SPEAKER_PROTECTION         0x6f64adcc, 0x8211, 0x11e2, 0x8c, 0x70, 0x2c, 0x27, 0xd7, 0xf0, 0x01, 0xfa
DEFINE_GUIDSTRUCT("6f64adcc-8211-11e2-8c70-2c27d7f001fa", AUDIO_EFFECT_TYPE_SPEAKER_PROTECTION);
#define AUDIO_EFFECT_TYPE_SPEAKER_PROTECTION DEFINE_GUIDNAMED(AUDIO_EFFECT_TYPE_SPEAKER_PROTECTION)
```

演讲者补偿

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

 

 




