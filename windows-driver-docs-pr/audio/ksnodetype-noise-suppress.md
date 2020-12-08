---
title: KSNODETYPE \_ 干扰 \_
description: KSNODETYPE \_ 干扰 \_
keywords:
- KSNODETYPE_NOISE_SUPPRESS 音频设备
topic_type:
- apiref
api_name:
- KSNODETYPE_NOISE_SUPPRESS
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 95a04e47cc0ac7de6bdd5eff5a99caa9ac1159d8
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96784615"
---
# <a name="ksnodetype_noise_suppress"></a>KSNODETYPE \_ 干扰 \_


## <span id="ddk_ksnodetype_noise_suppress_ks"></span><span id="DDK_KSNODETYPE_NOISE_SUPPRESS_KS"></span>


KSNODETYPE \_ 噪声抑制 \_ 节点表示 (NS) 控制的干扰。 NS 节点具有一个输入流和一个输出流的连接。 这两个流具有相同的格式。

当创建包含 NS 节点的筛选器或重置节点时，该节点最初配置为在传递模式下运行。

NS 节点可以合并到 AEC (声音回声取消) 筛选器，以支持全双工 DirectSound 应用程序。 有关详细信息，请参阅 [DirectSound 捕获效果](./directsound-capture-effects.md)。

\_ \_ AEC 筛选器中的 KSNODETYPE 干扰节点应支持以下属性，以启用硬件加速：

[**KSPROPERTY \_ 音频 \_ CPU \_ 资源**](ksproperty-audio-cpu-resources.md)

[**KSPROPERTY \_ 音频 \_ 算法 \_ 实例**](ksproperty-audio-algorithm-instance.md)

[**KSPROPERTY \_ TOPOLOGYNODE \_ ENABLE**](ksproperty-topologynode-enable.md)

[**KSPROPERTY \_ TOPOLOGYNODE \_ 重置**](ksproperty-topologynode-reset.md)

KSPROPERTY \_ TOPOLOGYNODE \_ enable 属性用于启用和禁用节点。 如果禁用，则节点在传递模式下运行 (也就是说，它允许输入流传递到输出，而无需) 修改。

 

