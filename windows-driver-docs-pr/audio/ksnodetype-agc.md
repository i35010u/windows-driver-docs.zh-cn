---
title: KSNODETYPE \_ AGC
description: KSNODETYPE \_ AGC
keywords:
- KSNODETYPE_AGC 音频设备
topic_type:
- apiref
api_name:
- KSNODETYPE_AGC
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: e33d370dce0db361e25453c756a2da6ea9ef5d3b
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96799181"
---
# <a name="ksnodetype_agc"></a>KSNODETYPE \_ AGC


## <span id="ddk_ksnodetype_agc_ks"></span><span id="DDK_KSNODETYPE_AGC_KS"></span>


KSNODETYPE \_ AGC 节点表示 (AGC) 的自动增益控制。 AGC 节点有一个输入流和一个输出流，两个流中的每一个都具有相同的数据格式。 节点会自动调整应用于输入流的衰减量或收益量，以实现最大动态范围而不剪裁信号。

KSNODETYPE \_ AGC 节点应支持以下属性：

[**KSPROPERTY \_ 音频 \_ AGC**](ksproperty-audio-agc.md)

KSNODETYPE \_ AGC 节点还可以支持以下可选属性：

[**KSPROPERTY \_ TOPOLOGYNODE \_ ENABLE**](ksproperty-topologynode-enable.md)

[**KSPROPERTY \_ TOPOLOGYNODE \_ 重置**](ksproperty-topologynode-reset.md)

KSPROPERTY \_ TOPOLOGYNODE \_ enable 属性用于启用和禁用节点。 如果禁用，则节点在传递模式下运行 (也就是说，它允许输入流传递到输出，而无需) 修改。

 

 





