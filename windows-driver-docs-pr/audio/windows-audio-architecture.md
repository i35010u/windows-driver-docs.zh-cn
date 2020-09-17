---
title: Windows 音频体系结构
description: 本主题提供了 Windows 10 音频体系结构的高级摘要。
ms.assetid: 1FC95504-18AA-4F3B-8E96-005276699694
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4b375b292c4a281c443d58b2d0686884d83c7f96
ms.sourcegitcommit: b84d760d4b45795be12e625db1d5a4167dc2c9ee
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/17/2020
ms.locfileid: "90716628"
---
# <a name="windows-audio-architecture"></a>Windows 音频体系结构


本主题提供了 Windows 10 音频体系结构的高级摘要。

## <a name="span-idwindows_10_audio_stack_diagramspanspan-idwindows_10_audio_stack_diagramspanspan-idwindows_10_audio_stack_diagramspanwindows-10-audio-stack-diagram"></a><span id="Windows_10_Audio_Stack_Diagram"></span><span id="windows_10_audio_stack_diagram"></span><span id="WINDOWS_10_AUDIO_STACK_DIAGRAM"></span>Windows 10 音频堆栈关系图


此图提供 Windows 10 音频堆栈的主要元素的摘要。

![显示应用、音频引擎、驱动程序和硬件的 windows 10 音频堆栈关系图 ](images/audio-windows-10-stack-diagram.png)

## <a name="span-idapisspanspan-idapisspanspan-idapisspanapis"></a><span id="APIs"></span><span id="apis"></span><span id="APIS"></span>Api


**顶级 Api**

顶级 Api 用于开发应用程序。 目前正在使用和支持这些 Api。

-   XAML [MediaElement 类](/uwp/api/Windows.UI.Xaml.Controls.MediaElement) (c #、VB、c + +) 
-   HTML[音频对象](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/audio)和[视频对象](https://developer.mozilla.org/en-US/docs/Web/API/HTMLVideoElement) &lt; 标记 &gt; (由网站和 Windows Web Apps 使用) 
-    (c #、VB、c + +) 的[Windows Media. 捕获命名空间](/uwp/api/Windows.Media.Capture)
-    (c + + [Microsoft 媒体基础](/windows/desktop/medfound/microsoft-media-foundation-sdk)) 

这些较旧的 Api 已弃用。

-   [DirectShow](/windows/desktop/DirectShow/directshow)
-   [DirectSound](/previous-versions/windows/desktop/ee416960(v=vs.85))
-   [PlaySound](/previous-versions/dd743680(v=vs.85))
-   [MediaControlContract](/uwp/extension-sdks/windows-desktop-extension-sdk)

**低级别 Api**

建议将这些较低级别的 Api 用于音频流式处理。

-   [WASAPI](/windows/desktop/CoreAudio/wasapi) (高性能，但更复杂) 
-   [IXAudio2](/windows/win32/api/xaudio2/nn-xaudio2-ixaudio2) (通常用于游戏) 
-   [MIDI](/windows/desktop/Multimedia/about-midi)

建议将此低级别 API 用于枚举。

-   [Windows.Devices.Enumeration](/uwp/api/Windows.Devices.Enumeration)

对于 Windows 应用程序，不建议使用这些 Api。

-   [关于 MMDEVICE API](/windows/desktop/CoreAudio/mmdevice-api) (替换为 Windows.) 
-   [DeviceTopology API](/windows/desktop/CoreAudio/devicetopology-api)
-   [EndpointVolume API](/windows/desktop/CoreAudio/endpointvolume-api)

## <a name="span-idaudio_enginespanspan-idaudio_enginespanspan-idaudio_enginespanaudio-engine"></a><span id="Audio_Engine"></span><span id="audio_engine"></span><span id="AUDIO_ENGINE"></span>音频引擎


音频引擎包括两个相关组件：音频设备图形 ( # A0) ，它可加载音频引擎 ( # A1) 。

音频引擎：

-   混合和处理音频流。 有关音频引擎如何使用缓冲区传输音频的详细信息，请参阅 [了解 WaveRT 端口驱动程序](understanding-the-wavert-port-driver.md)。
-   加载 (为) 的音频处理对象，这些对象是用于处理音频信号的 H/W 特定插件。 有关的详细信息，请参阅 [Windows 音频处理对象](windows-audio-processing-objects.md)。

## <a name="span-idaudio_service__audiosrvdll_spanspan-idaudio_service__audiosrvdll_spanaudio-service-audiosrvdll"></a><span id="audio_service__audiosrv.dll_"></span><span id="AUDIO_SERVICE__AUDIOSRV.DLL_"></span>音频服务 ( # A0) 


音频服务：

-   用于设置和控制音频流。
-   实现适用于后台音频播放、放掉等的 Windows 策略。

## <a name="span-idaudio_endpoint_builder__audioendpointbuilderexe_spanspan-idaudio_endpoint_builder__audioendpointbuilderexe_spanaudio-endpoint-builder-audioendpointbuilderexe"></a><span id="audio_endpoint_builder__audioendpointbuilder.exe_"></span><span id="AUDIO_ENDPOINT_BUILDER__AUDIOENDPOINTBUILDER.EXE_"></span>音频终结点生成器 ( # A0) 


音频终结点生成器 ( # A0) ：

-   用于发现新的音频设备和创建软件音频终结点。 有关所使用的算法的详细信息，请参阅 [音频终结点生成器算法](audio-endpoint-builder-algorithm.md)。

## <a name="span-idaudio_driversspanspan-idaudio_driversspanspan-idaudio_driversspanaudio-drivers"></a><span id="Audio_Drivers"></span><span id="audio_drivers"></span><span id="AUDIO_DRIVERS"></span>音频驱动程序


音频驱动程序：

-   遵循端口-微型端口模型。 有关详细信息，请参阅 [WDM 音频术语](wdm-audio-terminology.md) 和 [开发 WaveRT 微型端口驱动程序](developing-a-wavert-miniport-driver.md)。
-   允许音频堆栈呈现并捕获几个音频设备的音频，其中包括：集成扬声器和麦克风、耳机/耳机、USB 设备、Bluetooth 设备、HDMI，等等。
-   Minport 模型对应于高级 Linux 音频体系结构 ALSA
-   有关示例驱动程序代码的信息，请参阅 [示例音频驱动程序](sample-audio-drivers.md)。

## <a name="span-idhardwarespanspan-idhardwarespanspan-idhardwarespanhardware"></a><span id="Hardware"></span><span id="hardware"></span><span id="HARDWARE"></span>软


任何设备上出现的音频硬件有所不同，但可能包括：

-   音频编解码器
-   DSP (可选) 
-   集成扬声器、麦克风等
-   外部设备： USB 音频设备、蓝牙音频设备、HDMI 音频等。
-   也可以在 H/W (（例如编解码器或 DSP) ，而不是在中实现信号处理。