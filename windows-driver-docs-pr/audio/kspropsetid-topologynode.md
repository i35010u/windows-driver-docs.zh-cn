---
title: KSPROPSETID \_ TopologyNode
description: KSPROPSETID \_ TopologyNode
keywords:
- KSPROPSETID_TopologyNode
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4cedc4777cb8d2b78c9bca7dfc4b812282536e01
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96801061"
---
# <a name="kspropsetid_topologynode"></a>KSPROPSETID \_ TopologyNode


## <span id="ddk_kspropsetid_topologynode_ks"></span><span id="DDK_KSPROPSETID_TOPOLOGYNODE_KS"></span>


`KSPROPSETID_TopologyNode`属性集对各种拓扑节点提供泛型控制。 有关拓扑节点类型的列表，请参阅 [音频拓扑节点](audio-topology-nodes.md)。 此集中的属性可用于启用、禁用和重置拓扑节点。

若要公开 AEC (声音回声取消) 系统的硬件加速，音频驱动程序必须实现 AEC 和干扰关闭节点 ([**KSNODETYPE 的 \_ 声音 \_ 回声 \_ 取消**](ksnodetype-acoustic-echo-cancel.md) 和 [**KSNODETYPE \_ 噪音 \_ 禁止显示**](ksnodetype-noise-suppress.md)) ，并且必须通过属性支持启用和禁用这些节点 `KSPROPSETID_TopologyNode` 。 有关详细信息，请参阅 [公开 Hardware-Accelerated 捕获效果](./exposing-hardware-accelerated-capture-effects.md)。

[**KSNODETYPE \_ PROLOGIC \_ 编码器**](ksnodetype-prologic-encoder.md)节点还必须支持 `KSPROPSETID_TopologyNode` 属性。

`KSPROPSETID_TopologyNode`属性集包含以下属性：

[**KSPROPERTY \_ TOPOLOGYNODE \_ ENABLE**](ksproperty-topologynode-enable.md)

[**KSPROPERTY \_ TOPOLOGYNODE \_ 重置**](ksproperty-topologynode-reset.md)

 

