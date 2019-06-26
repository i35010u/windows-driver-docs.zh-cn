---
title: 公开硬件加速捕获效果
description: 公开硬件加速捕获效果
ms.assetid: 032139e8-e758-4d63-b8c1-ca61c958b20b
keywords:
- 干扰抑制 WDK 音频
- NS WDK 音频
- 硬件加速 WDK DirectSound，捕获效果
- 硬件加速捕获 WDK 音频效果
- 回声取消 WDK 音频
- AEC WDK 音频
- 节点链 WDK 音频
- 节点排序要求 WDK DirectSound
- 逻辑引脚 WDK 音频
- 节点 pin 分配 WDK 音频
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e468778cb3f2c2fb52071bce94e683c190586cae
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67360060"
---
# <a name="exposing-hardware-accelerated-capture-effects"></a>公开硬件加速捕获效果


## <span id="exposing_hardware_accelerated_capture_effects"></span><span id="EXPOSING_HARDWARE_ACCELERATED_CAPTURE_EFFECTS"></span>


在 Windows XP 及更高版本，WDM 音频框架还支持通过 DirectSound 公开的音频捕获效果的硬件加速。 这些效果包括回声抵消 (AEC) 和干扰抑制 (NS)。 有关 DirectSoundCapture 应用程序如何通过使用硬件加速的 AEC 和 NS 的信息，请参阅 Microsoft Windows SDK 文档。

微型端口驱动程序可以公开这些效果，具体取决于基础设备的功能的任何子集的硬件加速。 若要公开的 AEC 和 NS 效果的硬件的功能，每个插针上 AEC 筛选，该驱动程序实现可以满足这些要求：

