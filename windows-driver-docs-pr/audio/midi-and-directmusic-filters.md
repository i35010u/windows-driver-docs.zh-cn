---
title: MIDI 和 DirectMusic 筛选器
description: MIDI 和 DirectMusic 筛选器
ms.assetid: 622aa4ae-c855-4088-bc1a-30dff7a24d23
keywords:
- 音频筛选 WDK 音频、MIDI
- 音频筛选器 WDK 音频，DirectMusic
- DirectMusic WDK 音频，筛选器
- MIDI 筛选 WDK 音频
- 枚举音频设备 WDK
- 系统提供的微型端口驱动程序 WDK 音频
- 系统提供的端口驱动程序 WDK 音频
- 合成器 WDK 音频，筛选器
- 筛选 WDK 音频、MIDI
- 筛选 WDK 音频，DirectMusic
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3b3e4ef561585c986eefcb50836b946a11724a44
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72830370"
---
# <a name="midi-and-directmusic-filters"></a>MIDI 和 DirectMusic 筛选器


## <span id="midi_and_directmusic_filters"></span><span id="MIDI_AND_DIRECTMUSIC_FILTERS"></span>


MIDI 和 DirectMusic 筛选器代表合成、输出或捕获 MIDI 音乐数据的设备。 通常，应用程序可以通过 DirectMusic API 或 Microsoft Windows 多媒体 **midiOut * * xxx*和 **MidiIn * * xxx*函数访问这些设备的功能。 有关这些接口的详细信息，请参阅 Microsoft Windows SDK 文档。

MIDI 或 DirectMusic*合成*器筛选器接收包含带有时间戳的 midi 事件的 midi 流作为输入。 筛选器输出以下内容之一：

-   波形格式数字音频流

-   可驱动一组扬声器的模拟音频信号

MIDI 或 DirectMusic*输出*筛选器将包含带有时间戳的 midi 事件的 midi 流作为输入接收。 该筛选器将原始 MIDI 消息输出到外部 MIDI 声音模块。

MIDI 或 DirectMusic*捕获*筛选器使用 midi 键盘或其他外部 MIDI 设备输入一系列原始 MIDI 消息。 此筛选器输出由带有时间戳的 MIDI 事件组成的 MIDI 流。

单个 MIDI 或 DirectMusic 筛选器可以执行三个函数（合成、输出和捕获）的组合，具体取决于该筛选器表示的设备的功能。 例如，纯 MPU-401 设备执行输出和捕获，而不是合成。

### <a name="span-idmidi_filterspanspan-idmidi_filterspanspan-idmidi_filterspanmidi-filter"></a><span id="MIDI_Filter"></span><span id="midi_filter"></span><span id="MIDI_FILTER"></span>MIDI 筛选器

MIDI 筛选器实现为端口/微型端口驱动程序对。 MIDI 筛选器工厂按如下方式创建 MIDI 筛选器：

-   它实例化 MIDI 微型端口驱动程序对象。

-   它通过调用具有 GUID 值**CLSID\_PortMidi**的[**PCNEWPORT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-pcnewport)实例化 MIDI 端口驱动程序对象。

-   它调用端口驱动程序的[**IPort：： Init**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iport-init)方法将微型端口驱动程序绑定到端口驱动程序。

[Subdevice 创建](subdevice-creation.md)中的代码示例演示了此过程。 端口和微型端口驱动程序通过其[IPortMidi](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-iportmidi)和[IMiniportMidi](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-iminiportmidi)接口相互通信。

为了支持 MIDI 输出和合成器设备，MIDI 端口驱动程序包含一个软件 sequencer，该 sequencer 将原始 MIDI 消息输出到微型端口驱动程序，计时器分辨率为1毫秒。

### <a name="span-iddirectmusic_filterspanspan-iddirectmusic_filterspanspan-iddirectmusic_filterspandirectmusic-filter"></a><span id="DirectMusic_Filter"></span><span id="directmusic_filter"></span><span id="DIRECTMUSIC_FILTER"></span>DirectMusic 筛选器

DirectMusic 筛选器提供了 MIDI 筛选器功能的超集。 超集包括以下附加功能：

