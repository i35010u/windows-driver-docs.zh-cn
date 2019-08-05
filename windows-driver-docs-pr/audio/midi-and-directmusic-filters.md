---
title: MIDI 和 DirectMusic 筛选器
description: MIDI 和 DirectMusic 筛选器
ms.assetid: 622aa4ae-c855-4088-bc1a-30dff7a24d23
keywords:
- 音频筛选器 WDK 音频 MIDI
- 音频筛选器 WDK 音频 DirectMusic
- DirectMusic WDK 音频，筛选器
- MIDI 筛选 WDK 音频
- 枚举音频设备 WDK
- 系统提供的微型端口驱动程序 WDK 音频
- 系统提供的端口驱动程序 WDK 音频
- 合成器 WDK 音频，筛选器
- 筛选器 WDK 音频 MIDI
- 筛选器 WDK 音频 DirectMusic
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 87c4e93dbf30bedb745867cb4a9c2fa0acdee4b7
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67363850"
---
# <a name="midi-and-directmusic-filters"></a>MIDI 和 DirectMusic 筛选器


## <span id="midi_and_directmusic_filters"></span><span id="MIDI_AND_DIRECTMUSIC_FILTERS"></span>


MIDI 和 DirectMusic 筛选器表示合成，输出中，会捕获的 MIDI 音乐数据的设备。 应用程序通常访问这些设备的功能，通过 DirectMusic API 或通过 Microsoft Windows 多媒体 **midiOut * * * Xxx*和 **midiIn * * * Xxx*函数。 有关这些接口的详细信息，请参阅 Microsoft Windows SDK 文档。

MIDI 或 DirectMusic*合成器*加盖时间戳 MIDI 事件所组成的 MIDI 流作为输入接收筛选器。 筛选器输出以下值之一：

-   Wave 格式的数字音频流

-   模拟可以推动套扬声器的音频信号

MIDI 或 DirectMusic*输出*加盖时间戳 MIDI 事件所组成的 MIDI 流作为输入接收筛选器。 筛选器原始 MIDI 消息输出到外部的 MIDI 声音模块。

MIDI 或 DirectMusic*捕获*筛选器将作为输入一系列的原始 MIDI 消息从 MIDI 键盘或其他外部 MIDI 设备。 筛选器输出带时间戳 MIDI 事件所组成的 MIDI 流。

单个 MIDI 或 DirectMusic 筛选器可以执行三个函数-合成、 输出和捕获-具体取决于筛选器表示设备的功能的组合。 例如，纯 MPU 401 设备执行输出和捕获，但不是合成。

### <a name="span-idmidi_filterspanspan-idmidi_filterspanspan-idmidi_filterspanmidi-filter"></a><span id="MIDI_Filter"></span><span id="midi_filter"></span><span id="MIDI_FILTER"></span>MIDI 筛选器

作为端口/微型端口驱动程序对实现的 MIDI 筛选器。 MIDI 筛选器工厂创建 MIDI 筛选器，如下所示：

-   它实例化 MIDI 微型端口驱动程序对象。

-   它通过调用实例化 MIDI 端口驱动程序对象[ **PcNewPort** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-pcnewport)使用的 GUID 值**CLSID\_PortMidi**。

-   它将调用端口驱动程序[ **IPort::Init** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-iport-init)方法绑定到端口驱动程序的微型端口驱动程序。

中的代码示例[子创建](subdevice-creation.md)说明了此过程。 通过与其他通信的端口和微型端口驱动程序及其[IPortMidi](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-iportmidi)并[IMiniportMidi](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-iminiportmidi)接口。

若要支持 MIDI 输出和合成器的设备，MIDI 端口驱动程序包含原始 MIDI 消息输出到与为一毫秒的计时器分辨率的微型端口驱动程序软件 sequencer。

### <a name="span-iddirectmusic_filterspanspan-iddirectmusic_filterspanspan-iddirectmusic_filterspandirectmusic-filter"></a><span id="DirectMusic_Filter"></span><span id="directmusic_filter"></span><span id="DIRECTMUSIC_FILTER"></span>DirectMusic 筛选器

DirectMusic 筛选器提供 MIDI 筛选器的功能的超集。 超集包括这些附加功能：

