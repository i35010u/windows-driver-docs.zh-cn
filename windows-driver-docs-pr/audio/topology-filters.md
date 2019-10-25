---
title: 拓扑筛选器
description: 拓扑筛选器
ms.assetid: 1b3d35e9-5858-407c-9cd0-06307d82ce58
keywords:
- 音频筛选 WDK 音频，拓扑筛选器
- 拓扑筛选 WDK 音频
- 筛选 WDK 音频、拓扑
- 混合渲染流 WDK 音频
- 多路复用捕获流 WDK 音频
- 桥接 WDK 音频
- 连接 WDK 音频
- 筛选器工厂 WDK 音频
- 锁定 WDK 音频，拓扑筛选器
- 节点 WDK 音频
- 输入插针 WDK 音频
- 输出插针 WDK 音频
- PCCONNECTION_DESCRIPTOR 数组
- 音频插孔
- 数字连接器 WDK 音频
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9d860aa8c23be7e5670322a4652420dfa7f517da
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72830002"
---
# <a name="topology-filters"></a>拓扑筛选器


## <span id="topology_filters"></span><span id="TOPOLOGY_FILTERS"></span>


*拓扑筛选器*表示音频适配器卡上电路的部分，用于处理在卡上管理的各种波形和 MIDI 流之间的交互。 此电路混合了捕获流的呈现流和多路复用。

拓扑筛选器提供了*桥接*器（请参阅[音频筛选器图](audio-filter-graphs.md)），它表示音频适配器与外部设备的物理连接。 这些连接通常携带模拟输出信号，可驱动扬声器和来自麦克风的模拟输入信号。 拓扑筛选器的桥接器还可能表示模拟 linein 和 lineout 插孔，甚至可能表示数字输入和输出连接器。

术语 "拓扑筛选器" misnomer。 无论其名称如何，拓扑筛选器都只是公开其内部拓扑或布局的多种类型的音频筛选器之一。 尽管拓扑筛选器包含关键拓扑功能，但它不一定包含适配器的整个拓扑。 Wave 和 MIDI 筛选器都具有自己的拓扑。 例如，最小的 WaveCyclic 或 WavePci 筛选器（请参阅[波形筛选](wave-filters.md)器）可能会公开包含两个插针和 DAC （数字到模拟转换器）或 ADC （模拟到数字转换器）的拓扑，具体取决于基础设备是否确实音频呈现或捕获。

拓扑筛选器实现为端口/微型端口对。 拓扑筛选器工厂创建拓扑筛选器，如下所示：

-   它实例化拓扑微型端口驱动程序对象。

-   它通过调用 GUID 值**CLSID\_PortTopology**的[**PcNewPort**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-pcnewport)实例化拓扑端口驱动程序对象。

-   它调用端口驱动程序的[**IPort：： Init**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iport-init)方法将微型端口驱动程序绑定到端口驱动程序。

[Subdevice 创建](subdevice-creation.md)中的代码示例演示了此过程。

拓扑端口和微型端口驱动程序通过各自的[IPortTopology](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-iporttopology)和[IMiniportTopology](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-iminiporttopology)接口相互通信。 与 wave 和 MIDI 端口和微型端口驱动程序相比，这些接口相对简单，因为拓扑筛选器不需要显式管理通过其 pin 的流。 拓扑筛选器的 pin 表示适配器硬件中的硬编码连接。 通常，拓扑筛选器 pin 的物理连接通常携带模拟音频信号，但可能会携带数字音频流，具体取决于硬件实现。