-   DL （可下载的声音）资源，其中包含描述 MIDI 乐器的波形和 articulation 数据。 [**KSPROPERTY\_合成\_dl\_下载**](https://docs.microsoft.com/previous-versions/ff537396(v=vs.85))集-属性请求将 DLS 资源下载到筛选器。

-   用于扩展可选择乐器数量的通道组。 [**Dmu\_内核\_事件**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dmusicks/ns-dmusicks-_dmus_kernel_event)结构，用于将每个带时间戳的 midi 消息打包到 midi 流中，指定要用于该消息的通道组。

-   64位时间戳，提供100毫微秒的分辨率以支持硬件 MIDI 顺序。 DMU\_内核\_事件结构指定了 MIDI 消息的高分辨率时间戳。

对于通道组，可以同时播放的便笺数量不再限制为原始 MIDI 规范的16个通道。 它仅受合成器中可用的声音数量的限制。

DirectMusic 筛选器实现为端口/微型端口驱动程序对。 DirectMusic 筛选器工厂创建 DirectMusic 筛选器，如下所示：

-   它实例化一个 Dmu （DirectMusic）微型端口驱动程序对象。

-   它通过使用 GUID 值**CLSID\_PortDMus**调用[**PcNewPort**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-pcnewport)来实例化 dmu 端口驱动程序对象。

-   它调用端口驱动程序的[**IPort：： Init**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iport-init)方法将微型端口驱动程序绑定到端口驱动程序。

[Subdevice 创建](subdevice-creation.md)中的代码示例演示了此过程。 端口和微型端口驱动程序通过其[IPortDMus](https://docs.microsoft.com/windows-hardware/drivers/ddi/dmusicks/nn-dmusicks-iportdmus)和[IMiniportDMus](https://docs.microsoft.com/windows-hardware/drivers/ddi/dmusicks/nn-dmusicks-iminiportdmus)接口相互通信。

为了支持 DirectMusic 合成器设备，Dmu 端口驱动程序包含低分辨率（单毫秒）软件 sequencer，在计划播放时，可以将时间戳的 MIDI 事件输出到硬件 sequencer 的缓冲区。 为了支持 DirectMusic 输出设备，还可以将端口驱动程序的软件 sequencer 配置为在播放时输出原始 MIDI 消息。

### <a name="span-idenumerating_midi_and_directmusic_devicesspanspan-idenumerating_midi_and_directmusic_devicesspanspan-idenumerating_midi_and_directmusic_devicesspanenumerating-midi-and-directmusic-devices"></a><span id="Enumerating_MIDI_and_DirectMusic_Devices"></span><span id="enumerating_midi_and_directmusic_devices"></span><span id="ENUMERATING_MIDI_AND_DIRECTMUSIC_DEVICES"></span>枚举 MIDI 和 DirectMusic 设备

通过 Windows 多媒体**midiInXxx**或**MIDIOUTXXX**函数枚举 MIDI 输入或输出设备时，应用程序只能看到其微型端口驱动程序公开*MIDI pin*的 WDM 设备。 这些是管理原始 MIDI 流但缺少对 DL 和通道组等高级功能的支持。 但是，在通过 DirectMusic 枚举设备时，应用程序可以看到 WDM 设备同时具有 MIDI 引脚和*DirectMusic 针脚*。 DirectMusic pin 管理带有时间戳的 MIDI 流，并支持 DL 和通道组。

实现自定义微型端口驱动程序时，硬件供应商通常会写入 MIDI 微型端口驱动程序或 Dmu 微型端口驱动程序，但不能同时编写两者。 MIDI 微型端口驱动程序只能公开 MIDI pin。 但是，Dmu 微型端口驱动程序可以同时公开 MIDI 和 DirectMusic pin，这无需编写单独的 MIDI 微型端口驱动程序。 有关 DirectMusic 筛选器上的 MIDI pin 的示例，请参阅 Windows 驱动程序工具包（WDK）中的 Dmusuart 示例音频驱动程序。

指定 MIDI 或 DirectMusic pin 的数据范围时，MIDI 或 Dmu 微型端口驱动程序指定类型为 KSDATAFORMAT\_类型的主要格式\_音乐和 KSDATARANGE 类型的 subformat\_子类型\_MIDI 的为 DirectMusic pin\_子类型\_DIRECTMUSIC。 MIDI 和 DirectMusic pin 的数据范围描述符的示例分别显示在[Midi 流数据范围](midi-stream-data-range.md)和[DirectMusic 流数据范围](directmusic-stream-data-range.md)内。

MIDI 筛选器上的 MIDI pin 实例公开[IMiniportMidiStream](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-iminiportmidistream)接口。 DirectMusic 筛选器上的 MIDI 或 DirectMusic pin 实例公开了[IMXF](https://docs.microsoft.com/windows-hardware/drivers/ddi/dmusicks/nn-dmusicks-imxf)接口。

在 Windows Me/98 中，DirectMusic 有时会两次枚举相同的 MPU-401 设备。 原因在于，一些硬件供应商将 MPU-401 设备同时作为旧的、WDM 的 MIDI 设备和 WDM 设备公开。 对于旧设备，DirectMusic 会枚举 MPU-401 设备，该设备表示从 DMusic 到 Ihvaudio 的直接路径。 对于 WDM 设备，DirectMusic 通过包含以下组件序列的 circuitous 路径枚举相同的 MPU-401 设备：

1.  DMusic

2.  DMusic16

3.  MMSystem

4.  WDMAud. winspool.drv

5.  WDMAud

6.  供应商的微型端口驱动程序

Windows 多媒体控制面板（Mmsys）中显示的 MIDI 合成器的名称将与 WDM 设备的名称相同。

### <a name="span-idsystem-supplied_port_and_miniport_driversspanspan-idsystem-supplied_port_and_miniport_driversspanspan-idsystem-supplied_port_and_miniport_driversspansystem-supplied-port-and-miniport-drivers"></a><span id="System-Supplied_Port_and_Miniport_Drivers"></span><span id="system-supplied_port_and_miniport_drivers"></span><span id="SYSTEM-SUPPLIED_PORT_AND_MINIPORT_DRIVERS"></span>系统提供的端口和微型端口驱动程序

PortCls 系统驱动程序内置了几个系统提供的 MIDI 和 Dmu 微型端口驱动程序：

-   FMSynth 微型端口驱动程序提供了一个用于实现 OPL3 的 FM 合成的 MIDI 设备接口。

-   UART 微型端口驱动程序支持使用 MPU-401 硬件接口的 MIDI 设备，但是该驱动程序现已过时（在 Windows 98 黄金之后），并且仅适用于现有的适配器驱动程序。 新的适配器驱动程序代码应改为使用 DMusUART 微型端口驱动程序（在 Windows 98 SE 和 Windows Me 中以及 Windows 2000 及更高版本中），这会取代 UART 并实现其功能的超集。

适配器驱动程序可以通过调用[**PcNewMiniport**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-pcnewminiport)函数来访问系统提供的微型端口驱动程序。 在 Windows 驱动程序工具包（WDK）中，FMSynth 和 DMusUART 微型端口驱动程序也作为示例音频驱动程序包含。 通过修改这些示例中的源代码，硬件供应商可以扩展驱动程序来管理其设备的专有功能。

DMusUART 是公开 MIDI 和 DirectMusic pin 的 Dmu 微型端口驱动程序的示例，但不支持 DLS 下载或硬件排序。 微型端口驱动程序的 DirectMusic 呈现 pin 具有支持多个[KSPROPSETID\_合成](https://docs.microsoft.com/windows-hardware/drivers/audio/kspropsetid-synth)属性的合成节点（[**KSNODETYPE\_合成**](https://docs.microsoft.com/windows-hardware/drivers/audio/ksnodetype-synthesizer)器）。 小型小型驱动程序将其本身包含在 KSCATEGORY 中\_捕获\_RENDER 和 KSCATEGORY 中，但不包含在 KSCATEGORY\_合成器中（因为它不包含内部合成器）。 有关详细信息，请参阅 WDK 中的 DMusUART 示例音频驱动程序。

请注意，在 Windows XP 和更高版本中，MIDI 和 Dmu 端口驱动程序使用相同的内部软件实现。 这意味着调用**PcNewPort**时， **clsid\_PortMidi**和**clsid\_PortDMus** guid 是等效的。 对于为以前版本的 Windows 编写的应用程序，不会因合并 MIDI 和 Dmu 端口驱动程序而导致行为发生变化。

 

 