-   DLS （可下载声音） 包含描述 MIDI instruments 波形和清晰表述数据的资源。 一个[ **KSPROPERTY\_合成\_DLS\_下载**](https://docs.microsoft.com/previous-versions/ff537396(v=vs.85))集属性请求将 DLS 资源下载到筛选器。

-   为扩展可选择 instruments 数信道组。 [ **DMU\_内核\_事件**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dmusicks/ns-dmusicks-_dmus_kernel_event)结构，它用于打包 MIDI 流中的每个时间戳 MIDI 消息，指定要使用该消息的通道组。

-   具有支持硬件 MIDI 序列化的 100 纳秒解决的 64 位时间戳。 DMU\_内核\_事件结构指定 MIDI 消息的高分辨率时间戳。

与通道组可以同时播放的备注不再限制为 16 个原始 MIDI 规范的通道。 它仅受到语音合成器中提供的数量。

作为端口/微型端口驱动程序对实现 DirectMusic 筛选器。 DirectMusic 筛选器工厂创建 DirectMusic 筛选器，如下所示：

-   它实例化 Dmu (DirectMusic) 微型端口驱动程序对象。

-   它通过调用实例化 Dmu 端口驱动程序对象[ **PcNewPort** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-pcnewport)使用的 GUID 值**CLSID\_PortDMus**。

-   它将调用端口驱动程序[ **IPort::Init** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-iport-init)方法绑定到端口驱动程序的微型端口驱动程序。

中的代码示例[子创建](subdevice-creation.md)说明了此过程。 通过与其他通信的端口和微型端口驱动程序及其[IPortDMus](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dmusicks/nn-dmusicks-iportdmus)并[IMiniportDMus](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dmusicks/nn-dmusicks-iminiportdmus)接口。

若要支持 DirectMusic 合成器设备，Dmu 端口驱动程序包含可以输出带时间戳之前它们计划要播放的硬件排序器的缓冲区的 MIDI 事件较低分辨率 （1 毫秒） 软件 sequencer。 若要支持 DirectMusic 输出设备，端口驱动程序软件 sequencer 可以还将配置为原始 MIDI 消息输出在它们是要播放的时间。

### <a name="span-idenumerating_midi_and_directmusic_devicesspanspan-idenumerating_midi_and_directmusic_devicesspanspan-idenumerating_midi_and_directmusic_devicesspanenumerating-midi-and-directmusic-devices"></a><span id="Enumerating_MIDI_and_DirectMusic_Devices"></span><span id="enumerating_midi_and_directmusic_devices"></span><span id="ENUMERATING_MIDI_AND_DIRECTMUSIC_DEVICES"></span>枚举 MIDI 和 DirectMusic 设备

当枚举输入或输出的 MIDI 设备的整个 Windows 多媒体**midiInXxx**或**midiOutXxx**函数中，应用程序能够看到其微型端口驱动程序公开仅WDM设备*MIDI pin*。 这些是管理但缺少支持高级功能，例如 DLS 和通道的组的原始 MIDI 流的 pin。 但是，枚举通过 DirectMusic 设备时，应用程序可以看到以这两个 MIDI 插针 WDM 设备和*DirectMusic pin*。 DirectMusic pin 管理加盖时间戳 MIDI 流，并支持 DLS 和通道的组。

在实现自定义的微型端口驱动程序时，硬件供应商通常会写入 MIDI 微型端口驱动程序或 Dmu 微型端口驱动程序，但不可同时使用两者。 MIDI 微型端口驱动程序可以公开仅 MIDI pin。 但是，Dmu 微型端口驱动程序可以公开 MIDI 和 DirectMusic 插针，这消除了需要编写单独的 MIDI 微型端口驱动程序。 有关 MIDI pin DirectMusic 筛选器的示例，请参阅 Dmusuart 示例音频驱动程序 Windows Driver Kit (WDK) 中。

MIDI 或 Dmu 微型端口驱动程序在指定 MIDI 或 DirectMusic pin 的数据范围时，指定的主要格式为类型 KSDATAFORMAT\_类型\_音乐和的子格式类型 KSDATARANGE\_子类型\_的 MIDIMIDI pin 或 KSDATARANGE\_子类型\_DIRECTMUSIC DirectMusic pin。 数据范围描述符的 MIDI 和 DirectMusic 插针的示例显示在[MIDI Stream 数据范围](midi-stream-data-range.md)并[DirectMusic Stream 数据范围](directmusic-stream-data-range.md)分别。

MIDI 筛选器上的 MIDI pin 实例公开[IMiniportMidiStream](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-iminiportmidistream)接口。 DirectMusic 筛选器的 MIDI 或 DirectMusic pin 实例公开[IMXF](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dmusicks/nn-dmusicks-imxf)接口。

在 Windows 中我 / 98，DirectMusic 有时枚举相同的 MPU 401 设备两次。 原因是某些硬件供应商公开其 MPU 401 设备作为旧，pre WDM MIDI 设备和 WDM 设备。 对于旧的设备，DirectMusic 枚举表示的直接路径从 DMusic.dll Ihvaudio.dll MPU 401 设备。 WDM 设备 DirectMusic 枚举通过间接路径包含以下一系列组件的相同的 MPU 401 设备：

1.  DMusic.dll

2.  DMusic16.dll

3.  MMSystem.dll

4.  WDMAud.drv

5.  WDMAud.sys

6.  供应商的微型端口驱动程序

MIDI 合成器，它显示位于 Windows 多媒体控制面板 (Mmsys.cpl) 将具有与 WDM 设备相同的名称。

### <a name="span-idsystem-supplied_port_and_miniport_driversspanspan-idsystem-supplied_port_and_miniport_driversspanspan-idsystem-supplied_port_and_miniport_driversspansystem-supplied-port-and-miniport-drivers"></a><span id="System-Supplied_Port_and_Miniport_Drivers"></span><span id="system-supplied_port_and_miniport_drivers"></span><span id="SYSTEM-SUPPLIED_PORT_AND_MINIPORT_DRIVERS"></span>系统提供的端口和微型端口驱动程序

多个系统提供 MIDI 和 Dmu 微型端口驱动程序已内置到 PortCls 系统驱动程序：

-   FMSynth 微型端口驱动程序提供一个接口实现 OPL3 样式 FM 合成的 MIDI 设备。

-   UART 微型端口驱动程序支持与 MPU 401 硬件接口，MIDI 设备，但此驱动程序 （在 Windows 98 金色） 现已过时，仅对现有适配器驱动程序支持。 新适配器驱动程序代码应改用 DMusUART 微型端口驱动程序 （在 Windows 98 SE 和 Windows Me，并在 Windows 2000 和更高版本），它取代了 UART 并实现了其功能的超集。

适配器驱动程序可以访问的系统提供的微型端口驱动程序通过调用[ **PcNewMiniport** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-pcnewminiport)函数。 FMSynth 和 DMusUART 微型端口驱动程序，还提供作为示例音频驱动程序 Windows Driver Kit (WDK) 中。 通过修改这些示例中的源代码，硬件供应商可以扩展的驱动程序来管理其设备的专有功能。

DMusUART 是 Dmu 微型端口驱动程序的公开 MIDI 和 DirectMusic 插针，但不支持 DLS 下载或硬件序列化的示例。 微型端口驱动程序的 DirectMusic 呈现 pin 都有一个合成器节点 ([**KSNODETYPE\_合成器**](https://docs.microsoft.com/windows-hardware/drivers/audio/ksnodetype-synthesizer))，支持多个[KSPROPSETID\_合成器](https://docs.microsoft.com/windows-hardware/drivers/audio/kspropsetid-synth)属性。 微型端口驱动程序包括本身类别 KSCATEGORY\_呈现器和 KSCATEGORY\_捕获，但不是在 KSCATEGORY\_合成器 （因为它不包含内部合成器）。 有关详细信息，请参阅 DMusUART 示例音频驱动程序 WDK 中。

请注意，在 Windows XP 及更高版本，MIDI 和 Dmu 端口驱动程序使用相同的内部软件实现。 这意味着**CLSID\_PortMidi**并**CLSID\_PortDMus**调用时，Guid 是等效**PcNewPort**。 对于早期版本的 Windows 编写的应用程序应会看到行为，从而从合并的 MIDI 和 Dmu 端口驱动程序没有的变化。

 

 




