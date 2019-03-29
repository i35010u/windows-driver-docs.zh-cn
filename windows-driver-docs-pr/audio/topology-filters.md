---
title: 拓扑筛选器
description: 拓扑筛选器
ms.assetid: 1b3d35e9-5858-407c-9cd0-06307d82ce58
keywords:
- 音频筛选器 WDK 音频，拓扑筛选器
- 拓扑 WDK 音频筛选器
- 筛选器 WDK 音频，拓扑
- 混合呈现流 WDK 音频
- 捕获流 WDK 音频多路复用
- 桥 pin WDK 音频
- 连接 WDK 音频
- 筛选器工厂 WDK 音频
- pin WDK 音频，拓扑筛选器
- 节点 WDK 音频
- 输入插针 WDK 音频
- 输出插针 WDK 音频
- PCCONNECTION_DESCRIPTOR 数组
- 音频插孔 WDK
- 数字连接器 WDK 音频
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9851047bb4543c196f8953ddb74adb03ab15dba9
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56566293"
---
# <a name="topology-filters"></a>拓扑筛选器


## <span id="topology_filters"></span><span id="TOPOLOGY_FILTERS"></span>


一个*拓扑筛选器*表示处理在不同的批和托管卡的 MIDI 流之间的交互的音频的适配器卡上的电路的部分。 此电路会呈现流的混合使用，并捕获流的多路复用。

拓扑筛选器提供*桥接插针*(请参阅[音频筛选器关系图](audio-filter-graphs.md))，可表示音频适配器的物理连接到外部设备。 这些连接通常承担驱动器发言人的模拟输出信号和麦克风从模拟输入的信号。 拓扑筛选器的桥 pin 可能还表示模拟的线路输入和线路输出插孔和甚至可以是数字输入和输出连接器。

术语"拓扑筛选器"中从某种意义上是用词不当。 尽管其名称，拓扑筛选器只是一个公开其内部拓扑或布局的几种类型的音频筛选器。 虽然拓扑筛选器包含拓扑的主要功能，但它不一定包含适配器的整个拓扑。 批和 MIDI 筛选器具有其自己的拓扑。 例如，最小 WaveCyclic 或 WavePci 筛选器 (请参阅[批筛选器](wave-filters.md)) 可能会公开具体取决于两个 pin 和 DAC （数字模拟转换器） 或 ADC （模拟到数字转换器） 组成的拓扑基础设备 does 音频呈现或捕获。

拓扑筛选器作为端口/微型端口对。 拓扑筛选器工厂创建拓扑筛选器，如下所示：

-   它实例化拓扑微型端口驱动程序对象。

