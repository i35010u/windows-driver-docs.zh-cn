---
title: 公开筛选器拓扑
description: 公开筛选器拓扑
ms.assetid: bf791f40-b2fb-48fe-8350-3b926db4ead7
keywords:
- 拓扑 WDK 音频筛选器
- 筛选拓扑 WDK 音频
- KS 筛选器 WDK 音频，拓扑
- 公开筛选拓扑
- 音频筛选器 WDK 音频，公开拓扑
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cbc0366e3fde41496139f495285a0b88ea6d87f4
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67360055"
---
# <a name="exposing-filter-topology"></a>公开筛选器拓扑


## <span id="exposing_filter_topology"></span><span id="EXPOSING_FILTER_TOPOLOGY"></span>


微型端口驱动程序介绍在 pin、 节点和连接方面的 KS 筛选器的内部拓扑。 此拓扑指定通过筛选器的数据流路径，并还定义了逻辑目标-pin 和节点--属性请求。 内部筛选器拓扑是硬件设备的基础筛选器的内部结构的逻辑表示形式。 微型端口驱动程序描述了此拓扑中使用的 pin、 节点和连接描述符的静态数组。

-   静态数组中指定的 pin [ **PCPIN\_描述符**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/ns-portcls-pcpin_descriptor)结构。 每个 pin 已是数组中的其序号的 ID。

-   节点的静态数组中指定[ **PCNODE\_描述符**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/ns-portcls-pcnode_descriptor)结构。 每个节点都有其序号数组中的 ID。

-   连接 （pin pin，pin 节点或节点到节点） 的静态数组中指定[ **PCCONNECTION\_描述符**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff537688(v=vs.85))结构。

微型端口驱动程序公开这些中的三个数组[ **PCFILTER\_描述符**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/ns-portcls-pcfilter_descriptor)结构，它将输出从其[ **IMiniport::GetDescription** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-iminiport-getdescription)方法。

### <a name="span-idexamplespanspan-idexamplespanspan-idexamplespanexample"></a><span id="Example"></span><span id="example"></span><span id="EXAMPLE"></span>示例

下面的代码示例指定一个具有一个输入插针和一个输出插针的简单 KS 筛选器的内部拓扑。 筛选器包含单个节点，这是卷级别控制。

```cpp
#define KSPIN_WAVEOUT_SRC  0
#define KSPIN_SPEAKERS_DST  1

PCPIN_DESCRIPTOR 
MiniportPins[] =
{
    {   // Pin 0 -- KSPIN_WAVEOUT_SRC
        0,0,0,  // InstanceCount
        NULL,   // AutomationTable
        {       // KsPinDescriptor
            0,                                          // InterfacesCount
            NULL,                                       // Interfaces
            0,                                          // MediumsCount
            NULL,                                       // Mediums
            SIZEOF_ARRAY(PinDataRangePointersBridge),   // DataRangesCount
            PinDataRangePointersBridge,                 // DataRanges
            KSPIN_DATAFLOW_IN,                          // DataFlow
            KSPIN_COMMUNICATION_NONE,                   // Communication
            &KSNODETYPE_LEGACY_AUDIO_CONNECTOR,         // Category
            NULL,                                       // Name
            0                                           // Reserved
        }
    },
    {   // Pin 1 -- KSPIN_SPEAKERS_DST
        0,0,0,  // InstanceCount
        NULL,   // AutomationTable
        {       // KsPinDescriptor
            0,                                          // InterfacesCount
            NULL,                                       // Interfaces
            0,                                          // MediumsCount
            NULL,                                       // Mediums
            SIZEOF_ARRAY(PinDataRangePointersBridge),   // DataRangesCount
            PinDataRangePointersBridge,                 // DataRanges
            KSPIN_DATAFLOW_OUT,                         // DataFlow
            KSPIN_COMMUNICATION_NONE,                   // Communication
            &KSNODETYPE_SPEAKER,                        // Category
            &KSAUDFNAME_VOLUME_CONTROL,                 // Name (This name shows up as the 
                                                        // playback panel name in SndVol32)
            0                                           // Reserved
        }
    }
};

#define KSNODE_WAVEOUT_VOLUME  0

PCNODE_DESCRIPTOR TopologyNodes[] =
{
    {   // KSNODE_WAVEOUT_VOLUME
        0,                      // Flags
        &AutomationVolume,      // AutomationTable
        &KSNODETYPE_VOLUME,     // Type
        &KSAUDFNAME_WAVE_VOLUME // Name
    }
};

PCCONNECTION_DESCRIPTOR MiniportConnections[] =
{ //FromNode---------------FromPin------------ToNode-----------------ToPin
  { PCFILTER_NODE,         KSPIN_WAVEOUT_SRC, KSNODE_WAVEOUT_VOLUME, 1 },
  { KSNODE_WAVEOUT_VOLUME, 0,                 PCFILTER_NODE,         KSPIN_SPEAKERS_DST }
};
```

