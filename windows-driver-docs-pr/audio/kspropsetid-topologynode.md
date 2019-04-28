---
title: KSPROPSETID\_TopologyNode
description: KSPROPSETID\_TopologyNode
ms.assetid: 0b6696aa-e80d-4806-9fbb-7de701164877
keywords:
- KSPROPSETID_TopologyNode
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4cec754c4ba7567e511d5692c4324dc65d3daeec
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63332443"
---
# <a name="kspropsetidtopologynode"></a>KSPROPSETID\_TopologyNode


## <span id="ddk_kspropsetid_topologynode_ks"></span><span id="DDK_KSPROPSETID_TOPOLOGYNODE_KS"></span>


`KSPROPSETID_TopologyNode`属性集提供了通用控制各种拓扑节点。 拓扑节点类型的列表，请参阅[音频拓扑节点](audio-topology-nodes.md)。 在此集中的属性可以用于启用、 禁用和重置拓扑节点。

若要公开到系统的 AEC （回声抵消） 硬件加速，音频驱动程序必须实现的 AEC 和干扰抑制节点 ([**KSNODETYPE\_声学\_ECHO\_取消** ](ksnodetype-acoustic-echo-cancel.md)并[ **KSNODETYPE\_干扰\_SUPPRESS**](ksnodetype-noise-suppress.md))，并且必须启用和禁用通过这些节点的支持`KSPROPSETID_TopologyNode`属性。 有关详细信息，请参阅[Exposing Hardware-Accelerated 捕获效果](https://msdn.microsoft.com/library/windows/hardware/ff536379)。

一个[ **KSNODETYPE\_PROLOGIC\_编码器**](ksnodetype-prologic-encoder.md)节点也必须支持`KSPROPSETID_TopologyNode`属性。

`KSPROPSETID_TopologyNode`属性集包含以下属性：

[**KSPROPERTY\_TOPOLOGYNODE\_启用**](ksproperty-topologynode-enable.md)

[**KSPROPERTY\_TOPOLOGYNODE\_重置**](ksproperty-topologynode-reset.md)

 

 





