---
title: 公开硬件加速捕获效果
description: 公开硬件加速捕获效果
ms.assetid: 032139e8-e758-4d63-b8c1-ca61c958b20b
keywords:
- 干扰声音频
- NS WDK 音频
- 硬件加速 WDK DirectSound，捕获效果
- 硬件加速捕获效果 WDK 音频
- 回声抵消乐曲音频
- AEC WDK 音频
- 节点链接 WDK 音频
- 节点顺序要求 WDK DirectSound
- 逻辑引脚 WDK 音频
- 节点 pin 分配 WDK 音频
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6322a0c2e7da665e0f5f75af058148c066201fa7
ms.sourcegitcommit: 372464be981a39781c71049126f36891cb5d0cad
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2020
ms.locfileid: "91646003"
---
# <a name="exposing-hardware-accelerated-capture-effects"></a>公开硬件加速捕获效果


## <span id="exposing_hardware_accelerated_capture_effects"></span><span id="EXPOSING_HARDWARE_ACCELERATED_CAPTURE_EFFECTS"></span>


在 Windows XP 和更高版本中，WDM 音频框架支持通过 DirectSound 公开的音频捕获效果的硬件加速。 这些影响包括) 的声音回声取消 ( (NS) 的干扰。 有关 DirectSoundCapture 应用程序如何允许使用硬件加速的 AEC 和 NS 的信息，请参阅 Microsoft Windows SDK 文档。

小型端口驱动程序可以根据基础设备的功能，为这些效果的任何子集公开硬件加速。 若要为 AEC 和 NS 的影响提供硬件功能，驱动程序实现的 AEC 筛选器上的每个 pin 应满足以下要求：

-   Pin 应在其节点链中包含一个单独的节点，用于表示要并入图形中的每个硬件效果。 AEC 和 NS 的 KS 节点类型的影响由以下 guid 指定： [**KSNODETYPE \_ \_ \_ **](./ksnodetype-acoustic-echo-cancel.md) 
     [** \_ \_ **](./ksnodetype-noise-suppress.md)
-   Pin 上的 AEC 和 NS 节点应支持 [KSPROPSETID \_ 常规](../stream/kspropsetid-general.md) 属性集，并应在查询 [**KSPROPERTY \_ 常规 \_ 组件 id**](../stream/ksproperty-general-componentid.md) 属性时提供有关制造商的信息。

-   Pin 上的 AEC 和 NS 节点应支持 [KSPROPSETID \_ TopologyNode](./kspropsetid-topologynode.md) 属性集及其两个属性：

    [**KSPROPERTY \_TOPOLOGYNODE \_ ENABLE**](./ksproperty-topologynode-enable.md) 启用了效果。

    [**KSPROPERTY \_TOPOLOGYNODE \_ RESET**](./ksproperty-topologynode-reset.md) 会将效果重置为其默认状态。

-   Pin 上的 AEC 和 NS 节点应支持[KSPROPSETID \_ audio](./kspropsetid-audio.md)属性集的以下属性： [**KSPROPERTY \_ audio \_ CPU \_ RESOURCES**](./ksproperty-audio-cpu-resources.md) 
     [**KSPROPERTY \_ 音频 \_ 算法 \_ 实例**](./ksproperty-audio-algorithm-instance.md)
-   Pin 应支持 KSPROPSETID audio 属性集的以下属性 \_ ： [**KSPROPERTY \_ audio \_ POSITION**](./ksproperty-audio-position.md) 
     [**KSPROPERTY \_ 音频 \_ 延迟**](./ksproperty-audio-latency.md)
-   Pin 应公开其数据范围功能 (请参阅 [固定数据范围和交集属性](pin-data-range-and-intersection-properties.md)) 。

下面提供了公开硬件加速 AEC 和 NS 节点的特定要求。

### <a name="span-idacoustic_echo_cancellationspanspan-idacoustic_echo_cancellationspanspan-idacoustic_echo_cancellationspanacoustic-echo-cancellation"></a><span id="Acoustic_Echo_Cancellation"></span><span id="acoustic_echo_cancellation"></span><span id="ACOUSTIC_ECHO_CANCELLATION"></span>回声取消

PCM 微型端口驱动程序以拓扑的形式为满足此附加要求的捕获和呈现流公开硬件支持：

-   Pin 必须包含 AEC 节点 (KSNODETYPE " [** \_ 声音 \_ 回声" \_ 取消**](./ksnodetype-acoustic-echo-cancel.md)) ，该节点必须在已排序的节点链中的适当位置进行指定 (参见下面的 ") "。

### <a name="span-idnoise_suppressionspanspan-idnoise_suppressionspanspan-idnoise_suppressionspannoise-suppression"></a><span id="Noise_Suppression"></span><span id="noise_suppression"></span><span id="NOISE_SUPPRESSION"></span>干扰性抑制

PCM 微型端口驱动程序以捕获流的拓扑形式为满足此附加要求的拓扑公开硬件支持：

-   Pin 必须包括一个 NS 节点 ([**KSNODETYPE \_ 噪声 \_ 禁止显示**](./ksnodetype-noise-suppress.md)) ，必须在有序的节点链中的适当位置指定该， (参见下面的) 。

### <a name="span-idnode-chain_orderingspanspan-idnode-chain_orderingspanspan-idnode-chain_orderingspannode-chain-ordering"></a><span id="Node-Chain_Ordering"></span><span id="node-chain_ordering"></span><span id="NODE-CHAIN_ORDERING"></span>节点链排序

目前，DirectSound 的捕获效果体系结构要求按应用程序请求的顺序指定节点。 因此，微型端口驱动程序指定其节点的顺序必须与 [AEC 系统筛选器](aec-system-filter.md) 所使用的顺序相匹配 ( # A0) ，它在软件中实现 AEC 和 NS 算法。

若要启用硬件加速，驱动程序必须按以下顺序指定硬件实现的效果：

[**KSNODETYPE \_ ADC**](./ksnodetype-adc.md)

[**KSNODETYPE \_ 回声 \_ \_ 取消**](./ksnodetype-acoustic-echo-cancel.md)

[**KSNODETYPE \_ 干扰 \_**](./ksnodetype-noise-suppress.md)

请注意，只要保留相对排序，此列表就可以省略任何未实现的效果。

### <a name="span-idaec_node_pin_assignmentsspanspan-idaec_node_pin_assignmentsspanspan-idaec_node_pin_assignmentsspanaec-node-pin-assignments"></a><span id="AEC_Node_Pin_Assignments"></span><span id="aec_node_pin_assignments"></span><span id="AEC_NODE_PIN_ASSIGNMENTS"></span>AEC 节点 Pin 分配

适配器驱动程序使用 [**PCCONNECTION \_ 描述符**](/windows-hardware/drivers/ddi/portcls/ns-portcls-_pcconnection_descriptor) 结构的数组指定筛选器中的连接。 每个数组元素描述一个连接，该连接可以是节点到节点、节点到 pin 或 pin 到 pin。 有关详细信息，请参阅 [节点和连接](nodes-and-connections.md)。

若要使用 PCCONNECTION \_ 描述符结构，驱动程序编写器会将 "逻辑" pin 分配给节点。 这些是节点本身的 "固定"，只用于指定筛选器内的连接。 这与用于连接到其他筛选器的筛选器上的外部 pin 不同。

下表显示了适配器驱动程序应分配给 AEC 节点上四个逻辑针的 pin Id。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Pin ID 参数名称</th>
<th align="left">值</th>
<th align="left">含义</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>KSNODEPIN_AEC_RENDER_IN</p></td>
<td align="left"><p>1</p></td>
<td align="left"><p>接收器 pin (用于呈现流的节点输入) </p></td>
</tr>
<tr class="even">
<td align="left"><p>KSNODEPIN_AEC_RENDER_OUT</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>呈现流 (节点输出) 的源插针</p></td>
</tr>
<tr class="odd">
<td align="left"><p>KSNODEPIN_AEC_CAPTURE_IN</p></td>
<td align="left"><p>2</p></td>
<td align="left"><p>用于捕获流 (节点输入) 的接收器 pin</p></td>
</tr>
<tr class="even">
<td align="left"><p>KSNODEPIN_AEC_CAPTURE_OUT</p></td>
<td align="left"><p>3</p></td>
<td align="left"><p>捕获流 (节点输出) 的源 pin</p></td>
</tr>
</tbody>
</table>

 

上表中的 pin Id 在头文件 Ksmedia 中定义。

下面的代码示例演示了适配器驱动程序如何指定包含 AEC 节点和 NS 节点的 AEC 筛选器的内部拓扑：

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

前面的代码示例中的 AecConnections 数组定义了下图中显示的筛选器拓扑。

![阐释 aec 筛选器内部拓扑的关系图](images/aectopo.png)

上图代表了筛选器内的每个连接，并带有一个指向数据流方向的虚线箭头。 图中总共显示了五个连接。 每个连接都对应于代码示例的 AecConnections 数组中的五个元素之一。

 

