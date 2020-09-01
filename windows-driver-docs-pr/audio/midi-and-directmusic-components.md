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
- 带有时间戳的 MIDI WDK 音频
- 便笺-事件 WDK 音频
- 便笺-关闭事件 WDK 音频
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 552aa9b54920201a2fad20214670c608d1e91551
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89211429"
---
# <a name="midi-and-directmusic-components"></a>MIDI 和 DirectMusic 组件


## <span id="midi_and_directmusic_components"></span><span id="MIDI_AND_DIRECTMUSIC_COMPONENTS"></span>


应用程序依赖于用户和内核模式组件的组合来捕获和播放 MIDI 和 DirectMusic 流。

应用程序可以使用以下任一软件接口进行 MIDI 播放和捕获：

-   Microsoft Windows 彩信 **midiOut * * * xxx* And **midiIn * ** *

-   DirectMusic API

**MidiOut * * * xxx* 和 **MidiIn * * xxx* 函数的行为基于旧版 MIDI 驱动程序和设备的功能。 从 Windows 98 开始， [WDMAud 系统驱动程序](user-mode-wdm-audio-components.md#wdmaud_system_driver) 将对这些函数的调用转换为 WDM 音频驱动程序的命令。 但是，通过模拟旧软件和硬件的行为，**midiOut * * * xxx* 和 **MidiIn * * xxx* 函数将牺牲通过 DirectMusic API 提供的准确性计时和增强的功能。 有关 DirectMusic 和 Windows 多媒体 MIDI 功能的详细信息，请参阅 Microsoft Windows SDK 文档。

DirectMusic 和 Windows 多媒体 MIDI 函数是 [SysAudio 系统驱动程序](kernel-mode-wdm-audio-components.md#sysaudio_system_driver)的客户端，它可生成用于处理 MIDI 和 DirectMusic 流的音频筛选器图形。 图形构建对于使用这些软件接口的应用程序而言是透明的。

### <a name="span-idmidi_componentsspanspan-idmidi_componentsspanspan-idmidi_componentsspanmidi-components"></a><span id="MIDI_Components"></span><span id="midi_components"></span><span id="MIDI_COMPONENTS"></span>MIDI 组件

下图显示了 MIDI 应用程序用于 *播放* midi 数据的用户模式和内核模式组件。 此应用程序通过 **midiOut * * Xxx* 函数（在 [winmm.dll 系统组件](user-mode-wdm-audio-components.md#winmm_system_component)Winmm.dll 中实现）向 WDM 音频驱动程序进行接口。

![显示 midi 播放组件的关系图](images/midiplay.png)

上图中的 MIDI 应用程序从 MIDI 文件中读取带有时间戳的 MIDI 事件，并播放它们。 MIDI 和 Dmu 微型端口驱动程序显示为暗盒，指示它们可以是供应商提供的组件。 如果需要，供应商可能选择使用系统提供的一个或多个微端口驱动程序--FMSynth、UART 或 DMusUART--而不是编写自定义微型端口驱动程序。 该图中的所有其他组件都是系统提供的。

典型的 MIDI 播放应用程序的主要循环会调用 **timeSetEvent** 来计划下一个便笺或附注关闭事件。 此调用会将函数指针用作应用程序的回调例程，作为其参数之一。 当发生事件并且操作系统调用回调例程时，此例程将调用 **midiOutShortMsg** 来打开或关闭一个或多个计划的便笺。 **MidiOutShortMsg**函数将 MIDI 消息存储在页面锁定的数据缓冲区中，以便在调用期间不需要在此内存中分页。 有关 **timeSetEvent** 和 **midiOutShortMsg** 调用的详细信息，请参阅 Microsoft Windows SDK 文档。

WDMAud 包括用户和内核模式组件 (winspool.drv 和 Wdmaud.sys) ，记录来自 **midiOutShortMsg** 调用的原始 MIDI 消息到达的时间。 WDMAud 将这些时间戳与 MIDI 消息组合在一起，以生成其发送到图中 WDMAud 下的某个内核模式组件的 MIDI 流。

为 MIDI 应用程序生成音频筛选器图时，SysAudio 只会选择上图中显示的三个可能的连接中的一种：--SWMidi、MIDI 端口或 Dmu 端口驱动程序。 如果应用程序选择默认的 MIDI 设备，SysAudio 将首先查找其 MIDI 或 Dmu 微型端口驱动程序具有 MIDI pin 的合成器设备。 如果在注册表中找不到此类设备，SysAudio 将改用 [SWMidi 系统驱动程序](kernel-mode-wdm-audio-components.md#swmidi_system_driver) ( # A0) 。 SWMidi 是在软件中实现 wavetable 合成器的 KS 筛选器，它只需要可呈现 wave 音频流的设备。

SWMidi 将其所有声音组合在一起，生成一个波形 PCM 流，并将其输出到 [KMixer 系统驱动程序](kernel-mode-wdm-audio-components.md#kmixer_system_driver)。 然后，KMixer 会将一个 PCM 格式的波形流传递到 WaveCyclic 或 WavePci 设备，该设备的端口和微型端口驱动程序显示在图的左下角。 或者，KMixer 可以将其输出流传递到由 [USBAudio 类系统驱动程序](kernel-mode-wdm-audio-components.md#usbaudio_class_system_driver) 控制的 USB 音频设备， (图) 中未显示。

在上图中，MIDI 端口驱动程序从 WDMAud 中取出带有时间戳的 MIDI 流，并将其转换为可通过合成器设备播放的原始 MIDI 消息。 MIDI 端口驱动程序包含一个 sequencer，该 sequencer 在软件中实现，并且能够计划使用一毫秒的计时器分辨率的原始 MIDI 消息。

如果合成器设备包含硬件 sequencer，则 Dmu 端口驱动程序能够实现比 MIDI 端口驱动程序更高的计时准确性。 在这种情况下，Dmu 微型端口驱动程序应指定一个足以满足 CPU 时间争用的硬件缓冲区，并使用 Isr (中断服务例程) 和其他高优先级操作。 MIDI 流中的时间戳，Dmu 端口驱动程序输出到微型端口驱动程序的时间戳为64位值，分辨率为100毫微秒。

如果 DMusic 合成没有硬件 sequencer，它必须依赖于 Dmu 端口驱动程序的软件 sequencer，如 MIDI 端口驱动程序的，计时器分辨率为1毫秒。

适配器驱动程序通过分别调用 GUID 值为**CLSID \_ PortMidi**或**clsid \_ PortDMus**的[**PcNewPort**](/windows-hardware/drivers/ddi/portcls/nf-portcls-pcnewport) ，创建一个 MIDI 或 dmu 端口驱动程序。 在 Windows XP 和更高版本中，MIDI 和 Dmu 端口驱动程序共享相同的软件实现。

如上图所示，是系统提供的微型端口驱动程序的名称 FMSynth、UART 和 DMusUART，它们包含在 Portcls.sys 中。 适配器驱动程序通过调用 [**PcNewMiniport**](/windows-hardware/drivers/ddi/portcls/nf-portcls-pcnewminiport)创建其中一个小型端口驱动程序。 FMSynth 和 UART 提供 [IMiniportMidi](/windows-hardware/drivers/ddi/portcls/nn-portcls-iminiportmidi) 接口，DMusUART 提供 [IMiniportDMus](/windows-hardware/drivers/ddi/dmusicks/nn-dmusicks-iminiportdmus) 接口。 请注意，在 Windows 98 黄金) 后，UART 现在已过时 (，仅对现有驱动程序支持。 新的适配器驱动程序应改为使用 Windows 98 SE 和更高版本中的 DMusUART (，以及在 Windows 2000 和更高版本中) ，它实现了 UART 功能的超集。 DMusUART 是 Dmu 微型端口驱动程序的一个示例，该驱动程序不支持 DL 下载和硬件排序。 Windows 驱动程序工具包 (WDK) 的示例音频驱动程序中提供了 FMSynth 和 DMusUART 微型端口驱动程序的源代码。

下图显示了 MIDI 应用程序用来 *捕获* MIDI 数据的用户模式和内核模式组件。 此应用程序通过 **midiIn * * Xxx* 函数向 WDM 音频驱动程序接口。

![说明 midi 捕获组件的示意图](images/midicapt.png)

在上图中，MIDI 和 Dmu 微型端口驱动程序显示为暗盒，指示它们可以是供应商提供的组件。 如果需要，供应商可以改为选择使用系统提供的微型端口驱动程序（UART 或 DMusUARTCapture）之一。 该图中的所有其他组件都是系统提供的。

MIDI 数据的源通常是 MPU-401 设备。 通过调用 **PcNewMiniport**，适配器驱动程序可以创建一个系统提供的微型端口驱动程序（UART 或 DMusUARTCapture），以从 MPU-401 设备捕获 MIDI 数据。 同样，UART 过时，新驱动程序应使用 DMusUARTCapture (在 Windows 98 SE 和更高版本中，以及在 Windows 2000 和更高版本中) 。

每次发生 MIDI 便笺或附注关闭事件时，上图 (的 MIDI 或 DMusic 捕获微型端口驱动程序) 将时间戳添加到 MIDI 消息，然后再将其添加到流向 MIDI 或 Dmu 端口驱动程序的 MIDI 流中。

MIDI 或 DMusic 捕获端口驱动程序将带时间戳的 MIDI 流输出到 Wdmaud.sys （WDMAud 系统驱动程序的内核模式）。 用户模式半 Wdmaud，winspool.drv，通过 Winmm.dll 中实现的 **midiIn * * Xxx* 函数将带时间戳的 MIDI 流输出到应用程序。

该图顶部的 MIDI 应用程序将带有时间戳的 MIDI 事件写入 MIDI 文件。 当应用程序调用 **midiInOpen** 打开 MIDI 输入流时，它会将函数指针传递到其回调例程。 当发生便笺或附注事件时，操作系统将调用带有包含一个或多个带时间戳的 MIDI 消息的数据块的回调例程。 这些消息的时间戳实质上与 MIDI 或 Dmu 微型端口驱动程序最初生成的时间戳相同。

### <a name="span-iddirectmusic_componentsspanspan-iddirectmusic_componentsspanspan-iddirectmusic_componentsspandirectmusic-components"></a><span id="DirectMusic_Components"></span><span id="directmusic_components"></span><span id="DIRECTMUSIC_COMPONENTS"></span>DirectMusic 组件

下图显示了 DirectMusic 应用程序用来 *播放* 或 *捕获* MIDI 数据的用户和内核模式组件。

![说明 directmusic 播放和捕获组件的示意图](images/dmusplay.png)

播放组件显示在上图的左半部分，而捕获组件显示在右侧。 Dmu 微型端口驱动程序显示为暗盒，指示它们可以是供应商提供的组件。 如果需要，供应商可以改为使用系统提供的微型端口驱动程序 DMusUART 或 DMusUARTCapture。 图形中的其他组件是系统提供的。

在该图的左上角，DirectMusic 应用程序将带时间戳的 MIDI 流从文件定向到用户模式 [DirectMusic 系统组件](user-mode-wdm-audio-components.md#directmusic_system_component) ( # A0) ，后者又将该流定向到 dmu 端口驱动程序。 此驱动程序可绑定到 DirectMusic 合成或 MPU-401 设备的微型端口驱动程序（如果有）。 或者，可以将端口驱动程序绑定到 [DMusic 系统驱动程序](kernel-mode-wdm-audio-components.md#dmusic_system_driver) ( # A0) ，它是系统提供的 dmu 微型端口驱动程序，用于在软件中实现支持 DLS 的 wavetable 合成器，并且只需要可呈现 wave 音频流的设备。

与 SWMidi 一样，DMusic 驱动程序 Dmusic.sys 将其所有声音组合在一起，生成一个 PCM 格式的波形流，并将其输出到 KMixer。 相反，KMixer 可以将波形流传递到波形设备，该设备的端口和微型端口驱动程序显示在图的左下角，或由 USBAudio 系统驱动程序控制的 USB 音频设备（未显示在图中）。

DirectMusic 捕获组件显示在上图的右半部分。 该图右下角的 DMusic 捕获微型端口驱动程序控制捕获硬件和它所记录的每个 MIDI 消息的时间戳。 Dmu 端口驱动程序将带时间戳的 MIDI 流定向到用户模式 DirectMusic 组件 DMusic.dll。 应用程序通过 DirectMusic API 访问此流，并将带时间戳的 MIDI 数据写入文件。

适配器驱动程序可以使用系统提供的 DMusUARTCapture 微型端口驱动程序来控制 MPU-401 捕获设备。 适配器驱动程序通过使用 GUID 值**CLSID \_ DMusUARTCapture**调用**PcNewMiniport**创建此小型端口驱动程序。 生成的微型端口驱动程序对象支持 **IMiniportDMus** 接口。 Windows 驱动程序工具包 (WDK) 的示例音频驱动程序中提供了 DMusUARTCapture 微型端口驱动程序的源代码。

DirectMusic 应用程序还可以通过 **midiOut ** * SWMidi Xxx 设备运行，例如 ( # A0) 选择。 为简单起见，上图中省略了此路径。 DMusic 驱动程序 ( # A0) 需要初始 DLS 下载才能正常运行;使用 SWMidi 可避免这一要求。

 

