---
title: MIDI 和 DirectMusic 组件
description: MIDI 和 DirectMusic 组件
ms.assetid: 6334f332-31ba-4daf-aad1-94bb65d25153
keywords:
- WDM 音频组件 WDK
- 用户模式组件 WDK 音频
- 内核模式组件 WDK 音频
- 捕获组件 WDK 音频
- MIDI 组件 WDK 音频
- DirectMusic WDK 音频，组件
- 播放 WDK 音频
- 带有时间戳 MIDI WDK 音频
- 请注意在事件 WDK 音频
- 请注意关闭事件 WDK 音频
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d12949b12e9eff3eb0478749773094e8749833b6
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56520984"
---
# <a name="midi-and-directmusic-components"></a>MIDI 和 DirectMusic 组件


## <span id="midi_and_directmusic_components"></span><span id="MIDI_AND_DIRECTMUSIC_COMPONENTS"></span>


应用程序的程序依赖于用户和内核模式组件，可捕获和播放 MIDI 和 DirectMusic 流的组合。

应用程序可以使用以下对象之一的 MIDI 播放和捕获的软件接口：

-   Microsoft Windows 多媒体 **midiOut * * * Xxx*和 **midiIn * * * Xxx*函数

-   DirectMusic API

行为 **midiOut * * * Xxx*和 **midiIn * * * Xxx*函数基于旧 MIDI 驱动程序和设备的功能。 从 Windows 98 [WDMAud 系统驱动程序](user-mode-wdm-audio-components.md#wdmaud_system_driver)对这些函数的调用转换为与 WDM 音频驱动程序的命令。 但是，通过模拟行为的较旧版本软件和硬件，**midiOut * * * Xxx*和 **midiIn * * * Xxx*精度计时和增强的功能，现已可用，否则会影响函数通过 DirectMusic API。 有关 DirectMusic 和 Windows 多媒体 MIDI 函数的详细信息，请参阅 Microsoft Windows SDK 文档。

DirectMusic 和 Windows 多媒体 MIDI 函数都的客户端[SysAudio 系统驱动程序](kernel-mode-wdm-audio-components.md#sysaudio_system_driver)，哪些生成处理 MIDI 和 DirectMusic 流音频筛选器关系图。 图形构建是透明的使用这些软件接口的应用程序。

### <a name="span-idmidicomponentsspanspan-idmidicomponentsspanspan-idmidicomponentsspanmidi-components"></a><span id="MIDI_Components"></span><span id="midi_components"></span><span id="MIDI_COMPONENTS"></span>MIDI 组件

下图显示了用户模式和内核模式组件 MIDI 应用程序使用到*播放*MIDI 数据。 WDM 音频驱动程序通过将此应用程序接口 **midiOut * * * Xxx*中实现的函数[WinMM 系统组件](user-mode-wdm-audio-components.md#winmm_system_component)，Winmm.dll。

![显示了 midi 播放组件的关系图](images/midiplay.png)

在上图中的 MIDI 应用程序从一个 MIDI 文件中读取加盖时间戳 MIDI 事件并播放它们。 MIDI 和 Dmu 微型端口驱动程序显示为变暗的框，以指示它们可以是供应商提供的组件。 如果适用，供应商可能选择使用一个系统提供的微型端口驱动程序-FMSynth、 UART 或 DMusUART-而不是编写自定义的微型端口驱动程序。 所有图中的其他组件都是系统提供。

典型的 MIDI 播放应用程序调用的主循环**timeSetEvent**计划下一步请注意打开或注意关闭事件。 此调用将作为其参数之一的函数指针传递到应用程序的回调例程。 当事件发生，并且操作系统将调用回调例程时，此例程会调用**midiOutShortMsg**打开或关闭一个或多个计划的说明。 **MidiOutShortMsg**函数将 MIDI 消息存储在页锁定数据缓冲区以无需页-在内存中的调用期间。 有关详细信息**timeSetEvent**并**midiOutShortMsg**调用，请参阅 Microsoft Windows SDK 文档。

WDMAud，其中包含这两个用户和内核模式组件 （Wdmaud.drv 和 Wdmaud.sys），记录原始 MIDI 从消息的时间**midiOutShortMsg**调用到达。 与 MIDI 消息生成 MIDI 流，它将发送到一个 WDMAud 下方显示在图中的内核模式组件进行 WDMAud 组合这些时间戳。

在生成 MIDI 应用程序的音频筛选器关系图，SysAudio 将选择三个可能的连接-SWMidi、 MIDI 端口或 Dmu 端口驱动程序，到在上图中显示的之一。 如果应用程序选择默认 MIDI 设备，SysAudio 首先查找合成器的设备的 MIDI 或 Dmu 微型端口驱动程序具有 MIDI pin。 如果在注册表中不找到任何此类设备，将改为使用 SysAudio [SWMidi 系统驱动程序](kernel-mode-wdm-audio-components.md#swmidi_system_driver)(Swmidi.sys)。 SWMidi 是在软件中，实现波表合成一个 KS 筛选器，这需要唯一的设备可以呈现波形音频流。

SWMidi 混合使用所有在一起以产生单个批 PCM 流，它将输出到其语音[KMixer 系统驱动程序](kernel-mode-wdm-audio-components.md#kmixer_system_driver)。 KMixer，反过来，将 PCM 格式的批流传递到 WaveCyclic 或 WavePci 设备，其端口和微型端口驱动程序出现在该图在左下角。 或者，KMixer 可以到 USB 音频设备控制的传递的输出流[USBAudio 类系统驱动程序](kernel-mode-wdm-audio-components.md#usbaudio_class_system_driver)（不在图中所示）。

上图中，在 MIDI 端口驱动程序从 WDMAud 所需的时间戳 MIDI 流，并将其转换为原始 MIDI 消息，这将通过合成器设备播放 MIDI 微型端口驱动程序。 MIDI 端口驱动程序包含 sequencer，后者在软件中实现的并且可以计划为一毫秒的计时器分辨率与原始的 MIDI 消息。

Dmu 端口驱动程序就能够实现比 MIDI 端口驱动程序的高得多的时间精度，如果合成器设备包含硬件 sequencer。 在这种情况下，Dmu 微型端口驱动程序应指定足够大，吸收导致的争用情况的 CPU 时间与 Isr （中断服务例程） 和其他高优先级操作抖动的硬件缓冲区。 Dmu 端口驱动程序将输出到微型端口驱动程序在 MIDI 流中的时间戳是以 100 毫微秒分辨率的 64 位值。

如果 DMusic 合成器没有硬件 sequencer，则它必须依赖于 Dmu 端口驱动程序软件 sequencer，这与在 MIDI 端口驱动程序，有一毫秒的计时器分辨率。

适配器驱动程序通过调用创建 MIDI 或 Dmu 端口驱动程序[ **PcNewPort** ](https://msdn.microsoft.com/library/windows/hardware/ff537715) GUID 值为**CLSID\_PortMidi**或**CLSID\_PortDMus**分别。 在 Windows XP 及更高版本，MIDI 和 Dmu 端口驱动程序将共享相同的软件实现。

在上图中的底部显示是 FMSynth、 UART 和 DMusUART，它包括在 Portcls.sys 的系统提供的微型端口驱动程序的名称。 适配器驱动程序创建一个微型端口驱动程序通过调用[ **PcNewMiniport**](https://msdn.microsoft.com/library/windows/hardware/ff537714)。 FMSynth 和 UART 提供[IMiniportMidi](https://msdn.microsoft.com/library/windows/hardware/ff536703)接口和 DMusUART 提供[IMiniportDMus](https://msdn.microsoft.com/library/windows/hardware/ff536699)接口。 请注意 UART （在 Windows 98 金色） 现已过时，仅支持现有的驱动程序。 新适配器驱动程序应改用 DMusUART （在 Windows 98 SE 和更高版本，并在 Windows 2000 及更高版本），它实现的 UART 的功能超集。 DMusUART 是支持 DLS 下载也硬件序列化不支持的 Dmu 微型端口驱动程序的示例。 FMSynth 和 DMusUART 微型端口驱动程序的源代码现已推出的示例音频驱动程序 Windows Driver Kit (WDK) 中。

下图显示了用户模式和内核模式组件 MIDI 应用程序使用到*捕获*MIDI 数据。 WDM 音频驱动程序通过将此应用程序接口 **midiIn * * * Xxx*函数。

![说明 midi 捕获组件的关系图](images/midicapt.png)

在上图中，MIDI 和 Dmu 微型端口驱动程序将显示为变暗的框以指示它们可以是供应商提供的组件。 如果适用，供应商可能会改为选择使用系统提供的微型端口驱动程序，UART 或 DMusUARTCapture 之一。 所有图中的其他组件都是系统提供。

MIDI 数据源通常是 MPU 401 设备。 通过调用**PcNewMiniport**，适配器驱动程序可以创建一个系统提供的微型端口驱动程序，UART 或 DMusUARTCapture，用来捕获 MIDI MPU 401 设备中的数据。 同样，UART 已过时，并且新的驱动程序应改用 DMusUARTCapture （在 Windows 98 SE 和更高版本，并在 Windows 2000 及更高版本）。

每次发生 MIDI 注意打开或注意关闭事件时，包含 MIDI 或 DMusic 捕获微型端口驱动程序 （在上图中底部） 将其添加到流向 MIDI 或 Dmu 端口驱动程序的 MIDI 流之前将时间戳添加到 MIDI 消息。

MIDI 或 DMusic 捕获端口驱动程序输出带时间戳的 MIDI 流 Wdmaud.sys，内核模式到一半 WDMAud 系统驱动程序。 用户模式下一半，Wdmaud.drv 输出带时间戳 MIDI 流式传输到应用程序通过 **midiIn * * * Xxx*函数，这在 Winmm.dll 中实现。

在图顶部的 MIDI 应用程序将加盖时间戳 MIDI 事件写入一个 MIDI 文件中。 在应用程序调用的时间**midiInOpen**若要打开的 MIDI 输入的流，它会传入函数指针到其回调例程。 请注意打开或注意关闭事件发生时，操作系统将调用回调例程与包含一个或多个具有时间戳的 MIDI 消息的数据块。 这些消息的时间戳是实质上是相同的与最初生成 MIDI 或 Dmu 微型端口驱动程序。

### <a name="span-iddirectmusiccomponentsspanspan-iddirectmusiccomponentsspanspan-iddirectmusiccomponentsspandirectmusic-components"></a><span id="DirectMusic_Components"></span><span id="directmusic_components"></span><span id="DIRECTMUSIC_COMPONENTS"></span>DirectMusic 组件

下图显示了通过到 DirectMusic 应用程序使用的用户和内核模式组件*播放*或*捕获*MIDI 数据。

![说明 directmusic 播放和捕获组件的关系图](images/dmusplay.png)

在上图中的左半部分显示了播放的组件和捕获组件显示在右侧。 Dmu 微型端口驱动程序显示为变暗的框，以指示它们可以是供应商提供的组件。 如果适用，供应商可以改为使用系统提供的微型端口驱动程序，DMusUART 或 DMusUARTCapture 之一。 在图中的其他组件是系统提供。

DirectMusic 应用程序中的图左上角，将定向加盖时间戳 MIDI 流文件中的为用户模式[DirectMusic 系统组件](user-mode-wdm-audio-components.md#directmusic_system_component)(DMusic.dll)，这反过来将定向到 Dmu 端口驱动程序的流。 此驱动程序可以绑定到 DirectMusic 合成器或 MPU 401 设备的微型端口驱动程序，如果有可用。 或者，可将端口驱动程序绑定到[DMusic 系统驱动程序](kernel-mode-wdm-audio-components.md#dmusic_system_driver)(Dmusic.sys)，这是一个系统提供 Dmu 微型端口驱动程序，在软件中，实现 DLS 能够波表合成器，并仅需要设备，可以呈现波形音频流。

如 SWMidi，DMusic 驱动程序，Dmusic.sys，混合使用所有在一起以产生单个 PCM 格式的批流，它将输出到 KMixer 其语音。 KMixer，反过来，可以将传递批流到波形设备时，其端口和微型端口驱动程序出现在该图在左下角处，或受 USBAudio 系统驱动程序，它未显示在图中的 USB 音频设备。

DirectMusic 捕获组件显示在上图中的右半部分。 图右下角中的 DMusic 捕获微型端口驱动程序控制它记录每个 MIDI 消息捕获硬件和时间戳。 Dmu 端口驱动程序将定向到用户模式下 DirectMusic 组件 DMusic.dll 加盖时间戳 MIDI 流。 应用程序通过 DirectMusic API 来访问此流，并将时间戳 MIDI 数据写入到文件。

适配器驱动程序可以使用系统提供 DMusUARTCapture 微型端口驱动程序来控制 MPU 401 捕获设备。 适配器驱动程序通过调用创建此微型端口驱动程序**PcNewMiniport**使用的 GUID 值**CLSID\_DMusUARTCapture**。 生成的微型端口驱动程序对象支持**IMiniportDMus**接口。 DMusUARTCapture 微型端口驱动程序的源代码现已推出的示例音频驱动程序 Windows Driver Kit (WDK) 中。

DirectMusic 应用程序还可以通过运行 **midiOut * * * Xxx*如 SWMidi (Swmidi.sys); 如果它为选择的设备。 为简单起见上, 图中省略了此路径。 DMusic 驱动程序 (Dmusic.sys) 需要才能正确运行; 的初始 DLS 下载使用 SWMidi 可避免这一要求。

 

 




