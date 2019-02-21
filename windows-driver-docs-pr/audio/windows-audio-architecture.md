---
title: Windows 音频体系结构
description: 本主题提供 Windows 10 音频体系结构的高级别摘要。
ms.assetid: 1FC95504-18AA-4F3B-8E96-005276699694
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 78b2b241feb5c90811a787e2d38b355764795172
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56546368"
---
# <a name="windows-audio-architecture"></a>Windows 音频体系结构


本主题提供 Windows 10 音频体系结构的高级别摘要。

## <a name="span-idwindows10audiostackdiagramspanspan-idwindows10audiostackdiagramspanspan-idwindows10audiostackdiagramspanwindows-10-audio-stack-diagram"></a><span id="Windows_10_Audio_Stack_Diagram"></span><span id="windows_10_audio_stack_diagram"></span><span id="WINDOWS_10_AUDIO_STACK_DIAGRAM"></span>Windows 10 的音频堆栈关系图


此图提供了 Windows 10 音频堆栈的主要元素的摘要。

![显示应用程序、 音频引擎、 驱动程序和硬件的 windows 10 音频堆栈关系图 ](images/audio-windows-10-stack-diagram.png)

## <a name="span-idapisspanspan-idapisspanspan-idapisspanapis"></a><span id="APIs"></span><span id="apis"></span><span id="APIS"></span>Api


**最高级别 Api**

最高级别 Api 用于应用程序开发。 这些 Api 中当前正在使用和支持。

-   XAML [MediaElement 类](https://msdn.microsoft.com/library/windows/apps/windows.ui.xaml.controls.mediaelement)(C#，VB、 c + +)
-   HTML[音频对象](https://msdn.microsoft.com/library/windows/apps/hh767373.aspx)并[视频对象](https://msdn.microsoft.com/library/windows/apps/hh767390.aspx)&lt;标记&gt;（由网站和 Windows Web 应用）
-   [Windows.Media.Capture 命名空间](https://msdn.microsoft.com/library/windows/apps/xaml/windows.media.capture)(C#，VB、 c + +)
-   [Microsoft Media Foundation](https://msdn.microsoft.com/library/windows/desktop/ms694197) （c + +）

这些较旧的 Api 已弃用。

-   [DirectShow](https://msdn.microsoft.com/library/windows/desktop/dd375454)
-   [DirectSound](https://msdn.microsoft.com/library/ee416960.aspx)
-   [PlaySound](https://msdn.microsoft.com/library/dd743680)
-   [Windows.Media.MediaControlContract](https://msdn.microsoft.com/library/windows/apps/dn706169)

**低级别 Api**

对于音频流，建议这些低级别 Api。

-   [Wasapi 就可以了](https://msdn.microsoft.com/library/windows/desktop/dd371455)（高性能，但更复杂）
-   [IXAudio2](https://msdn.microsoft.com/library/windows/desktop/ee415908) （通常用于游戏）
-   [MIDI](https://msdn.microsoft.com/library/windows/desktop/dd742875)

对于枚举建议使用此较低级别 API。

-   [Windows.Devices.Enumeration](https://msdn.microsoft.com/library/windows/apps/br225459)

这些 Api 不建议用于 Windows 应用程序中。

-   [有关 MMDevice API](https://msdn.microsoft.com/library/windows/desktop/dd316556) （替换 Windows.Devices.Enumeration）
-   [DeviceTopology API](https://msdn.microsoft.com/library/windows/desktop/dd370809)
-   [EndpointVolume API](https://msdn.microsoft.com/library/windows/desktop/dd370832)

## <a name="span-idaudioenginespanspan-idaudioenginespanspan-idaudioenginespanaudio-engine"></a><span id="Audio_Engine"></span><span id="audio_engine"></span><span id="AUDIO_ENGINE"></span>音频引擎


音频引擎包含两个相关组件，音频设备图形 (audiodg.exe)，这将加载音频引擎 (audioeng.dll)。

音频引擎：

-   混合使用和处理音频流。 有关音频引擎如何使用缓冲区传输音频的详细信息，请参阅[了解 WaveRT 端口驱动程序](understanding-the-wavert-port-driver.md)。
-   加载音频处理对象 (Apo)，后者是处理音频信号的特定于 H/W 的插件。 A p o s 有关详细信息，请参阅[Windows 音频处理对象](windows-audio-processing-objects.md)。

## <a name="span-idaudioserviceaudiosrvdllspanspan-idaudioserviceaudiosrvdllspanaudio-service-audiosrvdll"></a><span id="audio_service__audiosrv.dll_"></span><span id="AUDIO_SERVICE__AUDIOSRV.DLL_"></span>音频服务 (audiosrv.dll)


音频服务：

-   用于设置和控制音频流。
-   实现 Windows 策略的背景音频播放，放掉，等等。

## <a name="span-idaudioendpointbuilderaudioendpointbuilderexespanspan-idaudioendpointbuilderaudioendpointbuilderexespanaudio-endpoint-builder-audioendpointbuilderexe"></a><span id="audio_endpoint_builder__audioendpointbuilder.exe_"></span><span id="AUDIO_ENDPOINT_BUILDER__AUDIOENDPOINTBUILDER.EXE_"></span>音频的终结点生成器 (audioendpointbuilder.exe)


音频的终结点生成器 (audioendpointbuilder.exe):

-   用于发现新的音频设备和创建软件音频终结点。 有关使用的算法的详细信息，请参阅[音频终结点生成器算法](audio-endpoint-builder-algorithm.md)。

## <a name="span-idaudiodriversspanspan-idaudiodriversspanspan-idaudiodriversspanaudio-drivers"></a><span id="Audio_Drivers"></span><span id="audio_drivers"></span><span id="AUDIO_DRIVERS"></span>音频驱动程序


音频驱动程序：

-   遵循端口微型端口模型。 有关详细信息，请参阅[WDM 音频术语](wdm-audio-terminology.md)并[开发 WaveRT 微型端口驱动程序](developing-a-wavert-miniport-driver.md)。
-   允许音频堆栈来呈现和捕获音频从多个音频设备，包括： 集成的扬声器和麦克风、 耳机/耳机，USB 设备、 蓝牙设备、 HDMI，等等。
-   端口微型端口模型对应于 ALSA 高级的 Linux 声音体系结构
-   有关驱动程序的示例代码的信息，请参阅[示例音频驱动程序](sample-audio-drivers.md)。

## <a name="span-idhardwarespanspan-idhardwarespanspan-idhardwarespanhardware"></a><span id="Hardware"></span><span id="hardware"></span><span id="HARDWARE"></span>Hardware


在任何给定设备存在的音频硬件而异，但可以包括：

-   音频编解码器
-   DSP （可选）
-   集成的扬声器、 麦克风等等
-   外部设备：USB 音频设备、 音频的蓝牙设备、 HDMI 音频等。
-   此外可以在硬件 （例如编解码器或 DSP），而不是或者也不实现信号处理。








