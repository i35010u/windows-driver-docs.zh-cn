---
title: 公开筛选器拓扑
description: 公开筛选器拓扑
ms.assetid: bf791f40-b2fb-48fe-8350-3b926db4ead7
keywords:
- 拓扑筛选 WDK 音频
- 筛选拓扑 WDK 音频
- KS 筛选 WDK 音频、拓扑
- 公开筛选器拓扑
- 音频筛选 WDK 音频，露出拓扑
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 891efe8ca31977fc78cf2a5e7cd7ac8a6f137881
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89208033"
---
# <a name="exposing-filter-topology"></a>公开筛选器拓扑


## <span id="exposing_filter_topology"></span><span id="EXPOSING_FILTER_TOPOLOGY"></span>


微型端口驱动程序根据 pin、节点和连接来描述 KS 筛选器的内部拓扑。 此拓扑通过筛选器指定数据流路径，并且还为属性请求定义逻辑目标--pin 和节点。 筛选器内拓扑是筛选器的基础硬件设备的内部结构的逻辑表示形式。 微型端口驱动程序通过静态数组的 pin、节点和连接描述符描述此拓扑。

-   Pin 在 [**PCPIN \_ 描述符**](/windows-hardware/drivers/ddi/portcls/ns-portcls-pcpin_descriptor) 结构的静态数组中指定。 每个 pin 的 ID 都是其在数组中的序号。

-   节点在 [**PCNODE \_ 描述符**](/windows-hardware/drivers/ddi/portcls/ns-portcls-pcnode_descriptor) 结构的静态数组中指定。 每个节点的 ID 都是其在数组中的序号。

-   连接 (插针、固定到节点或节点到节点) 在 [**PCCONNECTION \_ 描述符**](/previous-versions/windows/hardware/drivers/ff537688(v=vs.85)) 结构的静态数组中指定。

微型端口驱动程序在从其[**IMiniport：： GetDescription**](/windows-hardware/drivers/ddi/portcls/nf-portcls-iminiport-getdescription)方法输出的[**PCFILTER \_ 描述符**](/windows-hardware/drivers/ddi/portcls/ns-portcls-pcfilter_descriptor)结构中公开这三个数组。

### <a name="span-idexamplespanspan-idexamplespanspan-idexamplespanexample"></a><span id="Example"></span><span id="example"></span><span id="EXAMPLE"></span>实例

下面的代码示例指定简单 KS 筛选器的内部拓扑，其中包含一个输入插针和一个输出插针。 筛选器包含单个节点，该节点是一个卷级控件。

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

下图显示了前面的示例代码描述的筛选器的拓扑。

![阐释简单筛选器拓扑的关系图](images/audtop.png)

此筛选器是一个简单的 [拓扑筛选器](topology-filters.md)示例，适配器驱动程序通过将其 [IMiniportTopology](/windows-hardware/drivers/ddi/portcls/nn-portcls-iminiporttopology) 对象绑定到 PortCls 系统驱动程序创建的 [IPortTopology](/windows-hardware/drivers/ddi/portcls/nn-portcls-iporttopology) 对象来形成。 筛选器的输入 (接收器) 和输出 (源) pin 的名称为 KSPIN \_ WAVEOUT \_ SRC 和 KSPIN \_ 发言人 \_ DST。 这两个针脚都带有模拟信号。 **混音**器 API 将这些引脚的连接公开为源和目标混合器行 (MIXERLINE \_ COMPONENTTYPE \_ SRC \_ WAVEOUT 和 MIXERLINE \_ COMPONENTTYPE \_ DST \_ 发言人) 。

下表说明了讨论 KS 引脚到混音器线的映射时可能会造成混淆的原因。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">引脚名称</th>
<th align="left">混音器 API 术语</th>
<th align="left">KS 筛选器术语</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>KSPIN_WAVEOUT_SRC</p></td>
<td align="left"><p>源混合器行</p></td>
<td align="left"><p>接收器 pin</p></td>
</tr>
<tr class="even">
<td align="left"><p>KSPIN_SPEAKERS_DST</p></td>
<td align="left"><p>目标混合器行</p></td>
<td align="left"><p>源 pin</p></td>
</tr>
</tbody>
</table>

 

请注意，KSPIN \_ WAVEOUT \_ SRC 是源混合器行，KSPIN \_ 扬声器 \_ DST 是源 pin。 有关详细信息，请参阅将内核流式处理拓扑中的 KS 和混音器行术语讨论 [到音频混音器 API 翻译](kernel-streaming-topology-to-audio-mixer-api-translation.md)。

另请注意，名称 "KSPIN \_ WAVEOUT \_ SRC" 不包含 "WAVEOUT"，这是因为 pin 携带了波形格式数字数据，但由于它携带了由波形筛选器生成的模拟信号，因此它是 WaveCyclic 或 WavePci 类型的筛选器。 波形筛选器表示音频适配器硬件的一部分，它将波形流转换为模拟信号。 Pin KSPIN \_ 扬声器 \_ DST 会输出驱动一组扬声器的模拟信号。

筛选器包含单一节点 KSNODE \_ WAVEOUT \_ volume，其中， **混音** 器 API 将它表示为 (MIXERCONTROL \_ CONTROLTYPE volume) 的卷控制 \_ 。 卷控件的 KS 节点类型为 [**KSNODETYPE \_ 卷**](./ksnodetype-volume.md)。 此类型的所有节点都支持 [**KSPROPERTY \_ AUDIO \_ VOLUMELEVEL**](./ksproperty-audio-volumelevel.md) 属性，筛选器的客户端使用该属性控制卷级别。

卷节点具有两个 "逻辑" 引脚，编号为0和1。 由 MiniportConnections 数组指定的两个连接由点沿数据流方向的虚线箭头表示。 数组中的两个元素之一描述每个连接。

KSPIN \_ WAVEOUT \_ SRC 和 KSPIN \_ 扬声器 \_ DST 引脚均为 *桥接 pin*，这意味着它们代表适配器中的硬编码连接。 在上面的示例代码中，MiniportPins 数组中的两个 pin 说明符都将 IRP 流方向指定为 KSPIN \_ 通信 \_ NONE，这种情况非常合适，因为桥插不发送也不接收 irp。 这两个 pin 描述符还引用了 PinDataRangePointersBridge 数组，定义如下：

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

PinDataRangePointersBridge 数组定义带有模拟音频信号的桥接的数据范围。 有关详细信息，请参阅 [音频筛选器图形](audio-filter-graphs.md)中的桥接程序讨论。

有关更复杂拓扑的示例，请参阅 [拓扑筛选器](topology-filters.md)。

 