-   Pin 应包括在其节点链来表示每个硬件效果要合并到关系图中的单个节点。 由以下 Guid 指定 AEC 和 NS 效果 KS 节点类型：[**KSNODETYPE\_声学\_ECHO\_取消**](https://docs.microsoft.com/windows-hardware/drivers/audio/ksnodetype-acoustic-echo-cancel)
    [**KSNODETYPE\_干扰\_禁止**](https://docs.microsoft.com/windows-hardware/drivers/audio/ksnodetype-noise-suppress)
-   支持的插针的 AEC 和 NS 节点应[KSPROPSETID\_常规](https://docs.microsoft.com/windows-hardware/drivers/stream/kspropsetid-general)属性设置，应提供有关查询时的制造商信息[ **KSPROPERTY\_常规\_COMPONENTID** ](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-general-componentid)属性。

-   支持的插针的 AEC 和 NS 节点应[KSPROPSETID\_TopologyNode](https://docs.microsoft.com/windows-hardware/drivers/audio/kspropsetid-topologynode)属性集和其两个属性：

    [**KSPROPERTY\_TOPOLOGYNODE\_启用**](https://docs.microsoft.com/windows-hardware/drivers/audio/ksproperty-topologynode-enable)启用影响。

    [**KSPROPERTY\_TOPOLOGYNODE\_重置**](https://docs.microsoft.com/windows-hardware/drivers/audio/ksproperty-topologynode-reset)将效果重置为其默认状态。

-   插针的 AEC 和 NS 节点应支持的以下属性[KSPROPSETID\_音频](https://docs.microsoft.com/windows-hardware/drivers/audio/kspropsetid-audio)属性集：[**KSPROPERTY\_音频\_CPU\_资源**](https://docs.microsoft.com/windows-hardware/drivers/audio/ksproperty-audio-cpu-resources)
    [**KSPROPERTY\_音频\_算法\_实例**](https://docs.microsoft.com/windows-hardware/drivers/audio/ksproperty-audio-algorithm-instance)
-   Pin 应支持以下属性的 KSPROPSETID\_音频属性集：[**KSPROPERTY\_音频\_位置**](https://docs.microsoft.com/windows-hardware/drivers/audio/ksproperty-audio-position)
    [**KSPROPERTY\_音频\_延迟**](https://docs.microsoft.com/windows-hardware/drivers/audio/ksproperty-audio-latency)
-   Pin 应公开其数据范围功能 (请参阅[Pin 数据范围和交集属性](pin-data-range-and-intersection-properties.md))。

下面提供用于公开硬件加速的 AEC 和 NS 节点的特定要求。

### <a name="span-idacousticechocancellationspanspan-idacousticechocancellationspanspan-idacousticechocancellationspanacoustic-echo-cancellation"></a><span id="Acoustic_Echo_Cancellation"></span><span id="acoustic_echo_cancellation"></span><span id="ACOUSTIC_ECHO_CANCELLATION"></span>回声

PCM 微型端口驱动程序公开的这两个捕获的拓扑形式的 AEC 的硬件支持，并呈现流满足此附加要求：

-   Pin 必须包含一个 AEC 节点 ([**KSNODETYPE\_声学\_ECHO\_取消**](https://docs.microsoft.com/windows-hardware/drivers/audio/ksnodetype-acoustic-echo-cancel))，必须在已排序的节点链 （请参阅中的正确位置中指定的下图）。

### <a name="span-idnoisesuppressionspanspan-idnoisesuppressionspanspan-idnoisesuppressionspannoise-suppression"></a><span id="Noise_Suppression"></span><span id="noise_suppression"></span><span id="NOISE_SUPPRESSION"></span>干扰禁止显示

PCM 微型端口驱动程序公开形式为满足此附加要求的捕获流的拓扑的 NS 硬件的支持：

-   Pin 必须包含 NS 节点 ([**KSNODETYPE\_干扰\_禁止**](https://docs.microsoft.com/windows-hardware/drivers/audio/ksnodetype-noise-suppress))，必须在已排序的节点链 （见下文） 中正确的位置中指定的。

### <a name="span-idnode-chainorderingspanspan-idnode-chainorderingspanspan-idnode-chainorderingspannode-chain-ordering"></a><span id="Node-Chain_Ordering"></span><span id="node-chain_ordering"></span><span id="NODE-CHAIN_ORDERING"></span>节点链排序

目前，DirectSound 捕获效果体系结构要求的应用程序请求的顺序指定节点。 结果是，在其中微型端口驱动程序指定其节点的顺序的顺序必须匹配，由[AEC 系统筛选器](aec-system-filter.md)(Aec.sys)，它可实现的 AEC 和 NS 算法在软件中。

若要启用硬件加速，驱动程序必须指定由按以下顺序的硬件实现的效果：

[**KSNODETYPE\_ADC**](https://docs.microsoft.com/windows-hardware/drivers/audio/ksnodetype-adc)

[**KSNODETYPE\_ACOUSTIC\_ECHO\_CANCEL**](https://docs.microsoft.com/windows-hardware/drivers/audio/ksnodetype-acoustic-echo-cancel)

[**KSNODETYPE\_干扰\_禁止**](https://docs.microsoft.com/windows-hardware/drivers/audio/ksnodetype-noise-suppress)

请注意，此列表可以忽略任何未实现的效果，只要保留相对顺序。

### <a name="span-idaecnodepinassignmentsspanspan-idaecnodepinassignmentsspanspan-idaecnodepinassignmentsspanaec-node-pin-assignments"></a><span id="AEC_Node_Pin_Assignments"></span><span id="aec_node_pin_assignments"></span><span id="AEC_NODE_PIN_ASSIGNMENTS"></span>AEC 节点 Pin 分配

适配器驱动程序使用的数组[ **PCCONNECTION\_描述符**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff537688(v=vs.85))结构，以指定内部筛选器的连接。 每个数组元素描述一个连接，可以是节点到节点、 节点 pin 或 pin 的 pin。 有关详细信息，请参阅[节点和连接](nodes-and-connections.md)。

若要使用 PCCONNECTION\_描述符结构，则驱动程序编写器会将"逻辑"插针分配给节点。 这些节点本身上是"固定"，仅用于指定在筛选器内部的连接。 这是与筛选器，用于连接到其他筛选器的外部 pin。

下表显示了适配器驱动程序应将分配到四个逻辑引脚 AEC 节点上的多个 pin Id。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Pin ID 参数名称</th>
<th align="left">ReplTest1</th>
<th align="left">含义</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>KSNODEPIN_AEC_RENDER_IN</p></td>
<td align="left"><p>1</p></td>
<td align="left"><p>为呈现的流式传输接收器 pin （节点输入）</p></td>
</tr>
<tr class="even">
<td align="left"><p>KSNODEPIN_AEC_RENDER_OUT</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>源 pin 码 （节点输出） 以进行呈现流</p></td>
</tr>
<tr class="odd">
<td align="left"><p>KSNODEPIN_AEC_CAPTURE_IN</p></td>
<td align="left"><p>2</p></td>
<td align="left"><p>接收器为捕获的流的 pin （节点输入）</p></td>
</tr>
<tr class="even">
<td align="left"><p>KSNODEPIN_AEC_CAPTURE_OUT</p></td>
<td align="left"><p>3</p></td>
<td align="left"><p>为捕获的流的源 pin （节点输出）</p></td>
</tr>
</tbody>
</table>

 

上表中的 pin Id 标头文件 Ksmedia.h 中定义。

下面的代码示例演示如何适配器驱动程序可以指定包含 AEC 节点和 NS 节点的 AEC 筛选器的内部拓扑：

```cpp
    // AEC Filter Topology

    // Pin IDs for external pins on AEC filter
    #define ID_CaptureOutPin   0   // microphone stream
    #define ID_CaptureInPin    1
    #define ID_RenderOutPin    2   // speaker stream
    #define ID_RenderInPin     3

    // Generic pin IDs for simple node with one input and one output
    #define NODE_INPUT_PIN     1
    #define NODE_OUTPUT_PIN    0

    // Node IDs
    #define NODE_ID_AEC        0   // acoustic echo cancellation
    #define NODE_ID_NS         1   // noise suppression

    // The array below defines the internal topology of an
    // AEC filter that contains an AEC node and an NS node.

    const PCCONNECTION_DESCRIPTOR AecConnections[] = {
        { PCFILTER_NODE, ID_RenderInPin,       NODE_ID_AEC,    KSNODEPIN_AEC_RENDER_IN  },
        { NODE_ID_AEC,   KSNODEPIN_AEC_RENDER_OUT,   PCFILTER_NODE,  ID_RenderOutPin    },
        { PCFILTER_NODE, ID_CaptureInPin,      NODE_ID_AEC,    KSNODEPIN_AEC_CAPTURE_IN },
        { NODE_ID_AEC,   KSNODEPIN_AEC_CAPTURE_OUT,  NODE_ID_NS,     NODE_INPUT_PIN     },
        { NODE_ID_NS,    NODE_OUTPUT_PIN,      PCFILTER_NODE,  ID_CaptureOutPin   }
    };
```

在前面的代码示例的 AecConnections 数组定义下图中所示的筛选器拓扑。

![说明 aec 筛选器的内部拓扑关系图](images/aectopo.png)

上图中表示带虚线箭头的数据流方向的筛选器内的每个连接。 在图中显示总共五个连接。 每个连接对应于一个 AecConnections 数组中的代码示例中的五个元素。

 

 




