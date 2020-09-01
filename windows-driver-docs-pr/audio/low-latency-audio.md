---
title: 低延迟音频
description: 本主题介绍 Windows 10 中的音频延迟更改。 它涵盖了应用程序开发人员的 API 选项，以及可用于支持低延迟音频的驱动程序中的更改。
ms.assetid: 888AEF01-271D-41CD-8372-A47551348959
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c14394be4e4a640ccfa94ad3ead2cd4c9502655b
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89211453"
---
# <a name="low-latency-audio"></a>低延迟音频

本主题介绍 Windows 10 中的音频延迟更改。 它涵盖了应用程序开发人员的 API 选项，以及可用于支持低延迟音频的驱动程序中的更改。

## <a name="overview"></a>概述

音频延迟是指在该时间内创建声音和听到声音的延迟时间。 对于几个关键方案（如下所示），具有较低的音频延迟非常重要。

- Pro 音频
- 音乐创建
- 通信
- 虚拟现实
- 游戏

Windows 10 包含更改以降低音频延迟。 本文档的目标是：

1. 描述 Windows 中的音频延迟源。
2. 说明在 Windows 10 音频堆栈中减小音频延迟的更改。
3. 提供有关应用程序开发人员和硬件制造商如何利用新基础结构的参考，以便开发低音频延迟的应用程序和驱动程序。 本主题包括以下各项：
4. 用于交互和媒体创建方案的新 [**AudioGraph**](/uwp/api/Windows.Media.Audio.AudioGraph) API。
5. WASAPI 中的更改，以支持低延迟。
6. 驱动程序 DDIs 中的增强功能。

## <a name="definitions"></a>定义

|术语|说明|
|--- |--- |
|呈现延迟|应用程序将音频数据的缓冲区提交到呈现 Api 的时间之间的延迟，直到扬声器听到该时间。|
|捕获延迟|从麦克风捕获声音到将其发送到应用程序正在使用的捕获 Api 的时间之间的延迟。|
|往返延迟|从麦克风捕获声音、由应用程序处理并由应用程序提交以呈现给扬声器的时间之间的延迟。 它大致等于呈现延迟 + 捕获延迟。|
|触控到应用延迟|用户点击屏幕到将信号发送到应用程序的时间之间的延迟。|
|触摸到声音延迟|用户点击屏幕后的延迟时间，事件会转到应用程序，并通过扬声器听到声音。 它相当于呈现延迟 + 触控到应用延迟。|

## <a name="windows-audio-stack"></a>Windows 音频堆栈

下图显示了 Windows 音频堆栈的简化版本。

![显示应用、音频引擎驱动程序和 h/w 的低延迟音频堆栈关系图](images/low-latency-audio-stack-diagram-1.png)

下面是渲染路径中延迟的摘要：

1. 应用程序将数据写入缓冲区
2. 音频引擎读取缓冲区中的数据并对其进行处理。 它还以音频处理对象的形式加载音频效果， (的) 。 有关的详细信息，请参阅 [Windows 音频处理对象](windows-audio-processing-objects.md)。
3. "中" 的延迟根据中的信号处理而变化。
4. 在 Windows 10 之前，对于使用浮点数据的应用程序，音频引擎的延迟等于 ~ 12ms，对于使用整数数据的应用程序，则为 ~ 6ms
5. 在 Windows 10 中，所有应用程序的延迟时间都缩短到1.3 毫秒

6. 音频引擎将处理的数据写入缓冲区。
7. 在 Windows 10 之前，此缓冲区始终设置为 ~ 10ms。
8. 从 Windows 10 开始，缓冲区大小由音频驱动程序定义 (详细信息，请参阅本主题) 的详细信息。