下图显示了筛选器前面的示例代码所述的拓扑。

![说明一个简单的筛选器拓扑关系图](images/audtop.png)

此筛选器是一个简单的示例[拓扑筛选器](topology-filters.md)，该适配器驱动程序通过将绑定窗体及其[IMiniportTopology](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-iminiporttopology)对象传递给[IPortTopology](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-iporttopology)对象PortCls 系统驱动程序创建。 筛选器的输入 （接收器） 和输出 （源） 插针名为 KSPIN\_WAVEOUT\_SRC 和 KSPIN\_扬声器\_DST。 这两个插针执行模拟信号。 **Mixer** API 公开为源和目标 mixer 线条这些引脚的连接 (MIXERLINE\_COMPONENTTYPE\_SRC\_WAVEOUT 和 MIXERLINE\_COMPONENTTYPE\_DST\_扬声器) 分别。

当讨论到 mixer 行 KS pin 的映射时下, 表说明了困惑的潜在来源。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Pin 名称</th>
<th align="left">Mixer API 术语</th>
<th align="left">KS 筛选器术语</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>KSPIN_WAVEOUT_SRC</p></td>
<td align="left"><p>源混音器行</p></td>
<td align="left"><p>接收器 pin</p></td>
</tr>
<tr class="even">
<td align="left"><p>KSPIN_SPEAKERS_DST</p></td>
<td align="left"><p>目标混音器行</p></td>
<td align="left"><p>源 pin</p></td>
</tr>
</tbody>
</table>

 

请注意该 KSPIN\_WAVEOUT\_SRC 是源 mixer 行、 和 KSPIN\_扬声器\_DST 是源 pin。 有关详细信息，请参阅 KS 和 mixer 行中的术语的讨论[音频 Mixer API 转换到内核流式处理拓扑](kernel-streaming-topology-to-audio-mixer-api-translation.md)。

另请注意，名称"KSPIN\_WAVEOUT\_SRC"包含"WAVEOUT"不是因为 pin 携带波形格式的数字数据，而是因为它会执行生成的批筛选器，这是筛选器类型 WaveCyclic 模拟信号或WavePci。 批筛选器表示的批流转换为模拟信号的音频适配器的硬件的一部分。 将固定 KSPIN\_扬声器\_DST 输出驱动器的说话人的一组模拟信号。

筛选器包含单个节点，KSNODE\_WAVEOUT\_卷，其中**mixer** API 表示作为音量控件 (MIXERCONTROL\_CONTROLTYPE\_卷)。 音量控制 KS 节点类型是[ **KSNODETYPE\_卷**](https://docs.microsoft.com/windows-hardware/drivers/audio/ksnodetype-volume)。 所有节点，此都类型支持[ **KSPROPERTY\_音频\_VOLUMELEVEL** ](https://docs.microsoft.com/windows-hardware/drivers/audio/ksproperty-audio-volumelevel)属性，该筛选器的客户端使用来控制音量级别属性。

卷节点都有两个"逻辑"pin 编号的 0 和 1。 在图中 MiniportConnections 数组由指定的两个连接由指向数据流的方向的虚线箭头表示。 一个数组中的两个元素描述每个连接。

KSPIN\_WAVEOUT\_SRC 和 KSPIN\_扬声器\_DST pin 都*桥接 pin*，这意味着它们表示适配器中的硬编码连接。 在前面的示例代码，这两个 MiniportPins 数组中的两个 pin 描述符其 IRP 流方向指定为 KSPIN\_通信\_NONE，非常适合，因为桥 pin 既不发送也不接收 Irp。 两个 pin 描述符还指 PinDataRangePointersBridge 数组，其定义，如下所示：

```cpp
static KSDATARANGE PinDataRangesBridge[] =
{
   {
      sizeof(KSDATARANGE),
      0, 0, 0,
      STATICGUIDOF(KSDATAFORMAT_TYPE_AUDIO),
      STATICGUIDOF(KSDATAFORMAT_SUBTYPE_ANALOG),
      STATICGUIDOF(KSDATAFORMAT_SPECIFIER_NONE)
   }
};

static PKSDATARANGE PinDataRangePointersBridge[] =
{
    &PinDataRangesBridge[0]
};
```

PinDataRangePointersBridge 数组定义桥 pin 携带模拟音频信号的数据范围。 有关详细信息，请参阅中的桥 pin 讨论[音频筛选器关系图](audio-filter-graphs.md)。

有关更复杂的拓扑的示例，请参阅[拓扑筛选器](topology-filters.md)。

 

 




