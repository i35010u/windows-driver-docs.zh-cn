---
title: 低延迟音频
description: 本主题讨论了 Windows 10 中的音频延迟更改。 它介绍了 API 的应用程序开发人员，以及可用于支持低滞后时间的音频驱动程序中的更改的选项。
ms.assetid: 888AEF01-271D-41CD-8372-A47551348959
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7eaba9c3798c396e8198024f9a4b0368130e7d35
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67358708"
---
# <a name="low-latency-audio"></a>低延迟音频


本主题讨论了 Windows 10 中的音频延迟更改。 它介绍了 API 的应用程序开发人员，以及可用于支持低滞后时间的音频驱动程序中的更改的选项。

本主题包含以下部分。

-   [概述](#overview)
-   [定义](#definitions)
-   [Windows Audio Stack](#windows_audio_stack)
-   [Windows 10 中的音频堆栈改进](#audio_stack_improvements_in_windows_10)
-   [API 改进](#api_improvements)
-   [AudioGraph](#audiograph)
-   [Windows Audio Session API (WASAPI)](#windows_audio_session_api_wasapi)
-   [驱动程序改进](#driver_improvements)
-   [评定工具](#measurement_tools)
-   [示例](#samples)
-   [常见问题解答](#faq)

## <a name="span-idoverviewspanspan-idoverviewspanspan-idoverviewspanoverview"></a><span id="Overview"></span><span id="overview"></span><span id="OVERVIEW"></span>概述


音频的滞后时间是创建该声音的时间之间的延迟和时听说过。 具有较低的音频延迟是非常重要的几个主要方案，如下所示。

-   Pro 音频
-   音乐创建
-   Communications
-   虚拟现实
-   游戏

Windows 10 包括更改以减少音频的延迟。 本文档的目标是：

1. 描述在 Windows 中的音频延迟的源。
2. 解释减少 Windows 10 音频堆栈中的音频延迟的更改。
3. 提供有关如何应用程序开发人员和硬件制造商可以利用新的基础结构，以较低的音频延迟开发应用程序和驱动程序的引用。 本主题介绍了这些项：
4. 新[ **AudioGraph** ](https://docs.microsoft.com/uwp/api/Windows.Media.Audio.AudioGraph) API 的交互和媒体创建方案。
5. Wasapi 就可以了，以支持较低的延迟方面的更改。
6. 驱动程序 DDIs 中的增强功能。

## <a name="span-iddefinitionsspanspan-iddefinitionsspanspan-iddefinitionsspandefinitions"></a><span id="Definitions"></span><span id="definitions"></span><span id="DEFINITIONS"></span>定义


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>术语</p></td>
<td align="left"><p>描述</p></td>
</tr>
<tr class="even">
<td align="left"><p>呈现延迟</p></td>
<td align="left"><p>应用程序提交到呈现 Api，直到扬声器发出的时间的音频数据的缓冲区的时间之间的延迟。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>捕获延迟</p></td>
<td align="left"><p>声音从麦克风捕获发送到捕获正在使用的应用程序的 Api 的时间之前的时间之间的延迟。</p></td>
</tr>
<tr class="even">
<td align="left"><p>往返延迟的情况</p></td>
<td align="left"><p>从麦克风捕获、 处理的应用程序和提交应用程序呈现到扬声器的声音的时间之间的延迟。 它是大致相同，以呈现延迟 + 捕获延迟。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>Touch 应用程序延迟</p></td>
<td align="left"><p>在用户点击屏幕信号发送到应用程序之前的时间之间的延迟。</p></td>
</tr>
<tr class="even">
<td align="left"><p>触摸声音延迟</p></td>
<td align="left"><p>在用户点击屏幕上，该事件的时间之间的延迟将转到应用程序，并通过扬声器播放音频。 它是等于呈现延迟 + touch 应用程序的延迟。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idwindowsaudiostackspanspan-idwindowsaudiostackspanspan-idwindowsaudiostackspanwindows-audio-stack"></a><span id="Windows_Audio_Stack"></span><span id="windows_audio_stack"></span><span id="WINDOWS_AUDIO_STACK"></span>Windows Audio Stack


下图显示了 Windows 音频堆栈的简化的版本。

![显示应用程序、 音频引擎驱动程序和硬件的低延迟音频堆栈关系图](images/low-latency-audio-stack-diagram-1.png)

下面是呈现路径中的延迟的摘要：

1. 应用程序将数据写入到缓冲区
2. 音频引擎从缓冲区读取数据，并对其进行处理。 它还会加载音频处理对象 (Apo) 窗体中的音频效果。 A p o s 有关详细信息，请参阅[Windows 音频处理对象](windows-audio-processing-objects.md)。
3. 根据信号内未处理的不延迟而异。
4. 在 Windows 10 之前的延迟音频引擎是等于 ~ 12 毫秒使用浮点型数据的应用程序和约 6 毫秒使用整数数据的应用程序
5. 在 Windows 10 中，延迟减少了到 1.3ms 的所有应用程序

6. 音频引擎将处理的数据写入缓冲区。
7. 在 Windows 10 之前此缓冲区始终设置为 ~ 10 毫秒。
8. 从 Windows 10 开始，将由 （稍后在本主题中描述了对此的更多详细信息） 的音频驱动程序定义的缓冲区大小。

9. 音频驱动程序从缓冲区读取数据，并将其写入到 H/w.
10. H/W 还可以选择要处理的数据 （在其他音频效果的形式）。
11. 用户会听到说话人的音频。

下面是捕获路径中的延迟时间摘要：

1. 从麦克风捕获音频。
2. H/W 可以选择要处理的数据 （即以添加音频效果）。
3. 驱动程序从 H/W 中读取数据，并将数据写入到缓冲区。
4. 在 Windows 10 之前此缓冲区始终设置为 10 毫秒。
5. 从 Windows 10 开始，由音频驱动程序 （下文更多详细信息） 定义的缓冲区大小。

6. 音频引擎从缓冲区读取数据，并对其进行处理。 它还会加载音频处理对象 (Apo) 窗体中的音频效果。
7. 根据信号内未处理的不延迟而异。
8. 在之前 Windows 10 中，音频引擎的延迟是等于约 6 毫秒的应用程序使用浮动点数据和 ~ 0ms 使用整数数据的应用程序。
9. 在 Windows 10 中，延迟已降低为 ~ 0ms 的所有应用程序。

10. 应用程序数据是可供读取，只要其处理完毕音频引擎发出信号。
    音频堆栈还提供了排他模式的选项。 在这种情况下，数据会绕过音频引擎，并直接从应用程序到其中的驱动程序将读取从缓冲区。 但是，如果应用程序在独占模式下打开一个终结点，则其他任何应用程序可以使用该终结点来呈现或捕获音频。

需要低延迟的应用程序的另一个常用方法是使用 ASIO （音频 Stream 输入/输出） 模型，使用独占模式。 在用户安装的第三方 ASIO 驱动程序后，应用程序可以直接从应用程序到 ASIO 驱动程序发送的数据。 但是，该应用程序直接与 ASIO 驱动程序的方式写入。

（排他模式和 ASIO） 这两种方法有其自己的限制。 它们提供低延迟，但它们具有其自己的限制 （其中有些是上文所述）。 因此，音频引擎已修改，以降低延迟，同时保留了灵活性。

## <a name="span-idaudiostackimprovementsinwindows10spanspan-idaudiostackimprovementsinwindows10spanspan-idaudiostackimprovementsinwindows10spanaudio-stack-improvements-in-windows-10"></a><span id="Audio_Stack_Improvements_in_Windows_10"></span><span id="audio_stack_improvements_in_windows_10"></span><span id="AUDIO_STACK_IMPROVEMENTS_IN_WINDOWS_10"></span>Windows 10 中的音频堆栈改进


Windows 10 进行了增强以减少延迟的三个方面：

1. 使用音频的所有应用程序中会看到 4.5 16ms年减少往返延迟 （如上面章节中所述） 无需任何代码更改或驱动程序更新，相比 Windows 8.1。
   a. 使用浮点数据将具有 16ms年的应用程序降低延迟。
   b. 使用整数数据的应用程序将具有 4.5ms年较低的延迟。
2. 具有更新的驱动程序的系统将提供更低的往返延迟：。 驱动程序可以使用新 DDIs 报告支持用于操作系统和 H/w.之间传输数据的缓冲区的大小 这意味着这些数据传输不需要始终使用 10 毫秒缓冲区 （就像在以前的操作系统版本）。 相反，该驱动程序可以指定是否它可以使用小缓冲区，例如 5 毫秒，3 毫秒，1 分钟，等 b。 需要低延迟的应用程序可以使用新的音频 Api （AudioGraph 或 wasapi 就可以了），以便查询驱动程序支持的缓冲区大小，并选择将用于向/从 H/w.数据传输
3. 当应用程序使用低于特定阈值的缓冲区大小来呈现和捕获音频时，操作系统将进入以特殊模式，其中它管理其资源中来避免这种音频流和其他子系统之间产生干扰。 这将减少执行过程中的音频子系统中断并最大程度减少的音频故障的概率。 当应用程序停止流式处理时，操作系统返回到其常规执行模式。 音频子系统包含的以下资源：。 正在处理低滞后时间的音频的音频引擎线程。
   b. 所有的线程和中断的已注册 （使用中有关驱动程序资源注册的一节介绍了新 DDIs） 驱动程序。
   c. 部分或全部音频线程从请求小缓冲区的应用程序以及与请求的小缓冲区的任何应用程序共享相同的音频设备图形 （例如同一个信号处理模式） 的所有应用程序：
4. AudioGraph 流式处理路径上的回调。
5. 如果应用程序使用 wasapi 就可以了，则为已提交的工作项[实时工作队列 API](https://docs.microsoft.com/windows/desktop/ProcThread/platform-work-queue-api)或[ **MFCreateMFByteStreamOnStreamEx** ](https://docs.microsoft.com/windows/desktop/api/mfidl/nf-mfidl-mfcreatemfbytestreamonstreamex)并被标记为"音频"或者"ProAudio"。

## <a name="span-idapiimprovementsspanspan-idapiimprovementsspanspan-idapiimprovementsspanapi-improvements"></a><span id="API_Improvements"></span><span id="api_improvements"></span><span id="API_IMPROVEMENTS"></span>API 改进


以下两个 Windows 10 Api 提供低延迟功能：

-   [**AudioGraph**](https://docs.microsoft.com/uwp/api/Windows.Media.Audio.AudioGraph)
-   [Windows Audio Session API (WASAPI)](https://docs.microsoft.com/windows/desktop/CoreAudio/wasapi)

这是应用程序开发人员可以确定这两个 Api 来使用：

-   倾向于 AudioGraph，只要有可能开发新应用程序。
-   如果仅使用 wasapi 就可以了:
    -   您需要比提供的 AudioGraph 的更多控制。
    -   您需要降低所提供的 AudioGraph 相比的延迟。

[评定工具](#measurement_tools)本主题显示了从 Haswell 系统使用收件箱 HDAudio 驱动程序特定的度量值的部分。

以下各节将介绍每个 API 中的低延迟功能。 它会被记录在前面部分中，为了使系统，以达到最小延迟，因为它需要已更新的驱动程序支持较小的缓冲区大小。

### <a name="span-idaudiographspanspan-idaudiographspanspan-idaudiographspanaudiograph"></a><span id="AudioGraph"></span><span id="audiograph"></span><span id="AUDIOGRAPH"></span>AudioGraph

AudioGraph 是新的通用 Windows 平台 API 在 Windows 10 中，针对的是意识到交互式和音乐创建方案轻松。 AudioGraph 是提供了多种编程语言 (C++， C#，JavaScript) 和具有简单而功能丰富的编程模型。

要针对低延迟方案，提供 AudioGraph [AudioGraphSettings::QuantumSizeSelectionMode 属性](https://docs.microsoft.com/uwp/api/Windows.Media.Audio.AudioGraphSettings#Windows_Media_Audio_AudioGraphSettings_QuantumSizeSelectionMode)。 此属性可以显示下表中的以下值之一：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>ReplTest1</p></td>
<td align="left"><p>描述</p></td>
</tr>
<tr class="even">
<td align="left"><p>SystemDefault</p></td>
<td align="left"><p>将缓冲区设置为默认缓冲区大小 （约 10 毫秒）</p></td>
</tr>
<tr class="odd">
<td align="left"><p>LowestLatency</p></td>
<td align="left"><p>将缓冲区设置为驱动程序支持的最小值</p></td>
</tr>
<tr class="even">
<td align="left"><p>ClosestToDesired</p></td>
<td align="left"><p>设置为等于 DesiredSamplesPerQuantum 属性定义的值或值接近于 DesiredSamplesPerQuantum 所支持的驱动程序的缓冲区大小。</p></td>
</tr>
</tbody>
</table>

 

AudioCreation 示例 (可在 GitHub 上下载： <https://github.com/Microsoft/Windows-universal-samples/tree/master/Samples/AudioCreation>) 演示如何使用 AudioGraph 以降低延迟。 下面的代码段演示如何设置最小缓冲区大小：

```cpp
AudioGraphSettings settings = new AudioGraphSettings(AudioRenderCategory.Media);
settings.QuantumSizeSelectionMode = QuantumSizeSelectionMode.LowestLatency;
CreateAudioGraphResult result = await AudioGraph.CreateAsync(settings);
```

### <a name="span-idwindowsaudiosessionapiwasapispanspan-idwindowsaudiosessionapiwasapispanspan-idwindowsaudiosessionapiwasapispanwindows-audio-session-api-wasapi"></a><span id="Windows_Audio_Session_API_WASAPI"></span><span id="windows_audio_session_api_wasapi"></span><span id="WINDOWS_AUDIO_SESSION_API_WASAPI"></span>Windows 音频会话 API （wasapi 就可以了）

从 Windows 10 开始，wasapi 就可以了已得到增强：

-   允许应用程序发现的缓冲区大小 （即周期值） 的支持给定的音频设备的音频驱动程序的范围。 这使得应用程序的默认缓冲区大小之间进行选择 （10 毫秒） 或一个较小缓冲区 (&lt;10 毫秒) 在共享模式下打开流时。 如果应用程序未指定缓冲区大小，则它将使用默认的缓冲区大小。
-   允许应用程序发现的当前格式和周期的音频引擎。 这允许应用程序管理单元为音频引擎的当前设置。
-   允许的应用程序来指定它想要指定不进行任何重新采样的音频引擎的格式中的呈现/捕获

上述功能会在所有 Windows 设备上可用。 但是，某些设备具有足够的资源和更新的驱动程序将提供比其他更好的用户体验。

上述功能提供的名为的新界面[ **IAudioClient3**](https://docs.microsoft.com/windows/desktop/api/audioclient/nn-audioclient-iaudioclient3)，又派生自[ **IAudioClient2**](https://docs.microsoft.com/windows/desktop/api/audioclient/nn-audioclient-iaudioclient2)。

[**IAudioClient3** ](https://docs.microsoft.com/windows/desktop/api/audioclient/nn-audioclient-iaudioclient3)定义以下三种方法：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>方法</p></td>
<td align="left"><p>描述</p></td>
</tr>
<tr class="even">
<td align="left"><p>GetCurrentSharedModeEnginePeriod</p></td>
<td align="left"><p>返回当前格式和周期的音频引擎</p></td>
</tr>
<tr class="odd">
<td align="left"><p>GetSharedModeEnginePeriod</p></td>
<td align="left"><p>返回由指定的流格式的引擎支持周期的范围</p></td>
</tr>
<tr class="even">
<td align="left"><p>InitializeSharedAudioStream</p></td>
<td align="left"><p>初始化指定周期的一个共享的流</p></td>
</tr>
</tbody>
</table>

 

WASAPIAudio 示例 (可在 GitHub 上： <https://github.com/Microsoft/Windows-universal-samples/tree/master/Samples/WindowsAudioSession>) 演示如何使用 IAudioClient3 以降低延迟。

以下代码片段演示如何音乐创建应用程序可以在系统支持的最低延迟设置操作。

```cpp
// 1. Activation

// Get a string representing the Default Audio (Render|Capture) Device
m_DeviceIdString = MediaDevice::GetDefaultAudio(Render|Capture)Id( 
Windows::Media::Devices::AudioDeviceRole::Default );

// This call must be made on the main UI thread.  Async operation will call back to 
// IActivateAudioInterfaceCompletionHandler::ActivateCompleted, which must be an agile // interface implementation
hr = ActivateAudioInterfaceAsync( m_DeviceIdString->Data(), __uuidof(IAudioClient3), 
nullptr, this, &asyncOp );

// 2. Setting the audio client properties – note that low latency offload is not supported

AudioClientProperties audioProps = {0};
audioProps.cbSize = sizeof( AudioClientProperties );
audioProps.eCategory = AudioCategory_Media;

// if the device has System.Devices.AudioDevice.RawProcessingSupported set to true and you want to use raw mode
// audioProps.Options |= AUDCLNT_STREAMOPTIONS_RAW;
//
// if it is important to avoid resampling in the audio engine, set this flag
// audioProps.Options |= AUDCLNT_STREAMOPTIONS_MATCH_FORMAT;


hr = m_AudioClient->SetClientProperties( &audioProps ); if (FAILED(hr)) { ... }

// 3. Querying the legal periods

hr = m_AudioClient->GetMixFormat( &mixFormat ); if (FAILED(hr)) { ... }

hr = m_AudioClient->GetSharedModeEnginePeriod(wfx, &defaultPeriodInFrames, &fundamentalPeriodInFrames, &minPeriodInFrames, &maxPeriodInFrames); if (FAILED(hr)) { ... }

// legal periods are any multiple of fundamentalPeriodInFrames between 
// minPeriodInFrames and maxPeriodInFrames, inclusive
// the Windows shared-mode engine uses defaultPeriodInFrames unless an audio client // has specifically requested otherwise

// 4. Initializing a low-latency client

hr = m_AudioClient->InitializeSharedAudioStream(
         AUDCLNT_STREAMFLAGS_EVENTCALLBACK,
         desiredPeriodInFrames,
         mixFormat,
         nullptr); // audio session GUID
         if (AUDCLNT_E_ENGINE_PERIODICITY_LOCKED == hr) {
         /* engine is already running at a different period; call m_AudioClient->GetSharedModeEnginePeriod to see what it is */
         } else if (FAILED(hr)) {
             ...
         }

// 5. Initializing a client with a specific format (if the format needs to be different than the default format)

AudioClientProperties audioProps = {0};
audioProps.cbSize = sizeof( AudioClientProperties );
audioProps.eCategory = AudioCategory_Media;
audioProps.Options |= AUDCLNT_STREAMOPTIONS_MATCH_FORMAT;

hr = m_AudioClient->SetClientProperties( &audioProps ); 
if (FAILED(hr)) { ... }

hr = m_AudioClient->IsFormatSupported(AUDCLNT_SHAREMODE_SHARED, appFormat, &closest);
if (S_OK == hr) {
       /* device supports the app format */
} else if (S_FALSE == hr) {
       /* device DOES NOT support the app format; closest supported format is in the "closest" output variable */
} else {
       /* device DOES NOT support the app format, and Windows could not find a close supported format */
}

hr = m_AudioClient->InitializeSharedAudioStream(
       AUDCLNT_STREAMFLAGS_EVENTCALLBACK,
       defaultPeriodInFrames,
       appFormat,
       nullptr); // audio session GUID
if (AUDCLNT_E_ENGINE_FORMAT_LOCKED == hr) {
       /* engine is already running at a different format */
} else if (FAILED(hr)) {
       ...
}
```

此外，建议使用 wasapi 就可以了也使用的应用程序[实时工作队列 API](https://docs.microsoft.com/windows/desktop/ProcThread/platform-work-queue-api)或[ **MFCreateMFByteStreamOnStreamEx** ](https://docs.microsoft.com/windows/desktop/api/mfidl/nf-mfidl-mfcreatemfbytestreamonstreamex)来创建工作项和将它们标记为音频或 Pro 音频，而不是其自己的线程。 这样，操作系统会避免干扰非音频子系统的方式来管理它们。 与此相反，所有 AudioGraph 线程自动都管理正确的操作系统。 WASAPIAudio 示例中的以下代码段演示如何使用 MF 工作队列 Api。

```cpp
// Specify Source Reader Attributes 
Attributes->SetUnknown( MF_SOURCE_READER_ASYNC_CALLBACK, static_cast<IMFSourceReaderCallback *>(this) ); 
    if (FAILED( hr )) 
    { 
        goto exit; 
    } 
    Attributes->SetString( MF_READWRITE_MMCSS_CLASS_AUDIO, L"Audio" ); 
    if (FAILED( hr )) 
    { 
        goto exit; 
    } 
    Attributes->SetUINT32( MF_READWRITE_MMCSS_PRIORITY_AUDIO, 0 ); 
    if (FAILED( hr )) 
    { 
        goto exit; 
    } 
    // Create a stream from IRandomAccessStream 
    hr = MFCreateMFByteStreamOnStreamEx (reinterpret_cast<IUnknown*>(m_ContentStream), &ByteStream ); 
    if ( FAILED( hr ) ) 
    { 
        goto exit; 
    } 
    // Create source reader 
    hr = MFCreateSourceReaderFromByteStream( ByteStream, Attributes, &m_MFSourceReader );
```

或者，以下代码片段演示如何使用 RT 工作队列 Api。

```cpp
#define INVALID_WORK_QUEUE_ID 0xffffffff
DWORD g_WorkQueueId = INVALID_WORK_QUEUE_ID;
//#define MMCSS_AUDIO_CLASS    L"Audio"
//#define MMCSS_PROAUDIO_CLASS L"ProAudio"

STDMETHODIMP TestClass::GetParameters(DWORD* pdwFlags, DWORD* pdwQueue)
{
       HRESULT hr = S_OK;
       *pdwFlags = 0;
       *pdwQueue = g_WorkQueueId;
       return hr;
}

//-------------------------------------------------------
STDMETHODIMP TestClass::Invoke(IRtwqAsyncResult* pAsyncResult)
{
       HRESULT hr = S_OK;
       IUnknown *pState = NULL;
       WCHAR className[20];
       DWORD  bufferLength = 20;
       DWORD taskID = 0;
       LONG priority = 0;

       printf("Callback is invoked pAsyncResult(0x%0x)  Current process id :0x%0x Current thread id :0x%0x\n", (INT64)pAsyncResult, GetCurrentProcessId(), GetCurrentThreadId());

       hr = RtwqGetWorkQueueMMCSSClass(g_WorkQueueId, className, &bufferLength);
       IF_FAIL_EXIT(hr, Exit);

       if (className[0])
       {
              hr = RtwqGetWorkQueueMMCSSTaskId(g_WorkQueueId, &taskID);
              IF_FAIL_EXIT(hr, Exit);

              hr = RtwqGetWorkQueueMMCSSPriority(g_WorkQueueId, &priority);
              IF_FAIL_EXIT(hr, Exit);
              printf("MMCSS: [%ws] taskID (%d) priority(%d)\n", className, taskID, priority);
       }
       else
       {
              printf("non-MMCSS\n");
       }
       hr = pAsyncResult->GetState(&pState);
       IF_FAIL_EXIT(hr, Exit);

Exit:
       return S_OK;
}
//-------------------------------------------------------

int _tmain(int argc, _TCHAR* argv[])
{
       HRESULT hr = S_OK;
       HANDLE signalEvent;
       LONG Priority = 1;
       IRtwqAsyncResult *pAsyncResult = NULL;
       RTWQWORKITEM_KEY workItemKey = NULL;;
       IRtwqAsyncCallback *callback = NULL;
       IUnknown *appObject = NULL;
       IUnknown *appState = NULL;
       DWORD taskId = 0;
       TestClass cbClass;
       NTSTATUS status;

       hr = RtwqStartup();
       IF_FAIL_EXIT(hr, Exit);

       signalEvent = CreateEvent(NULL, true, FALSE, NULL);
       IF_TRUE_ACTION_EXIT(signalEvent == NULL, hr = E_OUTOFMEMORY, Exit);

       g_WorkQueueId = RTWQ_MULTITHREADED_WORKQUEUE;

       hr = RtwqLockSharedWorkQueue(L"Audio", 0, &taskId, &g_WorkQueueId);
       IF_FAIL_EXIT(hr, Exit);

       hr = RtwqCreateAsyncResult(NULL, reinterpret_cast<IRtwqAsyncCallback*>(&cbClass), NULL, &pAsyncResult);
       IF_FAIL_EXIT(hr, Exit);

       hr = RtwqPutWaitingWorkItem(signalEvent, Priority, pAsyncResult, &workItemKey);
       IF_FAIL_EXIT(hr, Exit);

       for (int i = 0; i < 5; i++)
       {
              SetEvent(signalEvent);
              Sleep(30);
              hr = RtwqPutWaitingWorkItem(signalEvent, Priority, pAsyncResult, &workItemKey);
              IF_FAIL_EXIT(hr, Exit);
    }

Exit:
       if (pAsyncResult)
       {
              pAsyncResult->Release();
       }

      if (INVALID_WORK_QUEUE_ID != g_WorkQueueId)
      {
        hr = RtwqUnlockWorkQueue(g_WorkQueueId);
        if (FAILED(hr))
        {
            printf("Failed with RtwqUnlockWorkQueue 0x%x\n", hr);
        }

        hr = RtwqShutdown();
        if (FAILED(hr))
        {
            printf("Failed with RtwqShutdown 0x%x\n", hr);
        }
      }

       if (FAILED(hr))
       {
          printf("Failed with error code 0x%x\n", hr);
       }
       return 0;
}
```

最后，使用标记 wasapi 就可以了需要的应用程序开发人员使用的音频的类别以及是否使用原始的信号处理模式下，其流基于每个流的功能。 建议所有音频流不会使用原始的信号处理模式下，除非含义被理解。 Raw 模式将绕过所有信号处理，已被选由 OEM，因此：

-   为特定终结点的呈现信号可能欠佳。
-   捕获信号可能来自应用程序不能理解的格式。
-   延迟可能会提高。

## <a name="span-iddriverimprovementsspanspan-iddriverimprovementsspanspan-iddriverimprovementsspandriver-improvements"></a><span id="Driver_Improvements"></span><span id="driver_improvements"></span><span id="DRIVER_IMPROVEMENTS"></span>驱动程序改进


为了使音频驱动程序以支持较低的延迟，Windows 10 提供了以下 3 个新功能：

1. \[必需\]声明在每个模式下支持的最小缓冲区大小。
2. \[可选的但建议\]提高驱动程序和操作系统之间数据流的协调。
3. \[可选的但建议\]注册驱动程序资源 （中断、 线程），以便它们可以受到低延迟方案中的操作系统。
HDAudio 微型端口功能的驱动程序通过收件箱 HDAudio 总线驱动程序 hdaudbus.sys 枚举不需要注册 HDAudio 中断，因为这通过 hdaudbus.sys 已完成。 但是，如果微型端口驱动程序创建自己的线程，则它需要注册它们。

以下三个部分将介绍更多深入分析的每个新功能。

**1.声明的最小缓冲区大小。**

驱动程序将在各种约束下操作时操作系统、 驱动程序和硬件之间移动的音频数据。 这些约束可能是由于内存与硬件之间移动数据的物理硬件传输和/或由于信号处理的硬件或关联的 DSP 中的模块。

在 Windows 10 中驱动程序可以表示其缓冲区大小功能使用 DEVPKEY\_KsAudio\_PacketSize\_约束设备属性。 此属性允许用户定义的绝对最小缓冲区大小，支持的驱动程序，以及针对每个信号处理 （特定于模式的约束需要高于驱动程序最小缓冲区大小的模式特定的缓冲区大小限制否则将忽略音频堆栈)。 例如，下面的代码段演示如何声明一个驱动程序绝对最小的支持的缓冲区大小是 1 分钟，但默认模式支持 128 框架 （这对应于 3 毫秒，如果我们假设 48khz 采样率）。

```cpp
// Describe constraints for small buffers
static struct
{
    KSAUDIO_PACKETSIZE_CONSTRAINTS TransportPacketConstraints;
    KSAUDIO_PACKETSIZE_PROCESSINGMODE_CONSTRAINT AdditionalProcessingConstraints[1];
} SysvadWaveRtPacketSizeConstraintsRender =
{
    {
        1 * HNSTIME_PER_MILLISECOND,                // 1 ms minimum processing interval
        FILE_256_BYTE_ALIGNMENT,                    // 256 byte packet size alignment
        0,                                          // reserved
        1,                                          // 1 processing constraint below
        {
            STATIC_AUDIO_SIGNALPROCESSINGMODE_DEFAULT,          // constraint for default processing mode
            128,                                  // 128 samples per processing frame
            0,                                    // N/A hns per processing frame    
       },
    },
};
```

请参阅以下主题以更深入了解这些结构：

-   [**KSAUDIO\_PACKETSIZE\_约束结构**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-_ksaudio_packetsize_constraints)
-   [**KSAUDIO\_PACKETSIZE\_PROCESSINGMODE\_约束结构**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-_ksaudio_packetsize_signalprocessingmode_constraint)

此外，sysvad 示例 (<https://github.com/Microsoft/Windows-driver-samples/tree/master/audio/sysvad>) 演示如何使用这些属性，以使驱动程序来声明每种模式的最小缓冲区。

**2.提高驱动程序和操作系统之间进行协调。**

此部分所述 DDIs 允许到驱动程序：

-   清楚地指示哪一半 （数据包） 的缓冲区是可用于操作系统，而不是 OS 猜测基于编解码器链接位置。 这有助于更快地从音频故障中恢复的操作系统。
-   根据需要优化或简化其数据传输传入和传出 WaveRT 缓冲区。 这样做的好处的量取决于 DMA 引擎设计或其他数据传输机制 WaveRT 缓冲区和 (可能是 DSP) 之间的硬件。
-   "迸发"比实时如果驱动程序已在内部累积捕获的数据更快地捕获数据。 这主要适用于语音激活方案，但在正常流以及操作期间可以应用。
-   提供有关其当前流位置而不是 OS 猜测，可能会允许极为精确地反映位置信息的时间戳信息。

此 DDI 是非常有用的情况下，使用 DSP 的位置。 但是，标准的高清晰度音频驱动程序或其他简单的循环 DMA 缓冲区设计可能找不到这些新 DDIs 中带来的巨大优势此处列出。

-   [IMiniportWaveRTInputStream](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-iminiportwavertinputstream)
-   [IMiniportWaveRTOutputStream](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-iminiportwavertoutputstream)

多个驱动程序例程返回专用于反映将的时间示例是捕获或该设备提供的 Windows 性能计数器时间戳。

设备具有复杂 DSP 中的管道和信号处理，计算准确的时间戳可能具挑战性，并且应经过深思熟虑。 时间戳不应只是反映在该示例已传输到或从操作系统到 DSP 的时间。

若要计算的性能计数器值，驱动程序和 DSP 可能采用以下方法的一些。

-   内 DSP，跟踪示例使用某些内部的 DSP 时钟的时间戳。
-   驱动程序和 DSP，计算的 Windows 性能计数器和 DSP 时钟之间的相关性。 此过程的范围可以从非常简单 （但不太精确） 到相当复杂的或新颖 （但更精确的）。
-   除非这些延迟否则实现考虑进来由于信号处理算法或管道或硬件传输任何常量的延迟。

Sysvad 示例 (<https://github.com/Microsoft/Windows-driver-samples/tree/master/audio/sysvad>) 演示如何使用上述 DDIs。

**3.注册驱动程序资源**

若要帮助确保无故障操作，音频驱动程序必须向 portcls 注册其流式处理资源。 这样，操作系统来管理资源，以避免干扰音频流和其他 subystems 之间。

Stream 资源是音频驱动程序用来处理音频流，或确保音频数据流任何资源。 支持这一次，只有两种类型的流资源： 中断和驱动程序拥有线程。 音频驱动程序应注册一个资源创建资源后并注销该资源之前将其删除。

在初始化时加载驱动程序时，或在运行时，例如，I/O 资源重新平衡时，音频驱动程序可以注册的资源。 Portcls 使用全局状态来跟踪所有音频的流式处理资源。

在某些用例，例如那些要求非常低滞后时间的音频，OS 会尝试将音频驱动程序的已注册的资源与其他操作系统、 应用程序和硬件的活动的干扰隔离。 OS 和音频子系统不这根据需要与音频驱动程序，除音频驱动程序的注册的资源进行交互。

这项要求注册流资源意味着，在流式处理管道路径的所有驱动程序必须将注册其资源直接或间接 Portcls。 音频的微型端口驱动程序将显示以下选项：

-   音频的微型端口驱动程序是其堆栈 （直接交互 h/w），在这种情况下的底部驱动程序、 驱动程序知道其流资源和它可以向 Portcls 注册它们。
-   音频的微型端口驱动程序流式处理音频其他驱动程序 （示例音频总线驱动程序） 的帮助。 这些其他驱动程序还使用必须向 Portcls 注册的资源。 这些并行/总线驱动程序堆栈可以公开一个公共 （或专用接口，如果一家供应商拥有的所有驱动程序） 音频微型端口驱动程序，用于收集此信息。
-   音频的微型端口驱动程序流式处理音频的其他驱动程序 (示例 hdaudbus) 帮助。 这些其他驱动程序还使用必须向 Portcls 注册的资源。 这些并行/总线驱动程序可以与 Portcls 链接和直接注册其资源。 请注意音频微型端口驱动程序必须让 Portcls 知道他们依赖于这些资源其他并行/总线设备 (PDOs)。 高清晰度音频基础结构使用此选项，即，hd 音频总线驱动程序链接到 Portcls 和自动执行以下步骤：
    -   注册其总线驱动程序的资源和
    -   通知 Portcls 儿童的资源依赖于父级的资源。 在高清晰度音频体系结构中，音频微型端口驱动程序只需注册其自己的驱动程序拥有的线程资源。

注意：

-   HDAudio 微型端口功能的驱动程序通过收件箱 HDAudio 总线驱动程序 hdaudbus.sys 枚举不需要注册 HDAudio 中断，因为这通过 hdaudbus.sys 已完成。 但是，如果微型端口驱动程序创建自己的线程，则它需要注册它们。
-   与 Portcls 链接仅用于注册流式处理资源的驱动程序必须更新其 Inf 以包括/需求 wdmaudio.inf 和复制 portcls.sys （和相关文件）。 新的 INF 复制部分 wdmaudio.inf 仅复制那些文件中定义。
-   仅运行在 Windows 10 中的音频驱动程序可以指向硬链接：
    -   [**PcAddStreamResource**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-pcaddstreamresource)
    -   [**PcRemoveStreamResource**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-pcremovestreamresource)
-   必须在下级 OS 运行的音频驱动程序可以使用下面的接口 (微型端口可以调用 QueryInterface IID\_IPortClsStreamResourceManager 接口，并注册其资源，仅当 PortCls 支持接口时)。
    -   [IPortClsStreamResourceManager](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-iportclsstreamresourcemanager)
        -   [**AddStreamResource**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-iportclsstreamresourcemanager-addstreamresource)
        -   [**RemoveStreamResource**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-iportclsstreamresourcemanager-removestreamresource)
-   这些 DDIs，使用此枚举和结构：
    -   [**PcStreamResourceType**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/ne-portcls-_pcstreamresourcetype)
    -   [**PCSTREAMRESOURCE\_描述符**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/ns-portcls-_pcstreamresource_descriptor)

最后，链接项以 PortCls 注册资源的唯一目的的驱动程序必须在其 inf DDInstall 部分添加以下两行。 音频的微型端口驱动程序不需要这样做因为他们已有包括需求 wdmaudio.inf 中。

```inf
[<install-section-name>]
Include=wdmaudio.inf
Needs=WDMPORTCLS.CopyFilesOnly
```

在上述行请确保该 PortCls，安装其依赖的文件。

## <a name="span-idmeasurementtoolsspanspan-idmeasurementtoolsspanspan-idmeasurementtoolsspanmeasurement-tools"></a><span id="Measurement_Tools"></span><span id="measurement_tools"></span><span id="MEASUREMENT_TOOLS"></span>评定工具


来测量往返延迟的情况，用户可以利用播放波通过演讲者并通过麦克风捕获它们的工具。 因为前者衡量的以下路径的延迟：

1. 在应用程序调用呈现 API （AudioGraph 或 wasapi 就可以了） 播放脉冲
2. 通过扬声器播放音频
3. 从麦克风捕获音频
4. 脉冲中检测到捕获 API （AudioGraph 或 wasapi 就可以了） 来测量往返延迟的情况有关不同的缓冲区的大小，用户需要安装支持小缓冲区的驱动程序。 收件箱 HDAudio 驱动程序已更新为支持 128 示例之间的缓冲区大小 (2.66ms@48kHz) 和 480 示例 (10ms@48kHz)。 以下步骤演示如何安装收件箱 HDAudio 驱动程序 （这是所有 Windows 10 Sku 的一部分）：

-   启动设备管理器。
-   下**听起来视频和游戏控制器**，双击对应于内部演讲者在设备上。
-   在下一个窗口，转到**驱动程序**选项卡。
-   选择**更新驱动程序** - &gt; **浏览计算机以查找驱动程序软件** - &gt; **从设备中的驱动程序列表中选择此计算机** - &gt; **选择高定义音频设备**然后单击**下一步**。
-   如果出现一个窗口标题为"更新驱动程序警告"，单击**是**。
-   选择**关闭**。
-   如果您要求重新启动系统，请选择**是**重新启动。
-   重新启动后，将使用系统收件箱 Microsoft HDAudio 驱动程序，并不是第三方编码解码器驱动程序。 请记住之前，使用的驱动程序，以便您可以回退到该驱动程序，如果你想要用于音频编码解码器中使用的最佳设置。

![显示 wasapi 就可以了具有不同的缓冲区大小 audiograph 的区别的往返延迟图表。 ](images/low-latency-audio-roundtrip-latency.png)

延迟 wasapi 就可以了和 AudioGraph 之间的差异是由于以下原因：

-   AudioGraph 为了同步呈现并捕获 （这不由提供 wasapi 就可以了） 中的捕获端中，添加一个缓冲区的延迟。 此添加简化了应用程序使用 AudioGraph 编写的代码。
-   没有 AudioGraph 的呈现器端中的延迟时间的附加缓冲区使用系统时&gt;6 毫秒缓冲区。
-   AudioGraph 不具有此选项来禁用捕获音频效果

## <a name="span-idsamplesspanspan-idsamplesspanspan-idsamplesspansamples"></a><span id="Samples"></span><span id="samples"></span><span id="SAMPLES"></span>示例


-   Wasapi 就可以了音频示例： <https://github.com/Microsoft/Windows-universal-samples/tree/master/Samples/WindowsAudioSession>
-   AudioCreation 示例 (AudioGraph): <https://github.com/Microsoft/Windows-universal-samples/tree/master/Samples/AudioCreation>
-   Sysvad 驱动程序示例： <https://github.com/Microsoft/Windows-driver-samples/tree/master/audio/sysvad>

## <a name="span-idfaqspanspan-idfaqspanfaq"></a><span id="FAQ"></span><span id="faq"></span>常见问题


**1.岂不更好的如果所有应用程序使用新的 Api 的较低的延迟？较低的延迟并不始终保证用户更好的用户体验？**

不一定。 较低的延迟都有其缺点：

-   较低的延迟意味着更高版本的功率消耗。 如果系统使用 10 毫秒缓冲区，则表示 CPU 将唤醒每隔 10 毫秒、 填充数据缓冲区和进入睡眠状态。 但是，如果系统使用 1 毫秒的缓冲区，这意味着 CPU 将唤醒每隔 1 毫秒。 在第二个方案中，这意味着，CPU 将唤醒的详细信息通常，将会增加的功率消耗。 这将降低电池寿命。
-   大多数应用程序依赖于音频效果，以提供最佳用户体验。 例如，媒体播放器根据想要提供高保真音频。 通信的应用程序需要最小 echo 和噪音。 向流添加这些类型的音频效果会增加其延迟时间。 这些应用程序是更感兴趣的音频延迟比音频质量。

总之，每个应用程序类型都有音频延迟方面的不同需要。 如果应用程序不需要较低的延迟，然后它不应使用新的 Api 以降低延迟。

**2.将更新为 Windows 10 的所有系统会自动都更新以支持小缓冲区？此外，将所有系统都支持相同的最小缓冲区大小？**

否。 为了使系统以支持小缓冲区，它需要有更新的驱动程序。 由 Oem 决定哪些系统将更新为支持小缓冲区。 此外，较新的系统是更 likey 以支持较旧的系统 （即新系统的滞后时间很可能低于较旧的系统） 比较小的缓冲区。

**3.如果驱动程序支持较小的缓冲区大小 (&lt;10 毫秒缓冲区)，将 Windows 10 中的所有应用程序自动使用较小的缓冲区来呈现和捕获音频？**

否。 默认情况下，Windows 10 中的所有应用程序将使用 10 毫秒缓冲区来呈现和捕获音频。 如果应用程序需要使用小缓冲区，则它需要使用新的 AudioGraph 设置或 wasapi 就可以了 IAudioClient3 接口，以执行此操作。 但是，如果在 Windows 10 中的一个应用程序请求的小缓冲区的使用情况，则音频引擎将开始传输音频，使用该特定的缓冲区大小。 在这种情况下，使用相同的终结点和模式的所有应用程序将自动切换到该较小的缓冲区大小。 低延迟的应用程序退出时，音频引擎将再次切换到 10 毫秒的缓冲区。

 

 