9. 音频驱动程序从缓冲区中读取数据，并将其写入 H/W。
10. H/W 还可以选择以其他音频效果) 的形式再次处理数据 (。
11. 用户从扬声器中听到音频。

下面是捕获路径中延迟的摘要：

1. 从麦克风捕获音频。
2. H/W 具有处理数据的选项， (例如添加音频效果) 。
3. 该驱动程序从 H/W 中读取数据，并将数据写入缓冲区。
4. 在 Windows 10 之前，此缓冲区始终设置为10ms。
5. 从 Windows 10 开始，缓冲区大小由音频驱动程序定义 (下面) 的更多详细信息。

6. 音频引擎读取缓冲区中的数据并对其进行处理。 它还以音频处理对象的形式加载音频效果， (的) 。
7. "中" 的延迟根据中的信号处理而变化。
8. 在 Windows 10 之前，对于使用浮点数据的应用程序，音频引擎的延迟等于 ~ 6ms，对于使用整数数据的应用程序，则为 ~ 0ms。
9. 在 Windows 10 中，延迟已减少到 ~ 0ms 适用于所有应用程序。

10. 当音频引擎完成处理后，应用程序会收到数据可供读取的信号。
    音频堆栈还提供了 "独占" 模式选项。 在这种情况下，数据将绕过音频引擎，并直接从该应用程序转到驱动程序从中读取数据的缓冲区。 但是，如果应用程序在独占模式下打开终结点，则没有其他应用程序可以使用该终结点呈现或捕获音频。

对于需要低延迟的应用程序，另一个常见的替代方法是使用 ASIO (音频流输入/输出) 模型，该模型使用独占模式。 用户安装第三方 ASIO 驱动程序后，应用程序可以将数据直接从应用程序发送到 ASIO 驱动程序。 但是，必须以这种方式编写应用程序，以便它直接与 ASIO 驱动程序进行讨论。

 (独占模式和 ASIO) 的替换都有其自己的限制。 它们提供低延迟，但它们具有自己的限制 (以上) 对此进行了说明。 因此，为了降低延迟，同时保持灵活性，音频引擎已被修改。

## <a name="audio-stack-improvements-in-windows-10"></a>Windows 10 中的音频堆栈改进

Windows 10 在三个方面进行了增强，以减少延迟：

1. 与 Windows 8.1 相比，使用音频的所有应用程序都将在上一节中所述的 (，如以上) 所述，而不进行任何代码更改或驱动程序更新。
   a. 使用浮点数据的应用程序的延迟 m32-16ms。
   b. 使用整数数据的应用程序的滞后时间较低。
2. 具有更新的驱动程序的系统将提供更低的双程延迟： a。 驱动程序可以使用新的 DDIs 来报告支持的缓冲区大小，该缓冲区用于在 OS 和 H/W 之间传输数据。 这意味着数据传输不必始终使用10ms 的缓冲区 (与以前的操作系统版本) 相同。 相反，驱动程序可以指定它是否可以使用小型缓冲区，例如5ms、3ms、1ms 等。 需要低延迟的应用程序可以使用新的音频 Api (AudioGraph 或 WASAPI) ，以便查询驱动程序支持的缓冲区大小，并选择将用于传输到/从 H/W 传输数据的缓冲区大小。
3. 当应用程序使用低于某个阈值的缓冲区大小来呈现和捕获音频时，操作系统将进入一种特殊模式，在该模式下，它会以避免音频流和其他子系统之间的干扰的方式管理其资源。 这会减少执行音频子系统的中断，并最大程度地降低音频故障的概率。 当应用程序停止流式处理时，OS 会恢复为其正常执行模式。 音频子系统包含以下资源：。 处理低延迟音频的音频引擎线程。
   b. 驱动程序已注册的所有线程和中断都 (使用有关驱动程序资源注册) 部分所述的新 DDIs。
   c. 来自应用程序的部分或全部音频线程，这些线程请求较小的缓冲区以及共享同一音频设备图形的所有应用程序 (例如，相同的信号处理模式) 与请求较小缓冲区的任何应用程序：
4. AudioGraph 在流路径上进行回调。
5. 如果应用程序使用 WASAPI，则仅提交给 [实时工作队列 API](/windows/desktop/ProcThread/platform-work-queue-api) 或 [**MFCreateMFByteStreamOnStreamEx**](/windows/desktop/api/mfidl/nf-mfidl-mfcreatemfbytestreamonstreamex) 的工作项，并将其标记为 "音频" 或 "ProAudio"。

## <a name="api-improvements"></a>API 改进

以下两个 Windows 10 Api 提供低延迟功能：

- [**AudioGraph**](/uwp/api/Windows.Media.Audio.AudioGraph)
- [Windows 音频会话 API (WASAPI) ](/windows/desktop/CoreAudio/wasapi)

这是应用程序开发人员如何确定要使用的两个 Api 中的哪一个：

- 为新的应用程序开发提供任何可能的 AudioGraph。
- 仅在以下情况下使用 WASAPI：
  - 你需要比 AudioGraph 提供的更多的控制。
  - 需要的延迟低于 AudioGraph 提供的时间。

本主题中的 " [度量工具](#measurement-tools) " 部分显示了使用收件箱 HDAudio 驱动程序从 Haswell 系统进行的特定度量。

以下各节将说明每个 API 中的低延迟功能。 如前一部分中所述，为了使系统达到最小延迟，需要具有支持小型缓冲区大小的更新驱动程序。

### <a name="audiograph"></a>AudioGraph

AudioGraph 是 Windows 10 中新的通用 Windows 平台 API，旨在轻松实现交互和音乐创建方案。 AudioGraph 以多种编程语言提供， (c + +、c #、JavaScript) 并且具有简单且功能丰富的编程模型。

为了面向低延迟方案，AudioGraph 提供了 [AudioGraphSettings：： QuantumSizeSelectionMode 属性](/uwp/api/Windows.Media.Audio.AudioGraphSettings#Windows_Media_Audio_AudioGraphSettings_QuantumSizeSelectionMode)。 此属性可以是下表中所示的以下任何值：

|值|说明|
|--- |--- |
|SystemDefault|将缓冲区设置为默认缓冲区大小 (~ 10ms) |
|LowestLatency|将缓冲区设置为驱动程序支持的最小值|
|ClosestToDesired|将缓冲区大小设置为等于 DesiredSamplesPerQuantum 属性定义的值，或设置为与驱动程序支持的 DesiredSamplesPerQuantum 接近的值。|

 可在 GitHub 上下载的 AudioCreation 示例 (： <https://github.com/Microsoft/Windows-universal-samples/tree/master/Samples/AudioCreation>) 演示如何使用 AudioGraph 以降低延迟。 下面的代码段演示如何设置最小缓冲区大小：

```csharp
AudioGraphSettings settings = new AudioGraphSettings(AudioRenderCategory.Media);
settings.QuantumSizeSelectionMode = QuantumSizeSelectionMode.LowestLatency;
CreateAudioGraphResult result = await AudioGraph.CreateAsync(settings);
```

### <a name="windows-audio-session-api-wasapi"></a>Windows 音频会话 API (WASAPI) 

从 Windows 10 开始，WASAPI 已增强到：

- 允许应用程序发现缓冲区大小范围 (例如，) 指定音频设备的音频驱动程序支持的周期值。 这样，应用程序便可以在以共享模式打开流时，在默认缓冲区大小 (10ms) 或小型缓冲区 (&lt; 10ms) 。 如果应用程序未指定缓冲区大小，则它将使用默认的缓冲区大小。
- 允许应用程序发现音频引擎的当前格式和周期。 这允许应用程序与音频引擎的当前设置对齐。
- 允许应用指定它希望以它指定的格式呈现/捕获，而不是由音频引擎进行任何重新采样

以上功能将在所有 Windows 设备上可用。 但是，具有足够资源和更新驱动程序的某些设备将提供比其他设备更好的用户体验。

以上功能由名为 [**IAudioClient3**](/windows/desktop/api/audioclient/nn-audioclient-iaudioclient3)的新接口提供，该接口派生自 [**IAudioClient2**](/windows/desktop/api/audioclient/nn-audioclient-iaudioclient2)。

[**IAudioClient3**](/windows/desktop/api/audioclient/nn-audioclient-iaudioclient3) 定义以下3种方法：

|方法|说明|
|--- |--- |
|GetCurrentSharedModeEnginePeriod|返回音频引擎的当前格式和周期|
|GetSharedModeEnginePeriod|返回引擎支持的指定流格式的周期范围|
|InitializeSharedAudioStream|用指定的周期初始化共享流|

GitHub 上提供的 WASAPIAudio 示例 (： <https://github.com/Microsoft/Windows-universal-samples/tree/master/Samples/WindowsAudioSession>) 演示如何使用 IAudioClient3 以降低延迟。

以下代码片段演示了音乐创建应用如何在系统支持的最低延迟设置下运行。

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

此外，建议使用 WASAPI 的应用程序也使用 [实时工作队列 API](/windows/desktop/ProcThread/platform-work-queue-api) 或 [**MFCreateMFByteStreamOnStreamEx**](/windows/desktop/api/mfidl/nf-mfidl-mfcreatemfbytestreamonstreamex) 创建工作项，并将其标记为音频或 Pro 音频，而不是其自己的线程。 这将允许操作系统以避免非音频干扰干扰的方式对其进行管理。 相反，操作系统会自动对所有 AudioGraph 线程进行自动管理。 WASAPIAudio 示例中的以下代码片段演示如何使用 MF 工作队列 Api。

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

最后，使用 WASAPI 的应用程序开发人员需要使用音频类别标记其流，并根据每个流的功能是否使用原始信号处理模式。 建议所有音频流不使用原始信号处理模式，除非理解这些含义。 Raw 模式会绕过 OEM 选择的所有信号处理，因此：

- 特定终结点的呈现信号可能是最佳的。
- 捕获信号可能采用应用程序无法理解的格式。
- 延迟可能会提高。

## <a name="driver-improvements"></a>驱动程序改进

为了使音频驱动程序支持低延迟，Windows 10 提供了以下三个新功能：

1. \[必需 \] 声明每个模式所支持的最小缓冲区大小。
2. \[可选，但建议 \] 改善驱动程序和操作系统之间数据流的协调。
3. \[可选，但建议 \] (中断、线程) 注册驱动程序资源，以便在低延迟方案中可由 OS 保护这些资源。
收件箱 HDAudio 总线驱动程序 hdaudbus.sys 枚举的 HDAudio 微型端口函数驱动程序无需注册 HDAudio 中断，因为这已通过 hdaudbus.sys 完成。 但是，如果微型端口驱动程序创建其自己的线程，则需要对其进行注册。

以下三个部分将更深入地介绍每个新功能。

### <a name="declare-the-minimum-buffer-size"></a>声明最小缓冲区大小

在操作系统、驱动程序和硬件之间移动音频数据时，驱动程序在各种约束下运行。 这些限制可能是由于物理硬件传输在内存和硬件间移动数据，以及/或者由于硬件或关联的 DSP 中的信号处理模块导致的。

在 Windows 10 中，驱动程序可以使用 DEVPKEY \_ KsAudio \_ PacketSize \_ 约束设备属性来表示其缓冲区大小功能。 此属性允许用户定义驱动程序支持的绝对最小缓冲区大小，以及每个信号处理模式的特定缓冲区大小约束 (模式特定的约束需要高于驱动程序的最小缓冲区大小，否则音频堆栈) 将忽略它们。 例如，下面的代码段演示了驱动程序如何声明支持的绝对最小缓冲区大小为1ms，但如果我们假定 48 kHz 采样速率) ，则默认模式支持128帧， (对应于3毫秒。

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

有关这些结构的详细信息，请参阅下列主题：

- [**KSAUDIO \_ PACKETSIZE \_ 约束结构**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_ksaudio_packetsize_constraints)
- [**KSAUDIO \_ PACKETSIZE \_ PROCESSINGMODE \_ 约束结构**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_ksaudio_packetsize_signalprocessingmode_constraint)

此外，sysvad 示例 (<https://github.com/Microsoft/Windows-driver-samples/tree/master/audio/sysvad>) 演示了如何使用这些属性，以便驱动程序声明每个模式的最小缓冲区。

### <a name="improve-the-coordination-between-driver-and-os"></a>改善驱动程序和操作系统之间的协调

本部分中描述的 DDIs 允许驱动程序执行以下操作：

- 明确指出了可以在 OS 中使用的缓冲区 (数据包) ，而不是根据编解码器链接位置进行 OS 推测。 这有助于操作系统更快地从音频故障中恢复。
- （可选）优化或简化传入和传出 WaveRT 缓冲区的数据传输。 此处的权益量取决于 DMA 引擎设计或 WaveRT 缓冲区与 (可能的 DSP) 硬件之间的其他数据传输机制。
- 如果驱动程序具有内部累积的捕获数据，则 "突发" 捕获的数据的速度要快于实时。 这主要用于语音激活方案，但也可在正常流式处理过程中应用。
- 提供有关其当前流位置而不是操作系统猜测的时间戳信息，这可能会允许获得极准确的位置信息。

此 DDI 对于使用 DSP 的情况非常有用。 但是，在此处列出的新 DDIs 中，标准 HD 音频驱动程序或其他简单的循环 DMA 缓冲区设计可能不会带来很多好处。

- [IMiniportWaveRTInputStream](/windows-hardware/drivers/ddi/portcls/nn-portcls-iminiportwavertinputstream)
- [IMiniportWaveRTOutputStream](/windows-hardware/drivers/ddi/portcls/nn-portcls-iminiportwavertoutputstream)

几个驱动程序例程返回 Windows 性能计数器时间戳，反映设备捕获或显示样本的时间。

在具有复杂的 DSP 管道和信号处理的设备中，计算准确的时间戳可能会很困难，应周全完成。 时间戳不应简单地反映从 OS 向 DSP 传输样本的时间。

若要计算性能计数器值，驱动程序和 DSP 可能采用以下方法之一。

- 在 DSP 内，使用某种内部的 DSP 墙壁跟踪示例时间戳。
- 在驱动程序和 DSP 之间，计算 Windows 性能计数器和 DSP 墙壁时钟之间的关联。 此过程的过程包括非常简单的 (，但不太精确) 相当复杂或 novel (但更精确的) 。
- 由于信号处理算法、管道或硬件传输而导致的任何常量延迟，除非其他情况下会考虑这些延迟。

Sysvad 示例 (<https://github.com/Microsoft/Windows-driver-samples/tree/master/audio/sysvad>) 演示了如何使用上述 DDIs。

### <a name="register-the-driver-resources"></a>注册驱动程序资源

为了帮助确保无故障操作，音频驱动程序必须将其流式处理资源注册到 portcls。 这允许操作系统管理资源，以避免音频流和其他 subystems 之间的干扰。

流资源是音频驱动程序用来处理音频流或确保音频数据流的任何资源。 目前仅支持两种类型的流资源：中断和驱动程序拥有的线程。 音频驱动程序应在创建资源后注册资源，并在删除资源之前对其进行注销。

当加载了驱动程序时，或在运行时，音频驱动程序可以在初始化时注册资源，例如，在发生 i/o 资源重新平衡的情况下。 Portcls 使用全局状态跟踪所有音频流资源。

在某些用例中，如那些需要非常低延迟音频的用例，操作系统会尝试将音频驱动程序的已注册资源与其他操作系统、应用程序和硬件活动的干扰隔离开来。 OS 和音频子系统按需执行此操作，而不与音频驱动程序交互，因为音频驱动程序的资源注册除外。

注册流资源的这一要求意味着流式处理管道路径中的所有驱动程序都必须直接或间接地向 Portcls 注册其资源。 音频微型端口驱动程序具有以下选项：

- 音频微型端口驱动程序是其堆栈的底部驱动程序， (直接) ，在这种情况下，驱动程序将知道其流资源，并可以将其注册到 Portcls。
- 音频微型端口驱动程序正在流式传输音频，并提供其他驱动程序的帮助 (例如音频总线驱动程序) 。 其他这些驱动程序还使用必须向 Portcls 注册的资源。 如果单个供应商拥有音频微型端口驱动程序用于收集此信息) 的所有驱动程序，则这些并行/总线驱动程序堆栈可以公开公共 (或专用接口。
- 音频微型端口驱动程序正在流式传输音频，并提供其他驱动程序的帮助 (例如 hdaudbus) 。 其他这些驱动程序还使用必须向 Portcls 注册的资源。 这些并行/总线驱动程序可以链接到 Portcls 并直接注册其资源。 请注意，音频微型端口驱动程序必须让 Portcls 知道它们依赖于这些其他并行/总线设备的资源 (PDOs) 。 Hd 音频基础结构使用此选项，即 hd 音频总线驱动程序与 Portcls 的链接，并自动执行以下步骤：
  - 注册其总线驱动程序的资源和
  - 通知 Portcls 子级的资源依赖于父项的资源。 在 HD 音频体系结构中，音频微型端口驱动程序只需注册其自己的驱动程序拥有的线程资源。

注意：

- 收件箱 HDAudio 总线驱动程序 hdaudbus.sys 枚举的 HDAudio 微型端口函数驱动程序无需注册 HDAudio 中断，因为这已通过 hdaudbus.sys 完成。 但是，如果微型端口驱动程序创建其自己的线程，则需要对其进行注册。
- 仅为注册流式处理资源而与 Portcls 链接的驱动程序必须更新其 Inf，使其包含/需要 wdmaudio，并) 复制 portcls.sys (和依赖文件。 在 wdmaudio 中定义了一个新的 INF 复制部分，仅复制这些文件。
- 仅在 Windows 10 中运行的音频驱动程序可以硬链接到：
  - [**PcAddStreamResource**](/windows-hardware/drivers/ddi/portcls/nf-portcls-pcaddstreamresource)
  - [**PcRemoveStreamResource**](/windows-hardware/drivers/ddi/portcls/nf-portcls-pcremovestreamresource)
- 必须在下层操作系统上运行的音频驱动程序可以使用以下接口 (微型端口可以为 IID \_ IPortClsStreamResourceManager 接口调用 QueryInterface 并仅在 PortCls 支持接口) 时才注册其资源。
  - [IPortClsStreamResourceManager](/windows-hardware/drivers/ddi/portcls/nn-portcls-iportclsstreamresourcemanager)
        -   [**AddStreamResource**](/windows-hardware/drivers/ddi/portcls/nf-portcls-iportclsstreamresourcemanager-addstreamresource)
        -   [**RemoveStreamResource**](/windows-hardware/drivers/ddi/portcls/nf-portcls-iportclsstreamresourcemanager-removestreamresource)
- 这些 DDIs，请使用此枚举和结构：
  - [**PcStreamResourceType**](/windows-hardware/drivers/ddi/portcls/ne-portcls-_pcstreamresourcetype)
  - [**PCSTREAMRESOURCE \_ 描述符**](/windows-hardware/drivers/ddi/portcls/ns-portcls-_pcstreamresource_descriptor)

最后，仅用于注册资源的 PortCls 链接的驱动程序必须将以下两行添加到其 inf 的 DDInstall 部分中。 音频微型端口驱动程序不需要此项，因为它们已在 wdmaudio 中具有包含/需求。

```inf
[<install-section-name>]
Include=wdmaudio.inf
Needs=WDMPORTCLS.CopyFilesOnly
```

上述代码行确保已安装 PortCls 及其依赖文件。

## <a name="measurement-tools"></a>度量工具

为了衡量往返延迟，用户可以利用通过扬声器播放脉冲的工具，并通过麦克风捕获它们。 它们测量以下路径的延迟：

1. 应用程序调用 render API (AudioGraph 或 WASAPI) 播放脉冲
2. 音频通过扬声器播放
3. 从麦克风捕获音频
4. 捕获 API (AudioGraph 或 WASAPI) 检测脉冲：为了衡量不同缓冲区大小的往返延迟，用户需要安装支持小缓冲区的驱动程序。 收件箱 HDAudio 驱动程序已更新为支持128样本之间的缓冲区大小 (2.66ms@48kHz) 和480示例 (10ms@48kHz) 。 以下步骤演示了如何安装收件箱 HDAudio 驱动程序 (这是所有 Windows 10 Sku) 的一部分：

- 启动“设备管理器”。
- 在 " **声音视频和游戏控制器**" 下，双击与内部扬声器相对应的设备。
- 在下一个窗口中，请切换到 " **驱动程序** " 选项卡。
- 选择 "**更新驱动**程序  - &gt; **" "浏览计算机以查找驱动程序软件"。**  - &gt; **从设备驱动程序列表中**  - &gt; **选择 "高清晰音频设备**"，然后选择 "**下一步**"。
- 如果出现标题为 "更新驱动程序警告" 的窗口，请选择 **"是**"。
- 选择 " **关闭**"。
- 如果系统要求重新启动系统，请选择 **"是"** 重新启动。
- 重新启动后，系统将使用收件箱 Microsoft HDAudio 驱动程序，而不是第三方编解码器驱动程序。 请记住以前使用的驱动程序，如果想要对音频编解码器使用最佳设置，则可以回退到该驱动程序。

![显示 wasapi 和 audiograph 之间的往返延迟与不同缓冲区大小之间的差异的关系图。 ](images/low-latency-audio-roundtrip-latency.png)

由于以下原因，WASAPI 与 AudioGraph 之间的延迟差异：

- AudioGraph 在捕获端添加一个延迟缓冲区，以便同步) 不提供的呈现和捕获 (。 此加法简化了使用 AudioGraph 编写的应用程序的代码。
- 当系统使用6ms 缓冲区时，在 AudioGraph 的呈现端有一个额外的延迟 &gt; 。
- AudioGraph 没有禁用捕获音频效果的选项

## <a name="samples"></a>示例

- WASAPI 音频示例： <https://github.com/Microsoft/Windows-universal-samples/tree/master/Samples/WindowsAudioSession>
- AudioCreation 示例 (AudioGraph) ： <https://github.com/Microsoft/Windows-universal-samples/tree/master/Samples/AudioCreation>
- Sysvad 驱动程序示例： <https://github.com/Microsoft/Windows-driver-samples/tree/master/audio/sysvad>

## <a name="faq"></a>常见问题

**1. 如果所有应用程序都使用新 Api 来实现低延迟，则不是更好？低延迟始终保证用户获得更好的用户体验吗？**

不一定。 低延迟具有其折衷：

- 低延迟意味着更高的功率消耗。 如果系统使用10ms 缓冲区，则意味着 CPU 将唤醒每个10ms，填满数据缓冲区并进入睡眠状态。 但是，如果系统使用1ms 缓冲区，则意味着 CPU 将唤醒每个1ms。 在第二种情况下，这意味着 CPU 将更频繁地唤醒，并且功率消耗将增加。 这会缩短电池寿命。
- 大多数应用程序都依靠音频效果来提供最佳用户体验。 例如，媒体播放器需要提供高保真音频。 通信应用程序需要最少的回显和干扰。 将这些类型的音频效果添加到流会增加其延迟。 与音频延迟相比，这些应用程序比音频质量更感兴趣。

总而言之，每种应用程序类型对于音频延迟有不同的需求。 如果应用程序不需要低延迟，则不应使用新的 Api 来实现低延迟。

**2. 更新到 Windows 10 的所有系统是否会自动更新为支持小型缓冲区？同时，所有系统是否支持相同的最小缓冲区大小？**

否。 为了使系统支持小型缓冲区，需要更新驱动程序。 由 Oem 决定将更新哪些系统以支持小型缓冲区。 另外，较新的系统更 likey 支持比较早的系统更小的缓冲区 (例如，新系统中的延迟很可能低于旧系统) 。

**3. 如果驱动程序支持小缓冲区大小 (&lt; 10ms buffer) ，Windows 10 中的所有应用程序是否会自动使用小型缓冲区来呈现和捕获音频？**

否。 默认情况下，Windows 10 中的所有应用程序都将使用10ms 的缓冲区来呈现和捕获音频。 如果应用程序需要使用小型缓冲区，则需要使用新的 AudioGraph 设置或 WASAPI IAudioClient3 接口，以便执行此操作。 但是，如果 Windows 10 中的一个应用程序请求使用小型缓冲区，则音频引擎将使用该特定缓冲区大小开始传输音频。 在这种情况下，使用同一终结点和模式的所有应用程序都将自动切换到该小型缓冲区大小。 当低延迟应用程序退出时，音频引擎将再次切换到10ms 缓冲区。