-   它通过调用实例化拓扑端口驱动程序对象[ **PcNewPort** ](https://msdn.microsoft.com/library/windows/hardware/ff537715)使用的 GUID 值**CLSID\_PortTopology**。

-   它将调用端口驱动程序[ **IPort::Init** ](https://msdn.microsoft.com/library/windows/hardware/ff536943)方法绑定到端口驱动程序的微型端口驱动程序。

中的代码示例[子创建](subdevice-creation.md)说明了此过程。

拓扑端口和微型端口驱动程序与彼此通信通过其各自[IPortTopology](https://msdn.microsoft.com/library/windows/hardware/ff536896)并[IMiniportTopology](https://msdn.microsoft.com/library/windows/hardware/ff536712)接口。 由于拓扑筛选器不需要显式管理通过他们的 pin 的流比较与批和 MIDI 端口和微型端口驱动程序，这些接口是相对简单。 拓扑筛选器的插针表示适配器硬件中的硬编码连接。 通常基础拓扑筛选器 pin 的物理连接执行模拟的音频信号，但可以根据硬件实现相反，含有数字音频流。

与此相反[IMiniportWaveCyclic](https://msdn.microsoft.com/library/windows/hardware/ff536714)， [IMiniportWavePci](https://msdn.microsoft.com/library/windows/hardware/ff536724)， [IMiniportMidi](https://msdn.microsoft.com/library/windows/hardware/ff536703)，以及[IMiniportDMus](https://msdn.microsoft.com/library/windows/hardware/ff536699)接口[IMiniportTopology](https://msdn.microsoft.com/library/windows/hardware/ff536712)接口没有**NewStream**方法。

由其属性处理程序提供的大多数拓扑筛选器的功能。 拓扑筛选器存在主要是为了拓扑信息提供给[SysAudio 系统驱动程序](kernel-mode-wdm-audio-components.md#sysaudio_system_driver)和使用 Microsoft Windows 多媒体混音器 API 的应用程序。 中的拓扑筛选器的属性处理程序提供对音频适配器通常提供的各种控件 （如卷、 均衡和混响） 的访问。 通过属性请求混音器 API 可以枚举的适配器硬件中的控制节点、 发现节点之间的连接和同时查询和设置节点的控制参数。 SndVol32 应用程序 (请参阅[任务栏和 SndVol32](systray-and-sndvol32.md)) 使用混音器 API 来发现适配器的每个流音量和静音控件。

SysAudio 时生成筛选器关系图，查询的拓扑筛选器[ **KSPROPERTY\_PIN\_PHYSICALCONNECTION** ](https://msdn.microsoft.com/library/windows/hardware/ff565205)在其插针，以确定哪个批，MIDI 属性或 DirectMusic 筛选器插针连接到的拓扑的筛选器 pin。

与不同的是，会出现一批 MIDI 或 DirectMusic 筛选，拓扑筛选器不会实例化的 pin。 因此，任何 pin 对象不是可用于处理拓扑筛选器的固定属性的查询。 拓扑筛选器本身将处理有关在其 pin 的物理连接的所有查询。 有关详细信息，请参阅[KSPROPSETID\_Pin](https://msdn.microsoft.com/library/windows/hardware/ff566584)。

与其他类型的音频筛选器类似，拓扑筛选器使用的数组[ **PCCONNECTION\_描述符**](https://msdn.microsoft.com/library/windows/hardware/ff537688)结构来描述其内部的拓扑。 微型端口驱动程序显示在此数组[ **PCFILTER\_描述符**](https://msdn.microsoft.com/library/windows/hardware/ff537694)结构，它将输出从[ **IMiniport::GetDescription**](https://msdn.microsoft.com/library/windows/hardware/ff536765)方法。 该数组指定拓扑为拓扑筛选器的节点和 pin 之间的连接的列表 (请参阅[节点和连接](nodes-and-connections.md))。 [WDMAud 系统驱动程序](user-mode-wdm-audio-components.md#wdmaud_system_driver)转换 mixer 直线和 mixer API 向应用程序公开的控件为这些连接和节点。 如中所述[音频筛选器](audio-filters.md)、 输入插针上 KS 筛选器将映射到 SRC 混音器行中，并将固定到一个输出筛选器映射到 DST 混音器行。

典型的音频适配器可以播放波形文件和通过演讲者，MIDI 文件，这样可以捕获音频信号从麦克风和 MIDI 合成器。 下面的代码示例包含 PCCONNECTION\_公开这些功能的拓扑筛选器描述符数组：

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

常量[ **PCFILTER\_节点**](https://msdn.microsoft.com/library/windows/hardware/ff537695)在前面的代码示例是空的节点 ID 和头文件 Portcls.h 中定义。 有关如何使用此常量来将筛选器上的外部 pin 与逻辑引脚节点上区分开来的说明，请参阅[ **PCCONNECTION\_描述符**](https://msdn.microsoft.com/library/windows/hardware/ff537688)。

在前面的代码示例中的每个 pin 名称结尾"SRC"或"DST"具体取决于 mixer API 是否映射到源或目标的混音器行的 pin。 若要避免混淆，请记住，源和目标 mixer 分别行映射到接收器 （输入） 和源 （输出） KS 筛选器插针，。 有关详细信息，请参阅[音频筛选器](audio-filters.md)。

PCCONNECTION\_描述符数组在前面的代码示例介绍下图中的拓扑筛选器。

![说明通过 pcconnection 所述的拓扑筛选器连接的关系图\-描述符数组](images/topofilt.png)

在图中的拓扑筛选器在左侧具有四个输入 （接收器） 插针和两个输出 （源） 右侧的插针。 前两个输入插针和顶部输出插针连接使用的数据路径混合已呈现的批和正在播放的 MIDI 流从两个模拟信号。 数据路径下两个输入插针和底部输出插针连接多路复用记录捕获模拟信号。

四个输入插针，如下所示操作：

-   KSPIN\_TOPO\_WAVEOUT\_SRC pin 以物理方式连接到批筛选器，用于呈现.wav 文件，以生成在 pin 模拟信号等源中的批流的输出插针。

-   KSPIN\_TOPO\_SYNTHOUT\_SRC pin 以物理方式连接到合成器筛选器，它可能会呈现，例如，来自源如.mid 文件以生成在 pin 模拟信号的 MIDI 流的输出插针。

-   KSPIN\_TOPO\_SYNTHIN\_SRC pin 以物理方式连接到生成模拟信号合成器。 （请注意更实用的硬件设计可能会从 MPU 401 MIDI 接口获取 MIDI 输入的流并将其转换为声波格式，完全跳过拓扑筛选器直接）。

-   KSPIN\_TOPO\_MIC\_SRC pin 以物理方式连接到采用模拟信号从麦克风输入插孔。

两个输出插针，如下所示操作：

-   KSPIN\_TOPO\_线路输出\_DST pin 以物理方式连接到通常驱动器的说话人的一组模拟线路输出插孔。

-   KSPIN\_TOPO\_WAVEIN\_DST pin 以物理方式连接到批筛选器，它将模拟信号转换为批流并将其写入到如.wav 文件的目标的输入插针。

卷和静音节点 (请参阅[ **KSNODETYPE\_卷**](https://msdn.microsoft.com/library/windows/hardware/ff537208)并[ **KSNODETYPE\_设为静音**](https://msdn.microsoft.com/library/windows/hardware/ff537178)) 经常使用控制各种流音量级别。 SUM 节点 (请参阅[ **KSNODETYPE\_SUM**](https://msdn.microsoft.com/library/windows/hardware/ff537196)) 混合使用批和 MIDI 输入音频流。 MUX 节点 (请参阅[ **KSNODETYPE\_MUX**](https://msdn.microsoft.com/library/windows/hardware/ff537180)) 选择两个输入流之间。

图中使用的虚线的箭头指示两个节点之间或 pin 与节点之间的连接。 箭头指向数据流的方向。 该图显示了其中每个对应于一个在 PCCONNECTION 13 个元素的 13 连接，总共\_描述符数组在前面的代码示例。

除了拓扑筛选器，适配器驱动程序创建其他筛选器-批、 FM 合成器、 批表等-连接到拓扑筛选器上的针。

例如，批筛选器以物理方式连接到拓扑筛选器的 KSPIN\_TOPO\_WAVEOUT\_SRC pin 包含 DAC (由[ **KSNODETYPE\_DAC**](https://msdn.microsoft.com/library/windows/hardware/ff537158)节点) 以便将其输出到拓扑筛选器的 pin 模拟信号转换为 PCM 数据。 FM 合成或波表合成器筛选器以物理方式连接到拓扑筛选器的 KSPIN\_TOPO\_SYNTHOUT\_SRC pin 同样将 MIDI 数据转换为模拟信号，它将输出到拓扑筛选器的 pin。 拓扑筛选器将混合这两个 pin 从模拟信号，并输出混合到扬声器信号。

与其他筛选器表示相同的适配器卡上的其他硬件设备的拓扑筛选器的物理连接需要区别于其他类型的连接到筛选器。 例如，某些插针上批、 MIDI 和 DirectMusic 筛选器可以连接或断开连接下软件控制。

设备在启动期间，适配器驱动程序注册拓扑筛选器的物理连接通过调用[ **PcRegisterPhysicalConnection** ](https://msdn.microsoft.com/library/windows/hardware/ff537726)一次每个连接。 端口驱动程序需要此信息以响应[ **KSPROPERTY\_PIN\_PHYSICALCONNECTION** ](https://msdn.microsoft.com/library/windows/hardware/ff565205)获取属性的请求。

 

 