与[IMiniportWaveCyclic](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-iminiportwavecyclic)、 [IMiniportWavePci](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-iminiportwavepci)、 [IMiniportMidi](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-iminiportmidi)和[IMiniportDMus](https://docs.microsoft.com/windows-hardware/drivers/ddi/dmusicks/nn-dmusicks-iminiportdmus)接口相比， [IMiniportTopology](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-iminiporttopology)接口没有**newstream.ischecked**方法。

拓扑筛选器的大部分功能由其属性处理程序提供。 拓扑筛选器主要用于向[SysAudio 系统驱动程序](kernel-mode-wdm-audio-components.md#sysaudio_system_driver)和使用 Microsoft Windows 多媒体混音器 API 的应用程序提供拓扑信息。 拓扑筛选器中的属性处理程序提供对音频适配器通常提供的各种控件（如卷、均衡和回音）的访问权限。 通过属性请求，混音器 API 可以枚举适配器硬件中的控制节点，发现节点之间的连接，以及两个查询和设置节点的控制参数。 SndVol32 应用程序（请参阅[托盘和 SndVol32](systray-and-sndvol32.md)）使用混音器 API 来发现适配器的每个流的卷和静音控件。

生成筛选器图时，SysAudio 会在其 pin 中查询[**KSPROPERTY\_\_** ](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-pin-physicalconnection)的拓扑筛选器，以确定哪些 WAVE、MIDI 或 DirectMusic 筛选器 pin 连接到哪些拓扑筛选器 pin。

与 wave、MIDI 或 DirectMusic 筛选器不同，拓扑筛选器不会实例化 pin。 因此，不能使用 pin 对象处理拓扑筛选器的 pin 属性的查询。 拓扑筛选器自行处理有关其 pin 的物理连接的所有查询。 有关详细信息，请参阅[KSPROPSETID\_Pin](https://docs.microsoft.com/windows-hardware/drivers/stream/kspropsetid-pin)。

与其他类型的音频筛选器类似，拓扑筛选器使用[ **\_PCCONNECTION**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff537688(v=vs.85))的数组来描述其内部拓扑。 微型端口驱动程序会在[**PCFILTER\_描述符**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/ns-portcls-pcfilter_descriptor)结构中公开此数组，该数组是从[**IMiniport：： GetDescription**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iminiport-getdescription)方法输出的。 数组将拓扑指定为拓扑筛选器节点和 pin 之间的连接列表（请参阅[节点和连接](nodes-and-connections.md)）。 [WDMAud 系统驱动程序](user-mode-wdm-audio-components.md#wdmaud_system_driver)将这些连接和节点转换为混音器 API 向应用程序公开的混合器线条和控件。 如[音频筛选](audio-filters.md)器中所述，KS 筛选器上的输入插针映射到 SRC 混合器行，筛选器上的输出插针映射到 DST 混音器行。

典型的音频适配器可以通过扬声器播放波形和 MIDI 文件，并且可以从麦克风和 MIDI 合成器捕获音频信号。 下面的代码示例包含用于公开这些功能的拓扑筛选器的 PCCONNECTION\_说明符数组：

```cpp
    // topology pins
    enum
    {
        KSPIN_TOPO_WAVEOUT_SRC = 0,
        KSPIN_TOPO_SYNTHOUT_SRC,
        KSPIN_TOPO_SYNTHIN_SRC,
        KSPIN_TOPO_MIC_SRC,
        KSPIN_TOPO_LINEOUT_DST,
        KSPIN_TOPO_WAVEIN_DST
    };
 
    // topology nodes
    enum
    {
        KSNODE_TOPO_WAVEOUT_VOLUME = 0,
        KSNODE_TOPO_WAVEOUT_MUTE,
        KSNODE_TOPO_SYNTHOUT_VOLUME,
        KSNODE_TOPO_SYNTHOUT_MUTE,
        KSNODE_TOPO_MIC_VOLUME,
        KSNODE_TOPO_SYNTHIN_VOLUME,
        KSNODE_TOPO_LINEOUT_MIX,
        KSNODE_TOPO_LINEOUT_VOLUME,
        KSNODE_TOPO_WAVEIN_MUX
    };
 
    static PCCONNECTION_DESCRIPTOR MiniportConnections[] =
    {
       // FromNode---------------------FromPin------------------ToNode-----------------------ToPin
 
        { PCFILTER_NODE,               KSPIN_TOPO_WAVEOUT_SRC,  KSNODE_TOPO_WAVEOUT_VOLUME,  1 },
        { KSNODE_TOPO_WAVEOUT_VOLUME,  0,                       KSNODE_TOPO_WAVEOUT_MUTE,    1 },
        { KSNODE_TOPO_WAVEOUT_MUTE,    0,                       KSNODE_TOPO_LINEOUT_MIX,     1 },
 
        { PCFILTER_NODE,               KSPIN_TOPO_SYNTHOUT_SRC, KSNODE_TOPO_SYNTHOUT_VOLUME, 1 },
        { KSNODE_TOPO_SYNTHOUT_VOLUME, 0,                       KSNODE_TOPO_SYNTHOUT_MUTE,   1 },
        { KSNODE_TOPO_SYNTHOUT_MUTE,   0,                       KSNODE_TOPO_LINEOUT_MIX,     2 },
 
        { PCFILTER_NODE,               KSPIN_TOPO_SYNTHIN_SRC,  KSNODE_TOPO_SYNTHIN_VOLUME,  1 },
        { KSNODE_TOPO_SYNTHIN_VOLUME,  0,                       KSNODE_TOPO_WAVEIN_MUX,      1 },
 
        { PCFILTER_NODE,               KSPIN_TOPO_MIC_SRC,      KSNODE_TOPO_MIC_VOLUME,      1 },
        { KSNODE_TOPO_MIC_VOLUME,      0,                       KSNODE_TOPO_WAVEIN_MUX,      2 },
 
        { KSNODE_TOPO_LINEOUT_MIX,     0,                       KSNODE_TOPO_LINEOUT_VOLUME,  1 },
        { KSNODE_TOPO_LINEOUT_VOLUME,  0,                 PCFILTER_NODE,  KSPIN_TOPO_LINEOUT_DST },
 
        { KSNODE_TOPO_WAVEIN_MUX,      0,                 PCFILTER_NODE,  KSPIN_TOPO_WAVEIN_DST }
    };
```

前面的代码示例中的常量[**PCFILTER\_节点**](https://docs.microsoft.com/previous-versions/ff537695(v=vs.85))是 NULL 节点 ID，在头文件 Portcls 中定义。 有关如何使用此常量来区分某个节点上的逻辑引脚的筛选器上的外部 pin 的说明，请参阅[**PCCONNECTION\_描述符**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff537688(v=vs.85))。

前面的代码示例中的每个 pin 名称都以 "SRC" 或 "DST" 结尾，具体取决于混音器 API 是否将 pin 映射到源或目标混音器行。 为避免混淆，请记住源和目标混合器行将分别映射到接收器（input）和源（输出） KS 筛选器。 有关详细信息，请参阅[音频筛选器](audio-filters.md)。

前面的代码示例中的 PCCONNECTION\_说明符数组介绍了下图中的拓扑筛选器。

![说明 pcconnection\-描述符数组描述的拓扑筛选器连接的关系图](images/topofilt.png)

图中的拓扑筛选器左侧有四个输入（接收器）针脚，右侧有两个输出（源）针脚。 连接顶部两个输入插针和顶部输出插针的数据路径混合了两个模拟信号，它们已从 wave 和正在播放的 MIDI 流中呈现。 用于连接底部的两个输入插针和底部输出插针的数据路径会对正在记录的捕获的模拟信号进行多路复用。

四个输入插针按如下方式操作：

-   KSPIN\_TOPO\_WAVEOUT\_SRC pin 以物理方式连接到波形滤波器的输出插针，这会从诸如 .wav 文件之类的源呈现波形流，以在 pin 生成模拟信号。

-   KSPIN\_TOPO\_SYNTHOUT\_SRC pin 以物理方式连接到合成筛选器的输出插针，例如，来自源（如 mid 文件）的 MIDI 流将在 pin 中生成模拟信号。

-   KSPIN\_TOPO\_SYNTHIN\_SRC pin 以物理方式连接到生成模拟信号的合成器。 （请注意，更实用的硬件设计可能会从 MPU-401 MIDI 接口获取 MIDI 输入流，并将其直接转换为波形格式，同时绕过拓扑筛选器。）

-   KSPIN\_TOPO\_MIC\_SRC pin 以物理方式连接到使用麦克风发出模拟信号的输入插孔。

这两个输出插针的操作如下所示：

-   KSPIN\_TOPO\_LINEOUT\_DST pin 以物理方式连接到模拟 LINEOUT 插孔，通常驱动一组扬声器。

-   KSPIN\_TOPO\_WAVEIN\_DST pin 以物理方式连接到波形滤波器的输入插针，这会将模拟信号转换为波形流，并将其写入到目标（如 .wav 文件）。

卷和静音节点（请参阅[**KSNODETYPE\_volume**](https://docs.microsoft.com/windows-hardware/drivers/audio/ksnodetype-volume)和[**KSNODETYPE\_静音**](https://docs.microsoft.com/windows-hardware/drivers/audio/ksnodetype-mute)）用于控制各种流的音量级别。 SUM 节点（请参阅[**KSNODETYPE\_SUM**](https://docs.microsoft.com/windows-hardware/drivers/audio/ksnodetype-sum)）将音频流与 wave 输入混合。 MUX 节点（请参阅[**KSNODETYPE\_MUX**](https://docs.microsoft.com/windows-hardware/drivers/audio/ksnodetype-mux)）在两个输入流之间进行选择。

该图使用一个虚线箭头来表示两个节点之间的连接或 pin 与节点之间的连接。 箭头指向数据流的方向。 此关系图显示了总共13个连接，每个连接对应于前面的代码示例中 PCCONNECTION\_说明符数组中的13个元素之一。

除了拓扑筛选器外，适配器驱动程序还会创建其他筛选器--wave、FM 合成、波形表等，它们连接到拓扑筛选器上的 pin。

例如，物理连接到拓扑筛选器的 KSPIN\_TOPO\_WAVEOUT\_SRC pin 的波形筛选器包含一个 DAC （由[**KSNODETYPE\_DAC**](https://docs.microsoft.com/windows-hardware/drivers/audio/ksnodetype-dac)节点表示），该 DAC 将 PCM 数据转换为模拟信号输出到拓扑筛选器的 pin。 以物理方式连接到拓扑筛选器的 KSPIN\_TOPO\_SYNTHOUT\_SRC pin）的 FM 合成或 wavetable 合成筛选器同样会将 MIDI 数据转换为其输出到拓扑筛选器的 pin 的模拟信号。 拓扑筛选器将模拟信号与这两个针脚混合，并将混合信号输出到扬声器。

拓扑筛选器与其他筛选器的物理连接，这些筛选器表示同一适配器卡上的其他硬件设备，需要与筛选器的其他类型的连接区分开来。 例如，可以在 "软件控制" 下连接或断开 wave、MIDI 和 DirectMusic 过滤器上的某些针脚。

在设备启动过程中，适配器驱动程序通过对每个连接调用[**PcRegisterPhysicalConnection**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-pcregisterphysicalconnection)来注册拓扑筛选器的物理连接。 端口驱动程序需要此信息才能响应[**KSPROPERTY\_PIN\_PHYSICALCONNECTION**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-pin-physicalconnection)请求。

 

 




